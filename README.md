# CVE-2025-49666 Sigma Detection Rule

## Overview

This repository contains a Sigma detection rule for identifying exploitation attempts of **CVE-2025-49666**, a critical heap-based buffer overflow vulnerability in the Windows Setup and Boot Event Collection (SBEC) service.

## Vulnerability Details

- **CVE ID:** CVE-2025-49666
- **Severity:** High (CVSS 7.2)
- **Attack Vector:** Network (Requires authenticated network access)
- **Impact:** Remote Code Execution with SYSTEM-level privileges
- **Affected Component:** Windows SBEC Service (sbsvc.dll)

## Detection Logic

The rule detects two primary indicators of exploitation:

1. **Suspicious Child Processes** - Identifies command shells or scripts spawned by svchost.exe (which hosts the SBEC service) with references to 'sbsvc'
2. **Service Crashes** - Detects Windows Error Reporting (WerFault.exe) crashes related to the SBEC service, indicating failed exploitation attempts

## Requirements

- Windows event logging enabled
- Process creation logging (EventID 4688 or Sysmon EventID 1)
- Recommended: Sysmon for enhanced visibility

## False Positives

- Windows updates and system maintenance
- Legitimate administrative activities involving SBEC service

## Author

Patrick Maksimczuk

## References

- [Microsoft Security Response Center](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2025-49666)
- [MITRE ATT&CK: T1190](https://attack.mitre.org/techniques/T1190/)
- [MITRE ATT&CK: T1203](https://attack.mitre.org/techniques/T1203/)
