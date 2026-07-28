#  1 Connecting Remote Systems in linux
<img width="886" height="871" alt="sshLinux" src="https://github.com/user-attachments/assets/b11fcf4d-d4a2-4c93-afe5-960fcd86df50" />

#  2. GRUB password generations

<img width="860" height="850" alt="GrubPass" src="https://github.com/user-attachments/assets/7a4d1fd7-75d7-4e29-a199-7a50b68a311a" />

# 3.  LUKS (Linux Unified Key Setup)

<img width="674" height="220" alt="luks" src="https://github.com/user-attachments/assets/8bceccd0-62ac-4cf7-825b-14ab3a9cf981" />


### LUKS Components Overview

- **LUKS Partition Header (phdr)**: Contains the volume’s UUID, the encryption cipher and mode in use, the master-key length, and a checksum of the master key.

- **Key Material (KM1–KM8)**: Up to eight key-material areas, each linked to a key slot. When a slot is marked active in the header, its corresponding KM section stores a copy of the master key that has been encrypted with a user’s passphrase.

- **Bulk Data**: The actual payload encrypted under the master key (which itself is protected by the user passphrases stored in the active key-material sections).
