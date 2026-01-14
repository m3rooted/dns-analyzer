# DNS Analyzer

A simulation model of DNS data encapsulation in a local network and an analyzer program for suspicious DNS traffic.

> **Warning**: This project is not suitable for real-world misuse.

## Project metadata

- **Description**: DNS data encapsulation simulation + DNS traffic analyzer (lab/local network)
- **Author**: Nguyen Duong Quang
- **Date**: 2025-08-14

## Features

- Server with support for multiple client connections over both TCP and UDP
- Three sending modes for client: text messages, random bytes or text file.
- AES data encryption option for client.
- Sniffer can save its results to a `.pcap` file for further analysis.

## Supported DNS RR types

- **A**, **AAAA** for encoding in IPv4 or IPv6 addesses
- **CNAME**, **MX**, **NS** for encoding in domain names
- **NULL**, **TXT** for raw data

> **Note**: According to Wikipedia, NULL RR is considered obsolete by RFC 1035!

## Installing dependencies

Make sure that Python `3.10+` is installed.
Use pip (preferably in a virtual environment, e.g. `venv`) to install dependencies from requirements.txt

```bash
pip install -r requirements.txt
```

## Usage

Client script:

```text
usage: client.py [-h] -c CONN [-t TIMEOUT] [-T] [-F FILE] [-R] [-d DOMAIN]
                 [-q QTYPE] [-s SCRAMBLE [SCRAMBLE ...]] [-a AES_KEY] [-S]

DNS Analyzer: client script

optional arguments:
  -h, --help            show this help message and exit
  -c CONN, --connect CONN
                        Establishes a connection to the server at the
                        specified address:port
  -t TIMEOUT, --timeout TIMEOUT
                        Specifies the timeout for server UDP response
  -T, --send-text       Sends a text string to the server
  -F FILE, --send-file FILE
                        Sends the file to the server. The file path is
                        required.
  -R, --send-random     Sends a random byte array to the server
  -d DOMAIN, --domain DOMAIN
                        Specifies the domain name
  -q QTYPE, --qtype QTYPE
                        Specifies the type of record for a DNS question
  -s SCRAMBLE [SCRAMBLE ...], --scramble SCRAMBLE [SCRAMBLE ...]
                        Scrambles outgoing traffic passing through the DNS
                        channel. You need to specify an offset, e.g. (3, 11)
  -a AES_KEY, --aes AES_KEY
                        Encrypts with AES outgoing traffic passing through the
                        DNS channel. You need to specify an encryption key
  -S, --tcp             Forcibly sends DNS messages over TCP connection
```

Server script:

```text
usage: server.py [-h] [-p PORT] [-d] [-t TIMEOUT]

DNS Analyzer: server script

optional arguments:
  -h, --help            show this help message and exit
  -p PORT, --port PORT  Specifies the port that the server will listen to
  -d, --debug           Displays debugging information
  -t TIMEOUT, --timeout TIMEOUT
                        Specifies the timeout for incoming connections
```

Sniffer script:

```text
usage: sniffer.py [-h] (-g IP | -i PCAP) [-d] -f PATH [-m MINUTES]

DNS Analyzer: sniffer script for detecting suspicious traffic

optional arguments:
  -h, --help            show this help message and exit
  -g IP, --gateway IP   Specifies the gateway address (live capture)
  -i PCAP, --pcap-in PCAP
                        Analyze an existing .pcap file (offline mode)
  -d, --debug           Displays debugging information
  -f PATH, --filename PATH
                        Specifies path for .pcap file
  -m MINUTES, --minutes MINUTES
                        Size of the time window in minutes for traffic
                        analysis
```
