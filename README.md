# NETWORKWALKS-BASHIR-B084E-WK3-PROJECT-PASSWORD-CRACKING
# 🔐 Task 3: Password & Hash Cracking with John the Ripper and NW Tools

**Project:** Offline and Browser-Based Password Cracking of Encrypted PDF Files  
**Author:** Bashir Abdullahi  
**Degree:** Business Information Technology  
**University:** The Cooperative University of Kenya  
**Environment:** Kali Linux (John the Ripper / Johnny GUI) + NetworkWalks Tools (NW Tools)  
**Purpose:** Password security auditing, hash cracking, and authorized security testing

---

## 📌 1. Project Overview

This project focuses on cracking password-protected PDF files using **two independent tools**:

- **John the Ripper (JtR)** — an offline password-cracking engine, run via the Johnny GUI.
- **NetworkWalks Tools (NW Tools)** — NetworkWalks' own browser-based password-cracking platform.

Each PDF's encryption metadata was converted into a crackable hash (`$pdf$...` format), and that same hash was then attacked separately by both JtR and NW Tools, each running its own wordlist attack against the same ~3,556-entry password list. Both tools independently recovered the same plaintext passwords, and each successful crack on NW Tools triggered a flag as proof of completion.

This builds directly on the virtual lab environment set up in Task 1, applying hands-on password-auditing skills within that controlled, authorized environment.

## 🎯 2. Project Objectives

The objectives of this task are to:

- Understand how encrypted PDFs store password-verification data.
- Extract a crackable hash from a password-protected PDF.
- Run a wordlist attack against that hash using John the Ripper.
- Run an independent wordlist attack against the same hash using NW Tools.
- Compare results from both tools to confirm the recovered passwords.
- Capture and record flags issued by NW Tools for each completed exercise.
- Document the full workflow, evidence, and lessons learned.

## 💻 3. Tools and Specifications

| Component | Configuration |
|---|---|
| Cracking engine 1 | John the Ripper (JtR), via Johnny GUI |
| Cracking engine 2 | NetworkWalks Tools (NW Tools) — `networkwalks.com/password-cracker/` |
| Hash extraction method | pdf2john-style browser extractor |
| Hash format | `$pdf$4*4*128*-1028*1*16*...` (PDF, revision 4, 128-bit key) |
| Attack type | Wordlist attack (run independently on each tool) |
| Wordlist size | 3,556 entries (common passwords, ordered by frequency) |
| Files tested | My Locked PDF1.pdf, PDF2.pdf, PDF3.pdf |

*Note: Record the exact wordlist name/source and JtR version before submitting the final report.*

## 🏗️ 4. Workflow

```text
         Encrypted PDF (PDF1 / PDF2 / PDF3)
                     |
                     v
        Hash Extraction (pdf2john-style tool)
                     |
                     v
         $pdf$4*4*128*... hash generated
                     |
         +-----------+-----------+
         |                       |
         v                       v
  John the Ripper          NetworkWalks Tools
   (Johnny GUI)                (NW Tools)
  Wordlist attack           Wordlist attack
         |                       |
         v                       v
   [+] MATCH found         [+] MATCH found
         |                       |
         +-----------+-----------+
                     |
                     v
        Passwords compared — results match
                     |
                     v
          🚩 Flag captured via NW Tools
```

## ⚙️ 5. Implementation Procedure

### Step 1: Extract the Hash from Each PDF

Each encrypted PDF was uploaded to a browser-based extraction tool, which parsed its encryption dictionary (Revision 4, 128-bit key, V4) and returned a `$pdf$...` hash suitable for both JtR and NW Tools.

**Screenshot evidence:** Extracted hash output for PDF1, PDF2, and PDF3.

### Step 2: Crack with John the Ripper

The extracted hash was saved to a `.txt` file (`hash1.txt`, `hash2.txt`) and loaded into Johnny, the GUI front-end for John the Ripper, which ran a wordlist attack against it.

```bash
john --wordlist=rockyou.txt --format=pdf hash1.txt
```

JtR returned a `[+] MATCH` result once the correct password was found for each file.

### Step 3: Crack with NW Tools (Independently)

The same hash was separately pasted into **NW Tools** at `networkwalks.com/password-cracker/`, which ran its own in-browser wordlist

---

**Project Status:** All three provided PDFs successfully cracked and verified. Wordlist source and tool version documentation pending before final submission.

# networkwalks-B084-week3-password-cracking-jtr
password cracking using John the Ripper
I've completed my week three work
