# Encryption-Tool

## Overview 
The Python script provides a simple command-line interface for encrypting and decrypting files using the Fernet symmetric encryption algorithm from the cryptography library. The encryption keys are stored in an SQLite database for easy retrieval during the decryption process.

## Prerequisites
- Python 3.x
- cryptography library (pip install cryptography)

## Security
The encryption keys are stored in an SQLite database, which is encrypted using the DATABASE_PASSWORD environment variable.
The script uses the cryptography library, which provides secure encryption algorithms and key management.

## Code
This code is a Python script that provides functionality for encrypting and decrypting files using the Fernet symmetric encryption algorithm from the `cryptography` library. It also stores the encryption keys in an SQLite database.

Explanation of the code with some redacted parts:

```python
import os
import sqlite3
from cryptography.fernet import Fernet, InvalidToken
import uuid
import getpass
```

This section imports the necessary modules for the script, including `os` for interacting with the operating system, `sqlite3` for working with SQLite databases, `Fernet` and `InvalidToken` from `cryptography.fernet` for encryption and decryption, `uuid` for generating unique identifiers, and `getpass` for securely prompting the user for a password.

```python
# SQLite database file
DATABASE_FILE = 'keys.db'
DATABASE_PASSWORD = os.getenv('DATABASE_PASSWORD')  # Get the database password from an environment variable
```

This part specifies the name of the SQLite database file (`keys.db`) and retrieves the database password from an environment variable. The database password is kept confidential for security reasons.

```python
# Create the SQLite database and table if they don't exist
conn = sqlite3.connect(DATABASE_FILE)
c = conn.cursor()
c.execute('''CREATE TABLE IF NOT EXISTS encryption_keys
             (id TEXT PRIMARY KEY, file_name TEXT, key BLOB)''')
conn.commit()
```

This code creates a connection to the SQLite database and a table named `encryption_keys` if it doesn't already exist. The table has three columns: `id` (a unique identifier), `file_name` (the name of the encrypted file), and `key` (the encryption key stored as a BLOB).

```python
def generate_key():
    """Generate a new encryption key"""
    return Fernet.generate_key()
```

This function generates a new encryption key using `Fernet.generate_key()`.

```python
def encrypt_file(file_path):
    """Encrypt a file and store the encryption key in the database"""
    # ... (code redacted for confidentiality)
```

The `encrypt_file` function takes a file path as input, generates a new encryption key, encrypts the file using the `Fernet` algorithm, and stores the encrypted data in a new file with the `.encrypted` extension. It also stores the encryption key in the SQLite database, associating it with the file name and a unique identifier.

```python
def decrypt_file(file_path):
    """Decrypt a file using the encryption key from the database"""
    # ... (code redacted for confidentiality)
```

The `decrypt_file` function takes an encrypted file path as input, retrieves the corresponding encryption key from the SQLite database, and attempts to decrypt the file using the `Fernet` algorithm. If the decryption is successful, it stores the decrypted data in a new file without the `.encrypted` extension.

```python
def main():
    while True:
        action = input("Enter 'e' to encrypt a file, 'd' to decrypt a file, or 'q' to quit: ").lower()
        # ... (code redacted for confidentiality)

if __name__ == "__main__":
    main()
```

The `main` function provides a simple command-line interface for the user to encrypt or decrypt files by entering 'e', 'd', or 'q' respectively. The `if __name__ == "__main__":` block ensures that the `main` function is executed only when the script is run directly, and not when it is imported as a module.

## Notes 
Some parts of the code have been redacted for confidentiality reasons.

## License
This project is licensed under the MIT License.

