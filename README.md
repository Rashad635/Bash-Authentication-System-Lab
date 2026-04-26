## Bash Authentication System Lab

**Date: April 26, 2026**

#

**Objective**

The goal of this lab was to develop a functional command-line authentication system using Bash scripting on Kali Linux. The script focuses on implementing secure user registration (Sign Up) and authentication (Sign In) processes. Key learning objectives included handling user input, implementing password hashing with salts to prevent rainbow table attacks, and managing persistent data storage using flat files for users and activity logs.

**Ethical and legal scope**

This lab was conducted for educational purposes within a local, controlled environment. The script handles simulated user data and is intended to demonstrate the logic behind authentication workflows and secure credential storage. No real-world production data or external systems were involved.

**Tools used**

- Kali Linux: Development environment
- GNU nano 8.7.1: Text editor for scripting
- Bash: Shell scripting language
- OpenSSL: Used for generating salts and SHA-256 password hashing
- Grep/Awk/Cut: Text processing tools for data retrieval

**Process**

**Step 1:** Script Initialization and Variable Setup
The script defines the data storage files (users.txt and log.txt) and ensures they exist using the touch command. It sets up the environment to use the Bash interpreter.

#

**Step 2:** Implementing the Hashing Function
To ensure passwords are not stored in plaintext, a hash() function was created. It generates a random 10-character hex salt and combines it with the password before hashing it with SHA-256.

#

**Step 3:** Creating the Signup Function
The signup() function prompts for a username and checks if it already exists in users.txt using grep. If the user is unique, it prompts for a password, confirms it, and appends the salt and hash to the user file.

Screenshot:
<img width="1080" height="765" alt="1" src="https://github.com/user-attachments/assets/8c5d5538-a59c-4aca-9dca-b79d0e5eb938" />


<img width="1082" height="767" alt="2" src="https://github.com/user-attachments/assets/fd650975-e8a7-4dc8-8bb2-832aca09e646" />

#

**Step 4:** Creating the Signin Function
The signin() function handles user authentication. It retrieves the stored salt and hash for a given username, hashes the newly entered password with the stored salt, and compares the results to grant or deny access.

Screenshot:
<img width="1077" height="768" alt="3" src="https://github.com/user-attachments/assets/af75143c-c062-4462-a851-742b738aa729" />

#

**Step 5:** Implementing the Main Menu
A select loop and case statement were implemented to provide a user-friendly interface for choosing between Sign Up, Sign In, or Exit.

Screenshot:
<img width="1081" height="765" alt="4" src="https://github.com/user-attachments/assets/ce7d2e42-e7ef-4e67-8ee2-a324e41c0e89" />

#

**Step 6:** Running and Testing the Script
The script was executed to verify the workflow. A user "Rashad" was created, and a successful login was performed.

Screenshot:
<img width="1080" height="768" alt="5" src="https://github.com/user-attachments/assets/03c34883-52d9-4d1d-964d-69cee1eab7b2" />

#

**Step 7:** Testing Error Handling and Security Logic
To ensure robustness, the script was tested against duplicate usernames and incorrect credentials. The system correctly identified that the user "Rashad" already existed and denied a login attempt for a non-existent or incorrect user ("Adam").

Screenshot:
<img width="1082" height="765" alt="7" src="https://github.com/user-attachments/assets/c254a491-28be-4271-a4dc-694954b7372e" />

#

**Step 8:** Verifying Data Storage
After execution, the contents of users.txt and log.txt were inspected to confirm that passwords were encrypted and all attempts were logged with timestamps.

Screenshot:
<img width="1082" height="767" alt="6" src="https://github.com/user-attachments/assets/cb008b3a-1542-48ae-a859-779f883f5429" />
##


**Important Notes from the Lab**

- **Salted Hashing:** By using openssl rand, every user gets a unique salt. Even if two users have the same password, their hashes in users.txt will look different.
- **Input Masking:** The read -s flag was used to ensure passwords are not displayed on the screen while the user types.
- **Validation:** The script uses grep -q to silently check for existing users, allowing for a cleaner UI experience during errors.

**Defensive Analysis**

This lab demonstrates the Defense in Depth principle. Even if an attacker gains access to users.txt, they cannot immediately see user passwords because they are hashed. The use of a salt significantly increases the computational cost of cracking these hashes. Additionally, the logging system in log.txt provides an audit trail for monitoring failed login attempts, which is crucial for detecting brute-force attacks.

**Mitigation**

- Implement password complexity requirements (length, special characters).
- Add a "Lockout" mechanism after multiple failed login attempts to prevent automated brute-force attacks.
- Use a more secure hashing algorithm like Argon2 or bcrypt if available, as SHA-256 is fast and susceptible to GPU-accelerated cracking.

**Conclusion**

Building an authentication system from scratch in Bash highlights the critical steps of identity management. From validating user existence to securely transforming sensitive credentials into non-reversible hashes, the lab reinforces that security is a multi-layered process involving both logic and robust cryptographic tools.
