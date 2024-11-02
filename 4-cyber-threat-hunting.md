# Cyber Threat Hunting Tracking Your Adversaries

Presented by Brent King

## What is Threat Hunting?

- Proactively and methodically searching for potential threats within your organization's computer systems and networks

## Why Threat Hunt?

- Prepare to be comrpomised
- Practice ability to search telemetry for malicious behaviour
- Reveal new detection methods and missing log sources
- Improve the configuartion of security tools
- Force security team to learn the environment which will make team more effective when a security event happens

## Precursors to Threat Hunting

1. Know your environment (Baseline):
- VPN, perimeter access points
- Crown Jewels
- Typical commands, processes, services, software, scripts
- Remote admin tools
- Administrators

2. Know your toolsets, data sources available
- What are my key toolsets?
- DO I have access to them?
- DO I know how to use them?

## Threat Hunting Process

1. Scope - define hunt mission
2. Hunt - search for adversary
3. Analyze - compare results against baseline
4. Action - Determine impact and take actions
5. Improve - Review defenses, log sources, and tooling for future hunts

## What Threat Hunting Tools?

- Threat Intelligence/Advisories
- MITRE Att&ck Framework
- EDR - Endpoint Detection and Response
- SIEM/Log Management tools
- Network Management Systems (flows, connections, PCAP)
- Web Access/Proxy
- IAM/Active Directory

## Top Telemetry and Data Sources

- Security Alerts
- Process Execution
- Command Shell
- Script Execution
- Registry Changes
- Remote Admin Tool
- File Read/Write
- URL Access
- DNS
- IP Connectivity/Netflow

## What Threats to Hunt for?

- Threat Advisories & Intel Reports:
    - Canadian Centre for Cyber Security
    - America's Cyber Defense Agent
- Indicators of Compromise (IoC)
- Tactics, Techniques and Procedures (TTPs)
- Cyber Threat Actor Toolset (BITSAdmin, Cobalt Strike, Mimikatz, PSExec, PowerShell)
