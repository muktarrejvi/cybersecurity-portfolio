
### Creating a keypair using openssl.
## Command
openssl genrsa -out private-key.pem 2048
## Command Breakdown

| Component                  | Meaning                                      | Explanation |
|---------------------------|----------------------------------------------|-------------|
| `openssl`                 | Main OpenSSL tool                            | Command-line cryptography toolkit |
| `genrsa`                  | Generate RSA private key                     | Sub-command specifically for RSA key generation |
| `-out private-key.pem`    | Output file name                             | Saves the generated key to this file |
| `private-key.pem`         | Output filename with extension               | `.pem` = PEM format (Base64-encoded text file) |
| `2048`                    | Key size in bits                             | Creates a 2048-bit RSA private key |
