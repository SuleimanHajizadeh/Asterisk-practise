# Asterisk-practise

![Asterisk Logo](https://upload.wikimedia.org/wikipedia/commons/thumb/2/20/Asterisk_logo.svg/1200px-Asterisk_logo.svg.png)

**A hands-on GitHub repository for learning and experimenting with Asterisk, an open-source VoIP and PBX platform.**

This repository provides practical examples, configuration files, and scripts to help developers, students, and IT enthusiasts explore telephony protocols, SIP/IAX endpoints, call routing, and PBX functionalities.

---

## Table of Contents

* [About](#about)
* [Features](#features)
* [Installation](#installation)
* [Usage](#usage)
* [Repository Structure](#repository-structure)
* [Examples](#examples)
* [Learning Outcomes](#learning-outcomes)
* [Contributing](#contributing)
* [License](#license)
* [Contact](#contact)

---

## About

Asterisk is a widely-used open-source PBX system that allows you to build VoIP systems, manage calls, implement IVRs, and much more. This repository is designed as a **practice environment** where you can safely experiment with:

* SIP/IAX endpoints
* Call routing and dialplans
* Voicemail and call recording
* Basic automation and IVR scenarios

This project is ideal for learning practical telephony without the need for expensive proprietary hardware.

---

## Features

* Ready-to-use **Asterisk configuration files**
* Basic **scripts** for testing SIP registrations and call flows
* Example **dialplans** for practice
* Step-by-step instructions for running a **local Asterisk server**
* Safe environment for **hands-on learning**

---

## Installation

### Prerequisites

* Linux or macOS system
* Asterisk installed (>= 23.x recommended)
* Git

### Steps

1. Clone the repository:

git clone [https://github.com/SuleimanHajizadeh/Asterisk-practise.git](https://github.com/SuleimanHajizadeh/Asterisk-practise.git)
cd Asterisk-practise

2. Copy configuration files to your Asterisk directory:

sudo cp -r configs/* /etc/asterisk/

3. Reload Asterisk to apply the new configuration:

sudo asterisk -rx "core reload"

4. Start experimenting with endpoints, dialplans, and SIP registrations.

---

## Usage

### Start Asterisk CLI

sudo asterisk -rvvv

### Check Endpoints

pjsip show endpoints

### Make a Test Call

* Register two SIP endpoints
* Dial from one endpoint to another
* Observe call logs in the CLI

---
```
## Repository Structure

Asterisk-practise/
├── configs/          # Asterisk configuration files
│   ├── pjsip.conf
│   ├── extensions.conf
│   ├── voicemail.conf
├── scripts/          # Utility scripts for testing calls
│   ├── test_call.sh
│   ├── sip_register.sh
├── README.md
└── LICENSE
```
```
Asterisk-practise Dialplan / Call Flow Diagram
                        ┌─────────────┐
                        │  Caller     │
                        └─────┬───────┘
                              │
                              │ Dial
                              ▼
                        ┌─────────────┐
                        │  Asterisk   │
                        │  PBX Core   │
                        └─────┬───────┘
                              │
          ┌───────────────────┼───────────────────┐
          │                   │                   │
          ▼                   ▼                   ▼
   ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
   │ Extension   │     │ IVR Menu    │     │ Voicemail   │
   │ 1001/1002   │     │ 1->Sales    │     │ 1003        │
   │             │     │ 2->Support  │     │             │
   │             │     │ 3->Voicemail│     │             │
   └─────┬───────┘     └─────┬───────┘     └─────┬───────┘
         │                   │                   │
         │ Call Connected     │ Route to Dept     │ Store Message
         ▼                   ▼                   ▼
   ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
   │  Phone at   │     │  Sales/     │     │  Voicemail  │
   │ Destination │     │  Support    │     │  Inbox      │
   └─────────────┘     └─────────────┘     └─────────────┘

```
---

## Examples

### 1. Simple Call Flow

Extension 1001 --> Dial 1002 --> Call connected

### 2. Basic IVR

Welcome Menu:
1 -> Sales
2 -> Support
3 -> Voicemail

![IVR Example](https://docs.asterisk.org/Fundamentals/Asterisk-Architecture/AsteriskArchitecture.png)

---

## Learning Outcomes

By exploring this repository, you will learn:

* How to configure Asterisk endpoints (SIP/IAX)
* How to manage call routing and dialplans
* How to implement basic IVR and voicemail
* How to experiment with VoIP calls in a safe environment

This hands-on approach bridges the gap between theoretical knowledge and practical telephony implementation.

---

## Contributing

Contributions are welcome! Feel free to:

* Submit **pull requests**
* Report **issues** or bugs
* Suggest **new examples or scripts**

Please follow standard GitHub contribution guidelines.

---

## License

This repository is licensed under the MIT License. See the LICENSE file for details.

---

## Contact

For questions or feedback, feel free to contact me through GitHub: [SuleimanHajizadeh](https://github.com/SuleimanHajizadeh)

---

**Check out the repo:** [https://github.com/SuleimanHajizadeh/Asterisk-practise](https://github.com/SuleimanHajizadeh/Asterisk-practise)
