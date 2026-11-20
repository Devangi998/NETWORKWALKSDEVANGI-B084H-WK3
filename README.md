# NETWORKWALKSDEVANGI-B084H-WK3

Hands-on Cybersecurity & Ethical Hacking Week 3 lab projects demonstrating PDF hash extraction and password cracking using John the Ripper (Johnny GUI) and Networkwalks browser-based tools.

## Table of Contents
- [Overview & Concepts](#overview--concepts)
- [Module 1: Password Cracking with John the Ripper & Johnny GUI](#module-1-password-cracking-with-john-the-ripper--johnny-gui)
- [Module 2: Browser-Based Dictionary Attack with Networkwalks Tools](#module-2-browser-based-dictionary-attack-with-networkwalks-tools)
- [Key Takeaways & Security Mitigation](#key-takeaways--security-mitigation)

---

## Overview & Concepts
* **Encryption vs. Hashing:** Encryption is a two-way process that scrambles data using a key and can be decrypted with the proper key. Hashing is a one-way cryptographic function that converts plain text into a fixed-length message digest.
* **Attack Workflow:** Instead of attempting password guesses directly inside a PDF reader, security auditors extract the underlying `$pdf$` password hash and execute offline or dictionary-based attacks against the hash.

---

## Module 1: Password Cracking with John the Ripper & Johnny GUI

### Objective
Extract the cryptographic hash from `My Locked PDF1.pdf` and recover the document open password on Windows using John the Ripper (JTR) and Johnny GUI.

### Tools Used
* **OnlineHashCrack PDF Hash Extractor (`pdf2john`)** – Extracts `$pdf$` hashes compatible with JTR and Hashcat.
* **John the Ripper (1.9.0-jumbo-1 Windows x64)** – Core password cracking engine.
* **Johnny GUI (v2.2)** – Graphical front-end for managing JTR cracking sessions.

### Execution & Results
1. **Hash Extraction:** Uploaded `My Locked PDF1.pdf` to the PDF Hash Extractor and retrieved the 128-bit R4/V4 `$pdf$` hash string, saving it locally as a plain-text file.
   ![JTR Hash Extraction](<img width="1920" height="1020" alt="Screenshot 2026-11-20 201322" src="https://github.com/user-attachments/assets/24e74f4e-ed79-44d4-9c3f-9df42c4c8ad0" />
)
2. **Cracking with Johnny:** Configured Johnny to point to `john.exe`, loaded the saved hash file in `PASSWD` format, and started a new attack.
3. **Recovered Password:** Johnny successfully cracked the hash (`1/1 cracked`), revealing the plaintext password **`good-luck`**.
   ![Johnny Cracked Password](<img width="873" height="692" alt="Screenshot 2026-11-20 202102" src="https://github.com/user-attachments/assets/882c7b25-3574-44be-9779-9176b8c97482" />
)

---

## Module 2: Browser-Based Dictionary Attack with Networkwalks Tools

### Objective
Extract the cryptographic hash and perform a client-side dictionary attack against `My Locked PDF1 (for NW Tools Lab WK3-PM2).pdf` using Networkwalks web utilities.

### Tools Used
* **Networkwalks Hash Calculator** – Locally parses the encrypted PDF structure in the browser to generate a crackable `$pdf$` hash.
* **Networkwalks Password Cracker** – Performs a dictionary attack against the extracted `$pdf$` hash using a built-in wordlist.

### Execution & Results
1. **Hash Extraction:** Loaded `My Locked PDF1 (for NW Tools Lab WK3-PM2).pdf` into the Networkwalks Hash Calculator and copied the extracted 128-bit R4/V4 `$pdf$` hash.
   ![Networkwalks Hash Calculator](<img width="1920" height="1020" alt="Screenshot 2026-11-20 201208" src="https://github.com/user-attachments/assets/7cbb84a8-7357-42b7-89d5-d334c6f2dfba" />
)
2. **Dictionary Attack:** Pasted the `$pdf$` hash into the Networkwalks Password Cracker and initiated the dictionary attack.
3. **Recovered Password:** The tool matched the hash against the built-in wordlist and recovered the password **`password1`**.
   ![Networkwalks Password Cracker](<img width="1920" height="1020" alt="Screenshot 2026-11-20 201224" src="https://github.com/user-attachments/assets/77a69f8d-d295-4193-b8bc-21d50c16ac6d" />
)

---

## Key Takeaways & Security Mitigation
* **Vulnerability of Weak Passwords:** Common dictionary words and simple predictable combinations (`good-luck`, `password1`) can be recovered almost instantly once a document's hash is extracted.
* **Defense Recommendations:**
  * Use strong, high-entropy passwords (12+ characters combining uppercase, lowercase, numbers, and special symbols).
  * Avoid using dictionary words, common phrases, or predictable numeric suffixes.
  * Protect sensitive PDFs with modern AES-256 encryption standards.
