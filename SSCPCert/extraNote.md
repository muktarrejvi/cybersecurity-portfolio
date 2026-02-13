
## RSA Key Length Comparison

- **1024-bit** ❌ Insecure (deprecated)  
- **2048-bit** ✅ Current standard minimum (good for today)  
- **3072-bit** ✅ Stronger long-term protection with reasonable performance  
- **4096-bit** 🔒 Very strong but heavier performance impact  

According to modern cryptographic guidance (e.g., NIST), **RSA 3072-bit** provides security comparable to **128-bit symmetric encryption** and is considered suitable for long-term protection.

### Containerization (C)

Containerization effectively isolates corporate applications and data from personal applications on the same device.

This separation:
- Prevents corporate data leakage
- Maintains security boundaries
- Allows users to continue personal use of the device

It is commonly used in BYOD (Bring Your Own Device) environments to protect organizational data while preserving user privacy
