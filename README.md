# DTI
Homomorphic-encryption (lightweight partial homomorphic encryption )
### **README: Hybrid Encryption Framework with LightPHE for Employee Data Management**

---

#### **Framework Overview**
This framework demonstrates a secure, scalable, and efficient approach to handling sensitive and non-sensitive employee data in a hybrid encryption setup. By integrating AES for sensitive data encryption and LightPHE for homomorphic computations, it provides robust protection during data ingestion, storage, and processing while ensuring privacy-preserving computations.

---

### **Features**
1. **Secure Data Handling**:
   - Sensitive data is encrypted using AES.
   - Homomorphic encryption (LightPHE) ensures secure processing of non-sensitive data.

2. **Scalable Storage**:
   - Encrypted data is stored in the cloud, simulating scalable storage mechanisms.

3. **Privacy-Preserving Computations**:
   - Perform operations on encrypted data without decrypting it, leveraging homomorphic encryption.

4. **Integrity Auditing**:
   - Auditing and integrity checks via blockchain for compliance and data transparency.

---

### **Framework Architecture**

1. **Data Ingestion Layer**:
   - Allows users to upload sensitive and non-sensitive employee data.
   - Prepares data for encryption.

2. **Encryption Layer**:
   - Applies hybrid encryption:
     - AES for sensitive information.
     - LightPHE for enabling computations on encrypted non-sensitive data.

3. **Storage Layer**:
   - Secures encrypted data in cloud storage for scalable and safe management.

4. **Processing Layer**:
   - Enables computations like payroll calculations directly on encrypted data using LightPHE.

5. **Auditing Layer**:
   - Uses blockchain to log transactions and ensure data integrity.

---

### **Setup and Usage**

#### **Prerequisites**
1. Python 3.8+.
2. Libraries:
   - `pycryptodome` (for AES encryption).
   - `lightphe` (for homomorphic encryption).
3. Blockchain Framework (optional for auditing).
4. Cloud storage API (optional for cloud simulation).

#### **Installation**
Install the required libraries:
```bash
pip install pycryptodome lightphe
```

#### **Usage Steps**
1. **Data Ingestion**:
   - Collect employee data (e.g., name, salary, and sensitive information).

2. **Encryption**:
   - Encrypt sensitive data with AES.
   - Encrypt non-sensitive data (e.g., salary) with LightPHE for secure computations.

3. **Data Storage**:
   - Simulate secure storage by returning encrypted data (or use cloud APIs for actual implementation).

4. **Processing**:
   - Perform homomorphic computations on encrypted data, such as calculating total payroll.

5. **Auditing**:
   - Log changes and ensure integrity using blockchain (conceptual in this implementation).

---

### **Framework Code**

#### **Data Ingestion Layer**
```python
def ingest_employee_data():
    return {
        'employee_1': {'name': 'Alice', 'salary': 50000, 'sensitive_info': 'SSN1234'},
        'employee_2': {'name': 'Bob', 'salary': 60000, 'sensitive_info': 'SSN5678'},
        'employee_3': {'name': 'Charlie', 'salary': 70000, 'sensitive_info': 'SSN9101'},
    }
```

#### **Encryption Layer**
```python
from Crypto.Cipher import AES
from Crypto.Util.Padding import pad
import os
from lightphe import LightPHE

def aes_encrypt(data, key):
    cipher = AES.new(key, AES.MODE_CBC)
    return cipher.iv + cipher.encrypt(pad(data.encode(), AES.block_size))

lightphe_cs = LightPHE(algorithm_name='Paillier')

def encrypt_employee_data(employee_data):
    aes_key = os.urandom(16)
    encrypted_data = {}
    for emp_id, info in employee_data.items():
        encrypted_info = aes_encrypt(info['sensitive_info'], aes_key)
        encrypted_salary = lightphe_cs.encrypt(info['salary'])
        encrypted_data[emp_id] = {
            'name': info['name'],
            'encrypted_salary': encrypted_salary,
            'encrypted_sensitive_info': encrypted_info,
            'aes_key': aes_key,
        }
    return encrypted_data
```

#### **Storage Layer**
```python
def store_encrypted_data(encrypted_data):
    print("Storing encrypted data in cloud...")
    return encrypted_data
```

#### **Processing Layer**
```python
def compute_total_payroll(encrypted_data):
    total = lightphe_cs.encrypt(0)
    for info in encrypted_data.values():
        total += info['encrypted_salary']
    return total

def decrypt_total_payroll(total_encrypted):
    return lightphe_cs.decrypt(total_encrypted)
```

#### **Auditing Layer**
```python
def audit_with_blockchain(encrypted_data):
    print("Auditing data integrity with blockchain...")
```

---

### **Execution**
Run the framework as follows:
```python
if __name__ == "__main__":
    employee_data = ingest_employee_data()
    encrypted_data = encrypt_employee_data(employee_data)
    stored_data = store_encrypted_data(encrypted_data)
    total_payroll_encrypted = compute_total_payroll(stored_data)
    total_payroll_decrypted = decrypt_total_payroll(total_payroll_encrypted)
    print(f"\nTotal Payroll (Decrypted): ${total_payroll_decrypted}")
    audit_with_blockchain(stored_data)
```

---

### **Benefits**
- **Security**: AES ensures confidentiality for sensitive data, while LightPHE provides secure computations.
- **Efficiency**: Lightweight homomorphic encryption is computationally efficient compared to fully homomorphic encryption.
- **Scalability**: Cloud-based architecture supports large-scale data operations.
- **Transparency**: Blockchain auditing enhances trust and compliance.

---

For further inquiries or contributions, please contact the development team or submit a pull request.
