# NETWORKWALKS-BASHIR-B084E-WK3-PROJECT-PASSWORD-CRACKING
# 🔐 Task 3: Password & Hash Cracking with John the Ripper

**Project:** Offline Password Cracking of Encrypted PDF Files  
**Author:** Bashir Abdullahi  
**Degree:** Business Information Technology  
**University:** The Cooperative University of Kenya  
**Environment:** Kali Linux (John the Ripper / Johnny GUI) + browser-based hash extraction tools  
**Purpose:** Password security auditing, hash cracking, and authorized security testing

---

## 📌 1. Project Overview

This project focuses on offline password cracking using **John the Ripper (JtR)** against password-protected PDF files provided for the NetworkWalks Cybersecurity training program.

Each PDF's encryption metadata was converted into a crackable hash (`$pdf$...` format), loaded into John the Ripper via the Johnny GUI, and attacked using a wordlist of common passwords. Results were cross-verified against NetworkWalks' own browser-based password-cracking tool.

This builds directly on the virtual lab environment set up in Task 1, applying hands-on password-auditing skills within that controlled, authorized environment.

## 🎯 2. Project Objectives

The objectives of this task are to:

- Understand how encrypted PDFs store password-verification data.
- Extract a crackable hash from a password-protected PDF.
- Load a hash into John the Ripper and run a wordlist attack.
- Successfully recover plaintext passwords from encrypted PDFs.
- Verify cracked results using an independent tool.
- Capture and record flags issued for each completed exercise.
- Document the full workflow, evidence, and lessons learned.

## 💻 3. Tools and Specifications

| Component | Configuration |
|---|---|
| Cracking engine | John the Ripper (JtR) |
| GUI front-end | Johnny |
| Hash extraction method | pdf2john-style browser extractor |
| Hash format | `$pdf$4*4*128*-1028*1*16*...` (PDF, revision 4, 128-bit key) |
| Attack type | Wordlist attack |
| Wordlist size | 3,556 entries (common passwords, ordered by frequency) |
| Verification tool | NetworkWalks online password-cracker |
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
                     v
         Loaded into John the Ripper (Johnny GUI)
                     |
                     v
            Wordlist Attack Launched
                     |
                     v
          [+] MATCH — password recovered
                     |
                     v
       Verified against NetworkWalks cracker tool
                     |
                     v
              🚩 Flag captured
