# Secure Role-Based Access Control System

## Overview
This project implements a **Secure Role-Based Access Control (RBAC) System** using RSA encryption and bcrypt hashing. The system allows administrators to assign roles and manage users, while authorized users can access encrypted employee data.

## Features
- **RSA Encryption & Decryption**: Employee salary and address are encrypted using RSA (2048-bit).
- **Bcrypt Password Hashing**: Secure storage of user passwords.
- **Role-Based Access Control**: Users can be assigned roles as "Authorized" or "Malicious".
- **Admin Panel**: GUI-based user management for adding and flagging users.
- **User Panel**: GUI-based access request system.
- **Persistent User Data**: Uses a JSON file to store user credentials and roles securely.

## Dependencies
Ensure you have the following Python libraries installed:
```sh
pip install pycryptodome pandas bcrypt ipywidgets
```

## Files & Structure
- `main.py` - The core script implementing the system.
- `user_data.json` - Stores user roles and hashed passwords.
- `rsa_key.pem` - Stores the RSA key for encryption.

## Framework Code

### Data Ingestion Layer
```python
def ingest_employee_data():
    return {
        'employee_1': {'name': 'Alice', 'salary': 50000, 'sensitive_info': 'SSN1234'},
        'employee_2': {'name': 'Bob', 'salary': 60000, 'sensitive_info': 'SSN5678'},
        'employee_3': {'name': 'Charlie', 'salary': 70000, 'sensitive_info': 'SSN9101'},
    }
```

### Encryption Layer
```python
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
import os
from lightphe import LightPHE

def aes_encrypt(data, key):
    cipher = AES.new(key, AES.MODE_CBC)
    ciphertext = cipher.encrypt(pad(data.encode(), AES.block_size))
    return cipher.iv + ciphertext
```

## How It Works
1. **RSA Key Management**:
   - The script generates or loads an RSA key for encrypting sensitive data.
   - Employee salaries and addresses are encrypted using **PKCS1_OAEP**.

2. **User Authentication & Role Management**:
   - Users are stored with a hashed password using bcrypt.
   - Admins can assign or change user roles.
   - Malicious users can be flagged via the Admin Panel.

3. **Admin Panel**:
   - Add new users with a role and password.
   - Flag existing users as malicious.

4. **User Panel**:
   - Users enter their credentials to request access.
   - If authorized, decrypted employee data is displayed.

## Running the System
Run the script and choose between Admin or User mode:
```sh
python main.py
```
- **Admin Mode**: Allows adding and flagging users.
- **User Mode**: Allows access request based on credentials.

## Security Measures
- **Passwords are stored securely** with bcrypt hashing.
- **Data is encrypted** before storage using RSA.
- **Malicious users are flagged** to restrict access.

## Future Improvements
- Implement a database instead of JSON for better scalability.
- Add multi-factor authentication (MFA) for stronger security.
- Use AES for encrypting large datasets efficiently.

## License
This project is open-source and available for use under the MIT License.

---

*Created by Secure Access Control Team* 🚀

