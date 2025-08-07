📌 Overview
This lab simulates a scenario where all files in your Linux home directory have been encrypted.
Your mission: locate hidden files, break a Caesar cipher, and decrypt AES-256-CBC–encrypted data to recover a hidden message.

🗂 Scenario
A malicious actor has encrypted sensitive files in /home/analyst.
They’ve hidden clues in a subdirectory, protected with a Caesar cipher.
You must:

Explore the directory.

Find the hidden file.

Decrypt it using Linux commands.

Use the revealed password to unlock your encrypted data.

🛠 Tools & Commands Used
ls – List directory contents

cat – Display file contents

cd – Change directory

tr – Translate/replace characters (used for Caesar cipher decryption)

openssl – Perform AES-256-CBC decryption

📖 Step-by-Step Instructions
1. Explore Home Directory
bash
Copy
Edit
ls
cat README.txt
Files found:

pgsql
Copy
Edit
Q1.encrypted  README.txt  caesar/
2. Find the Hidden File
bash
Copy
Edit
cd caesar
ls -a
cat .leftShift3
The file .leftShift3 contains text encrypted with a Caesar cipher (shift 3 to the left).

3. Decrypt the Caesar Cipher
bash
Copy
Edit
cat .leftShift3 | tr "d-za-cD-ZA-C" "a-zA-Z"
This reveals the openssl command to use in the next step.

4. Return to Home Directory
bash
Copy
Edit
cd ~
5. Decrypt the AES-256-CBC File
bash
Copy
Edit
openssl aes-256-cbc -pbkdf2 -a -d -in Q1.encrypted -out Q1.recovered -k ettubrute
AES-256-CBC: Strong symmetric cipher

-pbkdf2: Adds secure key derivation

-a: Base64 encoding

-d: Decrypt mode

-in / -out: Input & output files

-k: Password revealed from Caesar cipher

6. Read the Recovered Message
bash
Copy
Edit
cat Q1.recovered
🎉 You’ve successfully decrypted the hidden message!

📂 Directory Structure After Decryption
pgsql
Copy
Edit
/home/analyst
├── Q1.encrypted
├── Q1.recovered
├── README.txt
└── caesar/
    └── .leftShift3
💡 Key Takeaways
Caesar cipher is a basic encryption method vulnerable to brute force and known shifts.

AES-256-CBC is a strong encryption standard, but still depends on protecting the key.

Linux command-line tools like tr and openssl can be powerful for both encryption and decryption tasks.

Always check for hidden files using ls -a.
