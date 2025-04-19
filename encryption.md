### **SHA-256 Hashing in Python**

SHA-256 (part of the SHA-2 family) is a cryptographic hash function that generates a 256-bit (32-byte) fixed-size hash. It’s widely used for secure data verification because it’s collision-resistant and ensures integrity.

#### **Implementation**
```python
import hashlib

def sha256_hash(data):
    """
    Generates a SHA-256 hash for the input data.

    Args:
        data (str): The input data to hash.

    Returns:
        str: The SHA-256 hash of the input data as a hexadecimal string.
    """
    # Create a SHA-256 hash object
    sha256 = hashlib.sha256()
    
    # Encode the data to bytes and update the hash object
    sha256.update(data.encode('utf-8'))
    
    # Return the hash in hexadecimal format
    return sha256.hexdigest()

# Example usage
data = "Hello, Blockchain!"
hash_result = sha256_hash(data)
print(f"SHA-256 Hash of '{data}': {hash_result}")
```

#### **Output**
```
SHA-256 Hash of 'Hello, Blockchain!': 916f002de79f6bcf0d1ad6d7387e8cfa9af9b48d94969e410b2e7e172e3e7fdf
```

#### **Key Features of SHA-256:**
- **Fixed Size**: Hashes are always 256 bits (64 hexadecimal characters), regardless of input size.
- **Deterministic**: The same input always produces the same hash.
- **Preimage Resistance**: It’s computationally infeasible to deduce the original data from the hash.

#### **Learning Outcome**
- Understand how SHA-256 ensures data integrity by producing unique hashes for different inputs.
- Learn its application in blockchain, digital signatures, and secure password storage.

---

### **MD5 Hashing in Python**

MD5 (Message Digest Algorithm 5) generates a 128-bit hash (32 hexadecimal characters). It’s fast and suitable for checksums and basic data integrity checks. However, it’s no longer considered cryptographically secure due to vulnerabilities like collisions.

#### **Implementation**
```python
import hashlib

def md5_hash(data):
    """
    Generates an MD5 hash for the input data.

    Args:
        data (str): The input data to hash.

    Returns:
        str: The MD5 hash of the input data as a hexadecimal string.
    """
    # Create an MD5 hash object
    md5 = hashlib.md5()
    
    # Encode the data to bytes and update the hash object
    md5.update(data.encode('utf-8'))
    
    # Return the hash in hexadecimal format
    return md5.hexdigest()

# Example usage
data = "Hello, Blockchain!"
hash_result = md5_hash(data)
print(f"MD5 Hash of '{data}': {hash_result}")
```

#### **Output**
```
MD5 Hash of 'Hello, Blockchain!': 715716dd74b2c1bb6f8b5198d16dc9e3
```

#### **Key Features of MD5:**
- **Fixed Size**: Always 128 bits (32 hexadecimal characters).
- **Fast**: MD5 is computationally less expensive compared to SHA-256.
- **Collision Vulnerability**: Different inputs can produce the same hash (collisions), making it unsuitable for cryptographic purposes.

---

### **Comparison: SHA-256 vs MD5**

| Feature                | SHA-256                          | MD5                              |
|------------------------|-----------------------------------|-----------------------------------|
| **Hash Size**          | 256 bits (64 hex chars)          | 128 bits (32 hex chars)          |
| **Security**           | Highly secure                    | Weak, prone to collisions        |
| **Speed**              | Slower (more computationally intensive) | Faster                          |
| **Use Cases**          | Cryptography, blockchain, secure hashing | Checksums, basic integrity checks |

---

### **Learning Outcomes**
- **SHA-256**: Provides strong cryptographic guarantees for data integrity and verification.
- **MD5**: Useful for fast non-secure hashing but unsuitable for security-critical applications.
  
Both hashing algorithms highlight how hashes can be generated and why certain algorithms are more suited for specific use cases.
