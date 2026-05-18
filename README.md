# NBLock-Black-Ransomware-Builder
Builder for NBLock Black Ransomware
## Warning
!THIS IS NOT A CRACK OR A LEAK!
## README
By analysing LockBit 3.0 Black (LB3) Ransomware
i made a copycat of it in C#,
i know the code is pretty gross and yes i did get help from AI (pls dont bully me over it).
the Binaries included in The zip file are fully C# & Easily Decompilable
## Encrypted Files [File icon Set true]
![NBLock](files.jpg)
## Builder Files
![Builderfiles](builder.jpg)
Same As LB3's Builder files.
## Decryptor UI 
![decryptor](dec.jpg)
i spent a LOT of time on copy'ing LB3's Decryptor UI.
## Nerdy Stuff
 [ THIS PART IS AI GENERATED BECAUSE IM LAZY, BASICLY ITS FAST,UNIQUE AND SECURE (AES 256 CBC, RSA-2048) ]
​🔑 Cryptographic Architecture
​Hybrid Encryption Scheme: The payload utilizes a high-performance hybrid encryption model combining symmetric and asymmetric cryptography.
​Symmetric Layer: Files are encrypted using AES-256 (CipherMode.CBC). A unique key and Initialization Vector (IV) are generated dynamically for each execution session.
​Asymmetric Layer: The dynamic AES key is wrapped/encrypted using a hardcoded RSA-2048 public key ([[PKEY]]). The encrypted key blob and IV are saved locally into a hidden system file (key.bin) on the desktop to facilitate potential recovery via the corresponding private key.
​⚙️ Encryption Engine & Optimization
​Inteligent File Chunking (Intermittent Encryption): To optimize performance and reduce I/O overhead on large files, the code splits its behavior into two modes based on file size (threshold: 100 MB):
​Full Encryption (mode 0x00): Files smaller than 100 MB are fully encrypted using PKCS7 padding.
​Intermittent/Streamed Encryption (mode 0x01): Files larger than 100 MB are encrypted in fixed steps using NoPadding to maximize speed. The step interval varies based on file size tiers (25 MB, 50 MB, or 100 MB steps).
​High-Throughput Multi-Threading: Scalability is managed via Parallel.ForEach. The payload queries the host cpu core count and scales the maximum degree of parallelism dynamically ({\text{Cores}} \times 1.5), bound to a minimum floor of 4 concurrent worker threads.
​Metadata Structuring: Every processed file is stamped with a custom 5-byte footer array (0x4E 0x42 0x4C 0x21 + mode_byte) translating to the ASCII marker NBL! followed by the encryption mode indicator.
​🛑 Anti-Recovery & System Modification
​Shadow Copy & Backup Deletion (DSC): Invokes system tools hiddenly (runas verb) to destroy system recovery points:
​vssadmin.exe delete shadows /all /quiet (Deletes Volume Shadow Copies).
​reagentc.exe /disable (Disables Windows Recovery Environment).
​bcdedit manipulation to ignore boot failures, disable automated recovery, and remove safe mode configurations.
​wbadmin delete catalog -quiet (Discards Windows Backup history).
​Disables the Windows Error Reporting Service (WerSvc).
​Event Log Cleansing (ZxaUus): Explicitly clears critical Windows Event Log channels (Application, System, Security, Setup) to erase execution footprints.
​Network & Security Invalidation (XqxacZi): Modifies the local Windows hosts file (drivers\etc\hosts) to redirect major cybersecurity domains, antivirus update endpoints, and reporting portals to loopback (127.0.0.1), preventing updates, threat analysis submissions, or victim support access.
​🛡️ Evasion & Environment Awareness
​Whitelisting: To maintain system stability during execution, the traversal engine strictly skips directories containing strings like "Microsoft" or "Windows", as well as essential extensions such as .exe, .sys, and .dat.
​Network Discovery (Kbzha): Queries the Windows Registry (MountPoints2) to actively scan for and append remote network shares and mapped network drives into the targeting queue.
​File Overwriting (Wiping/Shredding) (destr): Implements a destructive 64KB buffer rewrite engine that fills files with randomized noise via a Pseudo-Random Number Generator (PRNG) prior to standard OS deletion, neutralizing basic data-recovery or forensic carving attempts.
​Custom File Association: Creates a unique file extension dynamically mapped to the first 5 characters of the victim's unique hardware identifier (MD5 hash of hardware variables).
​Registry Hijacking: Injects keys under Software\Classes to associate the newly generated extension with a custom icon resource (lock.ico) and issues global shell refresh notices via native API calls (SHChangeNotify & SystemParametersInfo).
​Desktop Persistence: Rewrites the user wallpaper configuration to force a custom background image (locked.png).
## Educational Purposes Only

This repository and its contents are intended solely for academic research, educational purposes, and authorized security analysis. 

### Terms of Use

* **Strictly Educational:** The source code, concepts, and methodologies demonstrated in this repository are designed to help developers and security researchers understand binary structure, metadata manipulation, and assembly patching mechanics.
* **No Unauthorized Deployment:** The use of any concepts or artifacts derived from this project against systems without explicit, prior written authorization from the system owner is strictly prohibited.
* **No Liability:** This software is provided "as-is" without any express or implied warranty. Under no circumstances shall the author or contributors be liable for any direct, indirect, incidental, special, exemplary, or consequential damages, or legal repercussions arising from the use or misuse of this repository.
* **User Responsibility:** By downloading, cloning, or interacting with this repository, you assume full responsibility for your actions and compliance with all applicable local, national, and international laws.
