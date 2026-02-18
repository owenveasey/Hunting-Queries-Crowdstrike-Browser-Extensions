# Malicious Browser Extension Hunt 

## Overview
This repository contains a specialized **CrowdStrike Advanced Event Search (AES)** query designed to detect file-level artifacts associated with a known campaign of malicious browser extensions. 

These extensions, often disguised as "Emoji Keyboards," "Weather Forecasts," or "Productivity Tools," have been identified as high-risk for credential theft, browser hijacking, and unauthorized data exfiltration.

## Threat Intel Context
This hunt targets 18+ specific Extension IDs (IOCs) that have been flagged by the security community (including researchers from CrowdStrike, Malwarebytes, and CISA) as "Sleeper Agents." These plugins often remain benign for months before receiving a malicious update.

### **Detection Strategy**
Unlike standard inventory searches, this query focuses on **File System Telemetry** (`FileCreate`, `FileUpdate`, `FileRename`). This ensures that even if the browser isn't currently running, the presence of the malicious assets on the disk is flagged.

## Query Logic
The query utilizes Regex to monitor the following paths for confirmed malicious Extension IDs:
* `%AppData%\Local\Google\Chrome\User Data\Default\Extensions\`
* `%AppData%\Local\Microsoft\Edge\User Data\Default\Extensions\`

## Usage
1. Copy the query from `malicious_extension_hunt.fql`.
2. Execute within the **CrowdStrike Falcon Advanced Event Search** console.
3. Review `FilePath` results to identify affected `aid` (Agent IDs) and `UserName`.

## Disclaimer
This query is provided for threat hunting and incident response purposes. All Indicator of Compromise (IOC) IDs should be verified against the latest threat intelligence feeds as campaigns evolve.
