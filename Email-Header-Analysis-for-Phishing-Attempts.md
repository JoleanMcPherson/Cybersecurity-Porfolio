# Email Header Analysis for Phishing Attempts – KANO Project

## Overview

This project automates the analysis of email headers to detect phishing attempts by extracting key metadata and identifying suspicious patterns. Using Python scripting, it helps security teams quickly flag malicious emails and improve organizational email security protocols.

---

## Features

- Parses raw email headers to extract:
  - Sender IP addresses  
  - SPF (Sender Policy Framework) results  
  - DKIM (DomainKeys Identified Mail) signatures  
  - DMARC (Domain-based Message Authentication, Reporting & Conformance) status  
  - Email routing information through Received headers  
- Automates anomaly detection such as:
  - Spoofed or mismatched sender domains  
  - Failed or missing SPF and DKIM validation  
  - Unusual routing paths or IP addresses  
- Generates alerts or warnings for suspicious emails  
- Provides logging and report summaries for incident tracking  
- Easy to extend with additional email security checks  

---

## Why It Matters

Phishing is one of the top attack vectors targeting organizations. Analyzing email headers is a critical skill for Security Operations Centers (SOCs) to identify and stop phishing attempts before they cause damage.

By automating header analysis, this project demonstrates practical SOC-level threat detection capabilities using open-source tools and scripting.

---

## Getting Started

### Prerequisites

- Python 3.7 or higher  
- Basic Python knowledge  
- Raw email headers to analyze (usually extracted from email clients or logs)  

### Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/yourusername/email-header-analysis.git
    cd email-header-analysis
    ```

2. (Optional) Create and activate a virtual environment:

    ```bash
    python -m venv venv
    source venv/bin/activate  # Linux/macOS
    venv\Scripts\activate     # Windows
    ```

3. Install dependencies (if any):

    This basic version uses only Python standard libraries and requires no external packages.

---

### Usage

1. Prepare a text file with a raw email header you want to analyze, e.g., `sample_header.txt`.

2. Run the Python script to analyze it:

    ```bash
    python analyze_email_header.py sample_header.txt
    ```

3. The script will output key metadata extracted from the header, including sender IPs, SPF results, DKIM signatures, and alerts if any anomalies are detected.

---

## Example Code

Here is the main script (`analyze_email_header.py`):

```python
import sys
import email
import re

def parse_email_header(raw_header):
    msg = email.message_from_string(raw_header)
    received_headers = msg.get_all('Received', [])
    spf_result = msg.get('Received-SPF', 'None')
    dkim_signature = msg.get('DKIM-Signature', 'None')

    # Extract sender IPs from Received headers
    sender_ips = []
    for header in received_headers:
        ips = re.findall(r'\\b(?:[0-9]{1,3}\\.){3}[0-9]{1,3}\\b', header)
        sender_ips.extend(ips)

    # Check SPF result for anomalies
    if 'pass' not in spf_result.lower():
        print("⚠️ Warning: SPF check failed or missing")

    return {
        'sender_ips': sender_ips,
        'spf_result': spf_result,
        'dkim_signature': dkim_signature
    }

def main():
    if len(sys.argv) != 2:
        print(f"Usage: {sys.argv[0]} <email_header_file>")
        sys.exit(1)

    filename = sys.argv[1]

    with open(filename, 'r') as f:
        raw_header = f.read()

    result = parse_email_header(raw_header)
    print("=== Email Header Analysis Result ===")
    print(f"Sender IPs found: {result['sender_ips']}")
    print(f"SPF Result: {result['spf_result']}")
    print(f"DKIM Signature Present: {'Yes' if result['dkim_signature'] != 'None' else 'No'}")

if __name__ == "__main__":
    main()
