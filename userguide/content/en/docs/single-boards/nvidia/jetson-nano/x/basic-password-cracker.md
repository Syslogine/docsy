---
linkTitle: Basic Password Cracker
title: Basic Password Cracker with Nvidia Jetson Nano on Ubuntu
description: >
 In this tutorial, we will cover the steps to create a basic password cracker using the Nvidia Jetson Nano on Ubuntu. This tool can be used to test the strength of your own passwords or those of others, and may also have applications in security testing or forensic analysis.
toc_hide: true
hide_summary: true
categories: ["jetson nano"]
---

## Requirements
- Nvidia Jetson Nano with Ubuntu installed
- Python 3.x installed (usually comes pre-installed on most modern distributions)
- A list of passwords to crack (either a plaintext file or a hashed file, depending on the encryption algorithm used)

## Steps
1. Connect your Jetson Nano to a power source and insert an SD card with Ubuntu installed.
2. Power on the device and connect it to a monitor, keyboard, and mouse.
3. Open a terminal window by clicking on the top-left corner of the screen and selecting "Terminal".
4. Update the package lists by running the following command:
   ```
   sudo apt update
   ```
5. Install the `hashcat` password cracking tool by running the following command:
   ```
   sudo apt install hashcat
   ```
6. Create a new directory to store your password files and cracking scripts by running the following command:
   ```
   mkdir password_cracker
   cd password_cracker
   ```
7. Download a list of common passwords from the internet (e.g., [this one](https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/10-million-password-list-top-100k.txt)) and save it to your password_cracker directory.
8. Create a new Python script named `password_cracker.py` in your password_cracker directory by running the following command:
   ```
   nano password_cracker.py
   ```
9. Copy and paste the following code into your password_cracker.py file, replacing the placeholders with your own values:

```python
import hashlib
import os

# Define a function to crack a password hash using a list of common passwords
def crack_hash(hash_value):
    # Load the list of common passwords from a plaintext file
    password_list = open("common_passwords.txt").read().splitlines()
    
    # Loop through each password in the list and compute its hash value using SHA-1 algorithm
    for password in password_list:
        hash_object = hashlib.sha1(password.encode())
        computed_hash_value = hash_object.hexdigest()
        
        # Compare the computed hash value with the input hash value
        if computed_hash_value == hash_value:
            return password
    
    # If no matching password is found, return None
    return None

# Define a main function to read the user's input and display the results
def main():
    print("Basic Password Cracker")
    
    # Read the user's input for the password hash value
    hash_value = input("Enter the hash value of the password to crack: ")
    
    # Call the crack_hash function to attempt to crack the password hash using SHA-1 algorithm
    cracked_password = crack_hash(hash_value)
    
    # Display the results of the password cracking attempt
    if cracked_password is not None:
        print("The cracked password is:", cracked_password)
    else:
        print("Unable to crack the password hash.")

# Run the main function
if __name__ == "__main__":
    main()
```

or

```python
import hashlib
import secrets

def load_password_list(file_path):
    try:
        with open(file_path, "r") as file:
            return file.read().splitlines()
    except FileNotFoundError:
        print("Error: Password file not found.")
        exit()

def crack_hash(hash_value, password_list):
    for password in password_list:
        # Simulate salting by using a random salt
        salt = secrets.token_hex(16)  # 16-byte (32-character) hex salt
        salted_password = salt + password
        hash_object = hashlib.sha256(salted_password.encode())
        computed_hash_value = salt + hash_object.hexdigest()

        # Compare the computed hash value with the input hash value
        if computed_hash_value == hash_value:
            return password

    # If no matching password is found, return None
    return None

def main():
    print("Basic Password Cracker")

    # Read the user's input for the password hash value
    hash_value = input("Enter the hash value of the password to crack: ")

    # Load the list of common passwords from a plaintext file
    password_list = load_password_list("common_passwords.txt")

    # Call the crack_hash function to attempt to crack the password hash
    cracked_password = crack_hash(hash_value, password_list)

    # Display the results of the password cracking attempt
    if cracked_password is not None:
        print("The cracked password is:", cracked_password)
    else:
        print("Unable to crack the password hash.")

# Run the main function
if __name__ == "__main__":
    main()
```

10. Save and exit your password_cracker.py file by pressing `Ctrl+X`, then `Y`, then `Enter`.
11. Run your password_cracker.py script by running the following command:
    ```
    python3 password_cracker.py
    ```
12. Enter the hash value of a password that you want to crack (e.g., the output of the `hashlib.sha1` function when called with a sample password) and press `Enter`.
13. Observe the results of your password cracking attempt, which may include the cracked password if it is found in the list of common passwords.

## Conclusion
In this tutorial, we covered the steps to create a basic password cracker using the Nvidia Jetson Nano on Ubuntu. By following these steps, you should be able to use your new tool to test the strength of passwords and potentially identify weak or easily guessable credentials that could be exploited by attackers.
