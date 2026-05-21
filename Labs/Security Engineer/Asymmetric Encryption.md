
## Creating a keypair using openssl.
### Command
openssl genrsa -out private-key.pem 2048
### Command Breakdown

| Component                  | Meaning                                      | Explanation |
|---------------------------|----------------------------------------------|-------------|
| `openssl`                 | Main OpenSSL tool                            | Command-line cryptography toolkit |
| `genrsa`                  | Generate RSA private key                     | Sub-command specifically for RSA key generation |
| `-out private-key.pem`    | Output file name                             | Saves the generated key to this file |
| `private-key.pem`         | Output filename with extension               | `.pem` = PEM format (Base64-encoded text file) |
| `2048`                    | Key size in bits                             | Creates a 2048-bit RSA private key |

<img width="729" height="173" alt="image" src="https://github.com/user-attachments/assets/764d7e1f-7c4c-4a8d-8587-b458c49c7d82" />

openssl rsa -in private-key.pem -pubout -out public-key.pem
SCREENSHOTS

<img width="733" height="816" alt="image" src="https://github.com/user-attachments/assets/031ab275-5b1f-4d93-88e5-d537ec521bc0" />

Now generating public key.
# OpenSSL RSA Encryption & Decryption

## 1. Generate RSA Key Pair (2048-bit)

```bash
# Generate private key
openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:2048

# Extract public key
openssl rsa -pubout -in private_key.pem -out public_key.pem

# Encrypt a file/message
openssl pkeyutl -encrypt -pubin -inkey public_key.pem -in message.txt -out ciphertext.bin
# Decrypt the ciphertext
openssl pkeyutl -decrypt -inkey private_key.pem -in ciphertext.bin -out decrypted.txt