```

## ⚙️ 5. Implementation Procedure

### Step 1: Extract the Hash from Each PDF

Each encrypted PDF was uploaded to a browser-based extraction tool, which parsed its encryption dictionary (Revision 4, 128-bit key, V4) and returned a `$pdf$...` hash suitable for JtR or hashcat.

**Screenshot evidence:** Extracted hash output for PDF1, PDF2, and PDF3.

### Step 2: Save and Load the Hash

The extracted hash was saved to a `.txt` file (`hash1.txt`, `hash2.txt`) and opened in Johnny, the GUI front-end for John the Ripper.

```bash
john --format=pdf hash1.txt
```

### Step 3: Run the Wordlist Attack

A wordlist attack was launched from Johnny against each hash, testing candidate passwords sequentially (most common passwords first).

```bash
john --wordlist=rockyou.txt --format=pdf hash1.txt
```

### Step 4: Record the Match

JtR returned a `[+] MATCH` result once the correct password was found for each file.

### Step 5: Verify Independently

Each recovered password was cross-checked using NetworkWalks' own browser-based password-cracking tool at `networkwalks.com/password-cracker/`, which ran the same wordlist attack live and confirmed the match.

### Step 6: Capture the Flag

Each successful crack triggered a flag from the NetworkWalks platform, recorded below as evidence of task completion.

## 📊 6. Results

| PDF File            | Recovered Password |
|----------------------|----------------------|
| My Locked PDF1.pdf    | `good-luck`           |
| My Locked PDF2.pdf    | `password1`           |
| My Locked PDF3.pdf    | `1qaz2wsx`            |

## 🚩 7. Flags Captured

- `nw{cybersecurity_flag_captured_2608}`
- `nw{networkwalks_persistence_jtr_270521}`
- `nw{networkwalks_flag_260821_1}`

*(Consider redacting these before publishing publicly if other students share the same challenge set.)*

## 🔎 8. Verification Checklist

- [x] Hash successfully extracted from PDF1.
- [x] Hash successfully extracted from PDF2.
- [x] Hash successfully extracted from PDF3.
- [x] Hash loaded into John the Ripper / Johnny.
- [x] Wordlist attack completed for each file.
- [x] Password recovered and confirmed for each PDF.
- [x] Results cross-verified with NetworkWalks tool.
- [x] Flags captured and recorded.
- [ ] Wordlist source and JtR version documented.
- [ ] Screenshots organized and linked in repository.

## 🐞 9. Troubleshooting and Lessons Learned

### Problem 1: Slow Cracking Speed

The wordlist attack processed only a small number of passwords per second (as low as ~2–16 pw/s in testing), which would be impractical against a large or complex wordlist.

**Lesson:** Cracking speed depends heavily on hash complexity (PDF key derivation is intentionally slow) and hardware. Wordlist ordering (common passwords first) matters more than raw speed for realistic, weak passwords.

### Problem 2: Incorrect Hash Format

An improperly formatted or incomplete hash string causes John the Ripper to fail to recognize the format.

**Solution:** Always copy the full `$pdf$...` string exactly as extracted, without line breaks or missing characters, before saving it to a file.

### Problem 3: Confirming a True Match

A visual "MATCH" in a GUI or tool output should still be verified against the actual file, since copy errors can lead to false confidence.

**Solution:** Open the original PDF with the recovered password to confirm it actually unlocks the file before recording it as a final result.

## 🧠 10. What I Learned

1. **PDF encryption internals:** How encrypted PDFs store a verifiable hash separate from the reader's password prompt.
2. **Offline vs online cracking:** The difference between attacking a hash offline versus guessing through a login interface.
3. **Wordlist attacks:** How wordlist size, ordering, and content affect cracking success and speed.
4. **Tool proficiency:** Hands-on use of John the Ripper, both via command line and the Johnny GUI.
5. **Verification discipline:** The importance of independently confirming cracked results rather than trusting a single tool's output.
6. **Documentation:** Recording hashes, commands, and results clearly enough for the process to be reproduced or audited.

## 🔐 11. Security and Ethical Use

This exercise was conducted strictly within the NetworkWalks training environment, using files and challenges provided for educational purposes.

- Only PDFs provided for this authorized exercise were tested.
- No third-party or externally sourced files were cracked.
- Recovered passwords and hashes are used solely for learning password-security concepts.
- These techniques are intended to build defensive awareness (e.g., why weak passwords like `password1` are easily cracked), not for unauthorized access.
- Flags and hashes should be handled responsibly and not used to bypass real-world protections without authorization.

**Important:** Password cracking against any system or file without explicit authorization is illegal. This project only applies these skills to files and tools provided specifically for this authorized training exercise.

## 🚀 12. Future Improvements

- Test cracking performance using rule-based attacks (e.g., JtR's mangling rules) in addition to plain wordlists.
- Benchmark cracking speed across different hash types (PDF, ZIP, MD5, NTLM).
- Practice cracking hashes extracted from other file types (e.g., `zip2john`, `office2john`).
- Explore GPU-accelerated cracking with hashcat for comparison.
- Document password-strength recommendations based on observed cracking speeds.

## 📚 13. Tools and References

- [John the Ripper](https://www.openwall.com/john/)
- [Johnny (JtR GUI)](https://openwall.info/wiki/john/johnny)
- [NetworkWalks Password Cracker Tool](https://networkwalks.com/password-cracker/)
- [Online HashCrack – PDF Hash Extraction](https://www.onlinehashcrack.com/)

## 👤 14. Project Information

| Field | Details |
|---|---|
| Student | Bashir Abdullahi |
| University | The Cooperative University of Kenya |
| Task | Task 3 — Password & Hash Cracking with John the Ripper |
| Project category | Cybersecurity / Password Auditing / Digital Forensics |
| Tools used | John the Ripper, Johnny, pdf2john-style extractor |
| Files tested | 3 encrypted PDFs |
| Passwords recovered | 3 / 3 |

---

**Project Status:** All three provided PDFs successfully cracked and verified. Wordlist source and tool version documentation pending before final submission.

# networkwalks-B084-week3-password-cracking-jtr
password cracking using John the Ripper
I've completed my week three work
