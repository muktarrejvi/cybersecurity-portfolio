# KQL Notes

These are my personal notes for learning **KQL (Kusto Query Language)**. I started writing them while getting comfortable with Microsoft Sentinel and Defender, and kept adding stuff whenever I got stuck on something (which was often).

It's not an official guide. Some parts are rough, some examples are simplified, and I'll probably keep changing things. If you find a mistake, open an issue or just send a PR 🙂

> Most examples use Sentinel / Defender tables (`SigninLogs`, `SecurityEvent`, `DeviceProcessEvents` etc). If you don't have a workspace, the free **Azure Data Explorer help cluster** has a `StormEvents` table you can practice on: https://dataexplorer.azure.com/clusters/help/databases/Samples

---

## Table of contents

1. [What even is KQL](#1-what-even-is-kql)
2. [First query](#2-first-query)
3. [Basic operators](#3-basic-operators)
4. [Filtering with where](#4-filtering-with-where)
5. [Working with time](#5-working-with-time)
6. [project, extend, and friends](#6-project-extend-and-friends)
7. [summarize (the important one)](#7-summarize-the-important-one)
8. [Sorting and limiting](#8-sorting-and-limiting)
9. [Strings](#9-strings)
10. [let statements](#10-let-statements)
11. [Joins](#11-joins)
12. [union](#12-union)
13. [Dynamic / JSON columns](#13-dynamic--json-columns)
14. [Charts](#14-charts)
15. [Time series stuff](#15-time-series-stuff)
16. [Parsing messy logs](#16-parsing-messy-logs)
17. [Functions](#17-functions)
18. [Threat hunting examples](#18-threat-hunting-examples)
19. [Performance tips (learned the hard way)](#19-performance-tips-learned-the-hard-way)
20. [Cheat sheet](#20-cheat-sheet)
21. [Resources](#21-resources)

---

## 1. What even is KQL

KQL is a **read-only** query language made by Microsoft. You use it in:

- Azure Data Explorer (ADX)
- Log Analytics / Azure Monitor
- Microsoft Sentinel
- Microsoft Defender XDR (Advanced Hunting)
- Fabric Real-Time Intelligence

The thing that made it click for me: **data flows top to bottom through pipes (`|`)**. Each line takes the output of the line above and does something to it. Kind of like bash piping.

```
Table
| do something
| then do something else
| then this
```

If you know SQL it helps a bit, but honestly don't try to translate everything from SQL in your head. It'll slow you down. (There's a SQL→KQL cheat sheet in the docs though, see resources.)

KQL is case-sensitive for table names, column names and operators. `where` works, `Where` doesn't. This bit me more than once.

---

## 2. First query

Simplest possible query — just the table name:

```kql
SigninLogs
```

Don't actually run that on a big workspace, it'll try to return everything (well, it gets capped, but still). Do this instead:

```kql
SigninLogs
| take 10
```

`take` (or `limit`, same thing) gives you some random rows. Good for just seeing what columns exist.

Another handy one to see the schema:

```kql
SigninLogs
| getschema
```

And to count rows:

```kql
SigninLogs
| count
```

---

## 3. Basic operators

The ones I use like 90% of the time:

| Operator | What it does |
|---|---|
| `where` | filter rows |
| `project` | pick columns |
| `extend` | add new calculated column |
| `summarize` | group + aggregate |
| `sort by` / `order by` | sort |
| `top` | sort + take in one go |
| `take` / `limit` | grab N rows |
| `count` | count rows |
| `distinct` | unique values |
| `join` | combine tables |
| `union` | stack tables |
| `render` | make a chart |

Comments use `//`

```kql
// this is a comment
SecurityEvent
| take 5 // this too
```

---

## 4. Filtering with where

```kql
SecurityEvent
| where EventID == 4625
```

4625 = failed logon on Windows. You'll see this one a lot.

Multiple conditions:

```kql
SecurityEvent
| where EventID == 4625 and Account contains "admin"
```

Or just stack `where`s, which I find easier to read:

```kql
SecurityEvent
| where EventID == 4625
| where Account contains "admin"
```

### Comparison operators

- `==` equals (case sensitive for strings)
- `!=` not equals
- `=~` equals, **case insensitive** (use this for usernames etc)
- `!~` not equals, case insensitive
- `<`, `>`, `<=`, `>=`

### in / !in

```kql
SecurityEvent
| where EventID in (4624, 4625, 4634)
```

Case-insensitive version is `in~`:

```kql
SigninLogs
| where UserPrincipalName in~ ("Alice@contoso.com", "bob@contoso.com")
```

### isempty / isnotempty

```kql
SigninLogs
| where isnotempty(IPAddress)
```

### between

```kql
StormEvents
| where DamageProperty between (1000 .. 50000)
```

Note the two dots `..` — I kept typing a comma here at first.

---

## 5. Working with time

Time filtering is basically the most important thing for performance. **Always filter on time first.**

```kql
SigninLogs
| where TimeGenerated > ago(1h)
```

`ago()` accepts:
- `d` days
- `h` hours
- `m` minutes
- `s` seconds
- `ms` milliseconds

```kql
| where TimeGenerated > ago(7d)
| where TimeGenerated > ago(30m)
```

Specific range:

```kql
SecurityEvent
| where TimeGenerated between (datetime(2026-01-01) .. datetime(2026-01-07))
```

`now()` gives current time in UTC. Everything in KQL is UTC by default btw, keep that in mind when someone says "it happened at 3pm".

### Useful time functions

```kql
SigninLogs
| where TimeGenerated > ago(1d)
| extend Hour = hourofday(TimeGenerated)
| extend Day = dayofweek(TimeGenerated)   // returns a timespan, 0d = Sunday
| extend DateOnly = startofday(TimeGenerated)
| project TimeGenerated, Hour, Day, DateOnly
```

Converting to local time (Melbourne for me):

```kql
| extend LocalTime = datetime_utc_to_local(TimeGenerated, "Australia/Melbourne")
```

### bin()

`bin()` rounds time down into buckets. You'll use it with summarize all the time.

```kql
| summarize count() by bin(TimeGenerated, 1h)
```

---

## 6. project, extend, and friends

### project

Pick which columns you want (and in what order):

```kql
SigninLogs
| project TimeGenerated, UserPrincipalName, IPAddress, ResultType
```

Rename while projecting:

```kql
| project Time = TimeGenerated, User = UserPrincipalName
```

### project-away

Remove columns, keep the rest:

```kql
| project-away TenantId, SourceSystem
```

### project-rename

```kql
| project-rename User = UserPrincipalName
```

### project-reorder

```kql
| project-reorder UserPrincipalName, IPAddress
```

(puts these first, everything else after)

### extend

Adds a new column, keeps all old ones.

```kql
StormEvents
| extend TotalDamage = DamageProperty + DamageCrops
| extend Duration = EndTime - StartTime
```

### iff and case

`iff` is if/else:

```kql
SigninLogs
| extend Status = iff(ResultType == "0", "Success", "Failed")
```

`case` for multiple:

```kql
StormEvents
| extend Severity = case(
    DamageProperty > 1000000, "High",
    DamageProperty > 10000, "Medium",
    "Low"
)
```

The last value is the default. Forgot it once and got an error that took me way too long to figure out.

---

## 7. summarize (the important one)

Honestly this is where KQL gets useful. `summarize` = group by + aggregate.

```kql
SecurityEvent
| where TimeGenerated > ago(1d)
| where EventID == 4625
| summarize FailedCount = count() by Account
```

### Common aggregation functions

| Function | Does |
|---|---|
| `count()` | row count |
| `countif(condition)` | count only matching |
| `dcount(col)` | distinct count (approximate!) |
| `sum(col)` | sum |
| `avg(col)` | average |
| `min(col)` / `max(col)` | min / max |
| `make_set(col)` | list of unique values |
| `make_list(col)` | list of all values |
| `arg_max(col, *)` | row with the max value |
| `arg_min(col, *)` | row with the min value |
| `percentile(col, 95)` | percentile |
| `take_any(col)` | any value (used to be `any()`) |

Multiple at once:

```kql
SigninLogs
| where TimeGenerated > ago(1d)
| summarize
    Total = count(),
    Failed = countif(ResultType != "0"),
    UniqueIPs = dcount(IPAddress),
    IPs = make_set(IPAddress)
    by UserPrincipalName
```

### arg_max — get the latest record per thing

This one is super common. "Give me the most recent sign-in for every user":

```kql
SigninLogs
| where TimeGenerated > ago(7d)
| summarize arg_max(TimeGenerated, *) by UserPrincipalName
```

The `*` means bring all the other columns from that row. Really handy for deduping.

### Grouping by time

```kql
SecurityEvent
| where TimeGenerated > ago(1d)
| summarize count() by bin(TimeGenerated, 1h), EventID
```

⚠️ Note: `dcount()` is an estimate. For small numbers it's basically exact but don't use it for something where you need an exact number. `count_distinct()` exists if you really need it (slower).

---

## 8. Sorting and limiting

```kql
StormEvents
| sort by DamageProperty desc
| take 10
```

Same thing but shorter:

```kql
StormEvents
| top 10 by DamageProperty desc
```

Default sort is **descending**, which confused me since SQL is ascending. Just always write `asc` or `desc` to be safe.

Sort by multiple:

```kql
| sort by State asc, DamageProperty desc
```

### distinct

```kql
SigninLogs
| distinct UserPrincipalName, AppDisplayName
```

---

## 9. Strings

KQL has a lot of string operators and it matters which one you pick (performance-wise, see section 19).

| Operator | Meaning | Case sensitive? |
|---|---|---|
| `has` | contains whole term | no |
| `has_cs` | contains whole term | yes |
| `contains` | contains substring | no |
| `contains_cs` | contains substring | yes |
| `startswith` | starts with | no |
| `endswith` | ends with | no |
| `matches regex` | regex match | yes |
| `has_any` | has any of a list | no |
| `has_all` | has all of a list | no |

Negate most of them with `!` → `!has`, `!contains`, `!startswith`

### has vs contains

This took me a while. `has` looks for whole **terms** (words separated by non-alphanumeric chars). `contains` looks for any substring.

- `"powershell.exe -enc abc"` **has** `"powershell"` → true
- `"mypowershelltool"` **has** `"powershell"` → false
- `"mypowershelltool"` **contains** `"powershell"` → true

`has` is way faster because it uses the index. Use it when you can.

```kql
DeviceProcessEvents
| where ProcessCommandLine has_any ("-enc", "-encodedcommand", "frombase64string")
```

### String functions

```kql
| extend lower = tolower(UserPrincipalName)
| extend upper = toupper(UserPrincipalName)
| extend len = strlen(UserPrincipalName)
| extend part = substring(UserPrincipalName, 0, 5)
| extend domain = tostring(split(UserPrincipalName, "@")[1])
| extend joined = strcat(FirstName, " ", LastName)
| extend cleaned = trim(" ", SomeColumn)
| extend replaced = replace_string(SomeColumn, "old", "new")
```

### Regex

```kql
| extend ip = extract(@"(\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})", 1, RawData)
```

Tip: use `@"..."` for regex so you don't have to double-escape backslashes. Wasted an hour on this before I learned it.

---

## 10. let statements

`let` = variables. Makes queries way cleaner.

```kql
let lookback = 7d;
let threshold = 20;
SecurityEvent
| where TimeGenerated > ago(lookback)
| where EventID == 4625
| summarize Failures = count() by Account
| where Failures > threshold
```

Don't forget the `;` at the end of each let. The error message when you forget isn't very helpful.

### let with a list

```kql
let suspiciousProcs = dynamic(["mimikatz.exe", "procdump.exe", "psexec.exe"]);
DeviceProcessEvents
| where FileName in~ (suspiciousProcs)
```

### let with a whole query (tabular)

```kql
let FailedUsers = SigninLogs
    | where TimeGenerated > ago(1d)
    | where ResultType != "0"
    | distinct UserPrincipalName;
SigninLogs
| where TimeGenerated > ago(1d)
| where ResultType == "0"
| where UserPrincipalName in (FailedUsers)
```

That finds users who failed AND succeeded in the last day. Could be password spray that worked… or just someone who typos a lot lol.

### let with a function (lambda)

```kql
let isPrivate = (ip:string) {
    ipv4_is_private(ip)
};
SigninLogs
| extend Private = isPrivate(IPAddress)
```

---

## 11. Joins

Joins confused me for the longest time, mainly because **the default join kind in KQL is NOT inner join**. It's `innerunique`, which dedupes the left side first. So always specify `kind=`.

```kql
TableA
| join kind=inner (TableB) on CommonColumn
```

### Join kinds

| kind | What you get |
|---|---|
| `innerunique` | default. left side deduped, then inner |
| `inner` | normal inner join |
| `leftouter` | all left rows + matches |
| `rightouter` | all right rows + matches |
| `fullouter` | everything |
| `leftanti` | left rows with NO match (super useful) |
| `rightanti` | right rows with no match |
| `leftsemi` | left rows that DO match (only left columns) |

### Example — process + network

```kql
let procs = DeviceProcessEvents
    | where TimeGenerated > ago(1d)
    | where FileName =~ "powershell.exe"
    | project DeviceId, ProcessId, ProcessCommandLine, ProcTime = TimeGenerated;
let conns = DeviceNetworkEvents
    | where TimeGenerated > ago(1d)
    | project DeviceId, InitiatingProcessId, RemoteIP, RemoteUrl, ConnTime = TimeGenerated;
procs
| join kind=inner (conns) on DeviceId, $left.ProcessId == $right.InitiatingProcessId
| project ProcTime, ConnTime, DeviceId, ProcessCommandLine, RemoteIP, RemoteUrl
```

When column names differ, use `$left.X == $right.Y`.

### leftanti example — new stuff

"Which IPs signed in today that we've never seen in the past 30 days?"

```kql
let known = SigninLogs
    | where TimeGenerated between (ago(30d) .. ago(1d))
    | distinct IPAddress;
SigninLogs
| where TimeGenerated > ago(1d)
| distinct IPAddress, UserPrincipalName
| join kind=leftanti (known) on IPAddress
```

### Join tips

- Put the **smaller table on the left**. (Or use hints, see perf section.)
- Filter both sides BEFORE joining.
- Project only columns you need before the join.

---

## 12. union

Stacks tables on top of each other.

```kql
union SecurityEvent, Syslog
| where TimeGenerated > ago(1h)
| take 10
```

See which table each row came from:

```kql
union withsource=SourceTable SigninLogs, AADNonInteractiveUserSignInLogs
| where TimeGenerated > ago(1h)
| summarize count() by SourceTable
```

Wildcards work too (careful, can be slow):

```kql
union Device*
| where TimeGenerated > ago(10m)
| summarize count() by Type
```

---

## 13. Dynamic / JSON columns

Lots of Sentinel columns are JSON (type `dynamic`). E.g. `LocationDetails` in `SigninLogs`.

Dot notation:

```kql
SigninLogs
| extend City = tostring(LocationDetails.city)
| extend Country = tostring(LocationDetails.countryOrRegion)
```

Bracket notation (needed if the key has weird chars):

```kql
| extend City = tostring(LocationDetails["city"])
```

Always wrap in `tostring()` / `toint()` etc, otherwise you get a dynamic type back and `summarize by` will complain.

### parse_json

If JSON is stored as a string:

```kql
| extend parsed = parse_json(AdditionalFields)
| extend Something = tostring(parsed.SomeKey)
```

### mv-expand

Turns an array into multiple rows. One row per element.

```kql
SigninLogs
| where TimeGenerated > ago(1d)
| mv-expand ConditionalAccessPolicies
| extend PolicyName = tostring(ConditionalAccessPolicies.displayName)
| extend PolicyResult = tostring(ConditionalAccessPolicies.result)
| summarize count() by PolicyName, PolicyResult
```

### bag_unpack

Explodes a property bag into columns:

```kql
datatable(d:dynamic)
[
    dynamic({"name":"alice","role":"admin"}),
    dynamic({"name":"bob","role":"user"})
]
| evaluate bag_unpack(d)
```

### datatable — for testing

Quick way to make fake data without a real table. I use this all the time when testing stuff:

```kql
datatable(User:string, Attempts:int)
[
    "alice", 3,
    "bob", 25,
    "carol", 1
]
| where Attempts > 5
```

---

## 14. Charts

Add `render` at the end.

```kql
SecurityEvent
| where TimeGenerated > ago(1d)
| summarize count() by bin(TimeGenerated, 1h)
| render timechart
```

Other types:
- `timechart`
- `barchart` / `columnchart`
- `piechart`
- `areachart`
- `scatterchart`
- `table`

```kql
SigninLogs
| where TimeGenerated > ago(7d)
| summarize count() by AppDisplayName
| top 10 by count_
| render piechart
```

(`count_` is the auto name when you don't name the `count()` column)

Some options:

```kql
| render timechart with (title="Failed logons per hour", ytitle="Count")
```

Note: in Defender Advanced Hunting, render support is more limited than in ADX. Sometimes you just have to click the chart button instead.

---

## 15. Time series stuff

Getting more advanced here. I'm still learning this part honestly.

### make-series

Like summarize but fills in empty time buckets with a default (0). Important for anomaly detection because gaps break things.

```kql
SecurityEvent
| where TimeGenerated > ago(14d)
| where EventID == 4625
| make-series Failures = count() default = 0 on TimeGenerated from ago(14d) to now() step 1h
| render timechart
```

### Anomaly detection

```kql
let series = SecurityEvent
    | where TimeGenerated > ago(14d)
    | where EventID == 4625
    | make-series Failures = count() default = 0 on TimeGenerated from ago(14d) to now() step 1h;
series
| extend (anomalies, score, baseline) = series_decompose_anomalies(Failures, 1.5, -1, 'linefit')
| render anomalychart with (anomalycolumns=anomalies)
```

The `1.5` is the sensitivity threshold. Lower = more anomalies flagged. I usually play with it between 1.5 and 3.

To get the anomalies out as rows instead of a chart:

```kql
series
| extend (anomalies, score, baseline) = series_decompose_anomalies(Failures, 1.5, -1, 'linefit')
| mv-expand TimeGenerated to typeof(datetime), Failures to typeof(long), anomalies to typeof(int), score to typeof(double)
| where anomalies != 0
```

### Other series functions worth knowing

- `series_fit_line()` — trend
- `series_stats()` — min/max/avg etc on the array
- `series_outliers()`
- `series_fill_linear()` — fill gaps

---

## 16. Parsing messy logs

For Syslog / CommonSecurityLog / custom logs that are just one big string.

### parse

```kql
let logs = datatable(RawData:string)
[
    "User=alice Action=login Src=10.0.0.5 Result=fail",
    "User=bob Action=login Src=10.0.0.8 Result=success"
];
logs
| parse RawData with "User=" User " Action=" Action " Src=" SrcIP " Result=" Result
```

Kind of like a template. Works great when the format is consistent. When it's not… pain.

### parse with kind=regex

```kql
| parse kind=regex RawData with @"User=" User @"\s+Action="
```

### extract

Grab one thing with regex:

```kql
| extend Port = extract(@"port\s(\d+)", 1, SyslogMessage)
```

### parse-kv

Newer operator, for key=value stuff:

```kql
logs
| parse-kv RawData as (User:string, Action:string, Src:string, Result:string) with (pair_delimiter=" ", kv_delimiter="=")
```

### split

```kql
| extend parts = split(RawData, " ")
| extend FirstPart = tostring(parts[0])
```

---

## 17. Functions

### Built-in handy ones

```kql
| extend geo = geo_info_from_ip_address(IPAddress)
| extend Country = tostring(geo.country)
```

```kql
| extend IsPrivate = ipv4_is_private(IPAddress)
| extend InRange = ipv4_is_in_range(IPAddress, "10.0.0.0/8")
```

```kql
| extend hash = hash_sha256(SomeString)
| extend b64 = base64_decode_tostring(EncodedString)
```

That last one is gold for decoding encoded PowerShell. Well, mostly — PowerShell `-enc` is UTF-16LE so sometimes the output looks weird with spaces/nulls between chars. There's `base64_decode_toarray()` if you need to deal with the bytes yourself.

### Saved functions

In Log Analytics / Sentinel you can save a query as a function and call it like a table. Really good for parsers (that's how ASIM parsers work).

In ADX:

```kql
.create-or-alter function with (folder="Hunting") FailedLogons(lookback:timespan) {
    SecurityEvent
    | where TimeGenerated > ago(lookback)
    | where EventID == 4625
}
```

Then:

```kql
FailedLogons(1d)
| summarize count() by Account
```

(The `.create` commands are management commands, only in ADX, not in Sentinel query window. In Sentinel you save via the UI.)

---

## 18. Threat hunting examples

The fun part. These are simplified starting points, **tune them for your environment** before making them analytics rules or you'll drown in false positives. Ask me how I know.

### Brute force — many failures from one IP

```kql
let threshold = 30;
SigninLogs
| where TimeGenerated > ago(1h)
| where ResultType != "0"
| summarize
    Attempts = count(),
    Users = dcount(UserPrincipalName),
    UserList = make_set(UserPrincipalName, 50)
    by IPAddress
| where Attempts > threshold
| sort by Attempts desc
```

### Password spray — one IP, many users, few attempts each

```kql
SigninLogs
| where TimeGenerated > ago(1d)
| where ResultType in ("50126", "50053")   // bad password, locked
| summarize Users = dcount(UserPrincipalName), Attempts = count() by IPAddress
| where Users > 10
| extend AttemptsPerUser = round(todouble(Attempts) / Users, 2)
| where AttemptsPerUser < 3
```

### Spray that worked

```kql
let sprayIPs = SigninLogs
    | where TimeGenerated > ago(1d)
    | where ResultType == "50126"
    | summarize Users = dcount(UserPrincipalName) by IPAddress
    | where Users > 10
    | project IPAddress;
SigninLogs
| where TimeGenerated > ago(1d)
| where ResultType == "0"
| where IPAddress in (sprayIPs)
| project TimeGenerated, UserPrincipalName, IPAddress, AppDisplayName
```

### Impossible travel (basic version)

```kql
SigninLogs
| where TimeGenerated > ago(1d)
| where ResultType == "0"
| extend Country = tostring(LocationDetails.countryOrRegion)
| where isnotempty(Country)
| sort by UserPrincipalName asc, TimeGenerated asc
| extend PrevCountry = prev(Country), PrevTime = prev(TimeGenerated), PrevUser = prev(UserPrincipalName)
| where UserPrincipalName == PrevUser and Country != PrevCountry
| extend MinutesBetween = datetime_diff('minute', TimeGenerated, PrevTime)
| where MinutesBetween < 120
| project UserPrincipalName, PrevCountry, Country, PrevTime, TimeGenerated, MinutesBetween
```

`prev()` needs the data to be sorted first ("serialized"). The `sort by` does that. Note VPNs will make this noisy.

### Encoded PowerShell

```kql
DeviceProcessEvents
| where Timestamp > ago(7d)
| where FileName in~ ("powershell.exe", "pwsh.exe")
| where ProcessCommandLine has_any ("-enc", "-encodedcommand", "-e ")
| project Timestamp, DeviceName, AccountName, ProcessCommandLine, InitiatingProcessFileName
```

(Defender uses `Timestamp`, Sentinel uses `TimeGenerated`. Yes it's annoying.)

### LSASS access (credential dumping)

```kql
DeviceEvents
| where Timestamp > ago(7d)
| where ActionType == "OpenProcessApiCall"
| where FileName =~ "lsass.exe"
| where InitiatingProcessFileName !in~ ("MsMpEng.exe", "svchost.exe")   // add your own exclusions
| project Timestamp, DeviceName, InitiatingProcessFileName, InitiatingProcessCommandLine
```

### New local admin added

```kql
SecurityEvent
| where TimeGenerated > ago(7d)
| where EventID == 4732
| where TargetUserName in~ ("Administrators", "Administratoren")
| project TimeGenerated, Computer, SubjectUserName, MemberName, TargetUserName
```

### Audit log cleared

```kql
SecurityEvent
| where TimeGenerated > ago(30d)
| where EventID == 1102
| project TimeGenerated, Computer, SubjectUserName
```

### Rare processes across the fleet

```kql
DeviceProcessEvents
| where Timestamp > ago(7d)
| summarize Devices = dcount(DeviceId), FirstSeen = min(Timestamp) by FileName, SHA256
| where Devices <= 2
| sort by FirstSeen desc
```

### Mailbox forwarding rule created

```kql
OfficeActivity
| where TimeGenerated > ago(7d)
| where Operation in ("New-InboxRule", "Set-InboxRule")
| where Parameters has_any ("ForwardTo", "RedirectTo", "ForwardAsAttachmentTo")
| project TimeGenerated, UserId, ClientIP, Parameters
```

### TODO
- [ ] add DNS tunneling query
- [ ] add OAuth consent grant hunting
- [ ] kerberoasting (4769 with RC4)

---

## 19. Performance tips (learned the hard way)

1. **Filter on time first.** Always. First line after the table.
2. **`where` early, `project` early.** Less data = faster everything.
3. **`has` beats `contains`.** `has` uses the term index. `contains` scans.
4. **`==` beats `=~`** when you know the exact case.
5. **Avoid `*` in `search`** across all tables unless you really have to.
6. **Filter before join**, and keep the smaller table on the left.
7. For big joins where the right side is small, try:
   ```kql
   | join hint.strategy=broadcast kind=inner (SmallTable) on Key
   ```
8. **`dcount()` over `count_distinct()`** unless you need exact numbers.
9. **Don't `mv-expand` huge arrays** unless needed — it multiplies rows.
10. **`materialize()`** if you reference the same let-query multiple times:
    ```kql
    let data = materialize(
        SigninLogs
        | where TimeGenerated > ago(1d)
        | project UserPrincipalName, IPAddress, ResultType
    );
    data | summarize count() by ResultType
    ```
11. Regex is slow. Use it last, after other filters have cut down the data.
12. Use the query stats / "Query details" in the UI to see what's actually expensive.

---

## 20. Cheat sheet

Quick copy-paste stuff.

```kql
// peek
T | take 10

// schema
T | getschema

// last hour
T | where TimeGenerated > ago(1h)

// count by column
T | summarize count() by Col

// top 10
T | summarize c = count() by Col | top 10 by c desc

// latest per entity
T | summarize arg_max(TimeGenerated, *) by Entity

// over time chart
T | summarize count() by bin(TimeGenerated, 1h) | render timechart

// unique list
T | summarize make_set(Col) by Other

// new values not seen before
T | where TimeGenerated > ago(1d) | distinct X
| join kind=leftanti (T | where TimeGenerated between (ago(30d)..ago(1d)) | distinct X) on X

// JSON field
T | extend v = tostring(Json.key)

// array to rows
T | mv-expand ArrayCol

// if / else
T | extend r = iff(x > 5, "big", "small")

// search everywhere (slow!!)
search "10.1.2.3"
| where TimeGenerated > ago(1d)
```

### SQL → KQL quick mapping

| SQL | KQL |
|---|---|
| `SELECT a, b` | `project a, b` |
| `WHERE` | `where` |
| `GROUP BY` | `summarize ... by` |
| `ORDER BY` | `sort by` |
| `TOP 10` / `LIMIT 10` | `take 10` / `top 10 by` |
| `COUNT(DISTINCT x)` | `dcount(x)` |
| `CASE WHEN` | `case()` |
| `LIKE '%x%'` | `contains "x"` |
| `IS NULL` | `isnull()` / `isempty()` |
| `UNION ALL` | `union` |
| `WITH cte AS` | `let cte = ...;` |

You can also run `EXPLAIN` in ADX with a SQL query and it'll show you the KQL version. Nice trick for learning.

---

## 21. Resources

Stuff that actually helped me:

- **Official docs** — https://learn.microsoft.com/en-us/kusto/query/
- **SQL to KQL cheat sheet** — https://learn.microsoft.com/en-us/kusto/query/sql-cheat-sheet
- **ADX help cluster (free practice)** — https://dataexplorer.azure.com/clusters/help/databases/Samples
- **Kusto Detective Agency** — https://detective.kusto.io/ — gamified, genuinely fun, do it
- **Microsoft Sentinel GitHub** (tons of real queries) — https://github.com/Azure/Azure-Sentinel
- **Must Learn KQL** by Rod Trent — search it, great free series
- **KQL Search** — https://www.kqlsearch.com/ — community query search
- **Microsoft Defender Hunting Queries** — https://github.com/microsoft/Microsoft-365-Defender-Hunting-Queries (older, archived, but still useful for ideas)

### How I'd learn it if starting again

1. Do the first few chapters of the docs tutorial on the help cluster (`StormEvents`)
2. Get comfortable with `where`, `project`, `summarize`, `sort` — that's most of daily work
3. Do Kusto Detective Agency season 1
4. Learn `let`, `join`, `mv-expand`
5. Take real Sentinel detection rules from GitHub and pull them apart line by line
6. Write your own hunting queries for your environment
7. Then time series / anomaly stuff

---

*Last updated: whenever I remember to update it.*
*If this helped, a ⭐ would be nice. If it didn't, well, sorry 😅*
