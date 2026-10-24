# CSFLabs

This repository contains the lab assignments for the "Ciber-Segurança Forense" (Forensics Cyber-Security) course @IST Instituto Superior Técnico (MEIC 2026/2027, 1st semester). The labs follow a single fictional investigation, **Operation DeepFISH**, across three stages: from a phishing website impersonating Técnico's login page, to the seized machines of its operator, to the network traffic of the organisation behind the hidden files.

## Repository Structure

- [Lab 1](/lab1/)
- [Lab 2](/lab2/)
- [Lab 3](/lab3/)

---

## Lab 1 - Operation DeepFISH, Stage I

This lab focused on investigating a phishing website cloning IST's CAS single sign-on page, and on recovering the secrets concealed in the files left behind by its operator.

- Reconstructed the site's **exposed `.git` directory** and walked its commit history to recover deleted files and date the build and deployment of the phishing kit.
- Recovered **seven concealed artifacts**, each hidden with a different technique:
  - a PNG with a **spoofed magic number**;
  - **Jsteg-style LSB** data in a JPEG's DCT coefficients, extracted with `jpegio`;
  - a payload encoded in the **frame durations** of an animated WebP;
  - text rasterised into the **stereo phase-difference spectrogram** of a WAV file;
  - an **ICO/HTML/PDF/MP4 polyglot**, repaired with `qpdf`;
  - **LSB pixel data** on a fixed grid across the frames of a reassembled video, found with a brute-force decoder;
  - a **password-protected ZIP**, cracked with John the Ripper and a wordlist generated from subtitle dialogue.
- Interpreted the recovered material as a whole and formulated a hypothesis about a larger scheme beyond the phishing campaign.

Files: [Report](lab1/lab1-report.pdf) · [Guidelines](lab1/csf2627-lab-assignment-1.pdf)

## Lab 2 - Operation DeepFISH, Stage II

This lab continued from Lab 1 with the analysis of the suspect's seized devices: a Windows laptop (memory and disk images) and a Linux workstation.

- Used **Volatility 3** on the RAM capture to identify the acquisition activity and recover the **BitLocker FVEK**, then decrypted the protected volume read-only with **dislocker**.
- Analysed NTFS and ext4 volumes with **The Sleuth Kit** (`mmls`, `fls`, `istat`, `icat`), extracting registry hives, browser history, PowerShell history and a **Discord cache**.
- Parsed the **SAM / SYSTEM / SECURITY / SOFTWARE** hives with `regripper` and `pypykatz` to recover account and autologon secrets.
- Derived the passphrase of a protected archive from clues spread across the evidence, and matched its contents byte-for-byte to the Stage I artifacts.
- Reconstructed how the hidden files reached the phishing repository (an auto-commit script and a server-side merge) and documented **anti-forensic activity** (secure deletion, journal wipe, server-side cleanup).
- Built a consolidated **timeline** of events across both machines.

Files: [Report](lab2/lab2-report.pdf) · [Guidelines](lab2/csf2627-lab-assignment-2.pdf)

## Lab 3 - Operation DeepFISH, Stage III

This lab moved the investigation to the network, analysing packet captures from the internal network of the organisation linked to the hidden files.

- Decrypted **TLS traffic** in Wireshark/`tshark` using key log files, including services running on non-standard ports.
- Mapped hosts and accounts from DNS, HTTP and login traffic, and reconstructed **chat, webmail and intranet** activity.
- Recovered files transferred in the clear over **TFTP** and over HTTP, and matched them by hash to the artifacts from the previous stages.
- Analysed the requests and responses of an **LLM-based evaluation service** to establish how a compliance check could be bypassed.
- Separated observations, inferences and hypotheses when attributing actions to accounts and hosts.

Files: [Report](lab3/lab3-report.pdf) · [Guidelines](lab3/csf2627-lab-assignment-3.pdf)

## Team

Group 53

- João Viegas (ist1109685)
- Rafael Gomes (ist1110285)
- Ilès Ouyahia (ist1121299)