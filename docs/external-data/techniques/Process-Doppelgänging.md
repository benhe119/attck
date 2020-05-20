
# Process Doppelgänging

## Description

### MITRE Description

> Windows Transactional NTFS (TxF) was introduced in Vista as a method to perform safe file operations. (Citation: Microsoft TxF) To ensure data integrity, TxF enables only one transacted handle to write to a file at a given time. Until the write handle transaction is terminated, all other handles are isolated from the writer and may only read the committed version of the file that existed at the time the handle was opened. (Citation: Microsoft Basic TxF Concepts) To avoid corruption, TxF performs an automatic rollback if the system or application fails during a write transaction. (Citation: Microsoft Where to use TxF)

Although deprecated, the TxF application programming interface (API) is still enabled as of Windows 10. (Citation: BlackHat Process Doppelgänging Dec 2017)

Adversaries may leverage TxF to a perform a file-less variation of [Process Injection](https://attack.mitre.org/techniques/T1055) called Process Doppelgänging. Similar to [Process Hollowing](https://attack.mitre.org/techniques/T1093), Process Doppelgänging involves replacing the memory of a legitimate process, enabling the veiled execution of malicious code that may evade defenses and detection. Process Doppelgänging's use of TxF also avoids the use of highly-monitored API functions such as NtUnmapViewOfSection, VirtualProtectEx, and SetThreadContext. (Citation: BlackHat Process Doppelgänging Dec 2017)

Process Doppelgänging is implemented in 4 steps (Citation: BlackHat Process Doppelgänging Dec 2017):

* Transact – Create a TxF transaction using a legitimate executable then overwrite the file with malicious code. These changes will be isolated and only visible within the context of the transaction.
* Load – Create a shared section of memory and load the malicious executable.
* Rollback – Undo changes to original executable, effectively removing malicious code from the file system.
* Animate – Create a process from the tainted section of memory and initiate execution.

## Aliases

```

```

## Additional Attributes

* Bypass: ['Process whitelisting', 'Anti-virus', 'Whitelisting by file name or path', 'Signature-based detection']
* Effective Permissions: None
* Network: None
* Permissions: ['Administrator', 'SYSTEM', 'User']
* Platforms: ['Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1186

## Potential Commands

```

```

## Commands Dataset

```

```

## Potential Detections

```json
[{'data_source': ['4688', 'Process Execution']},
 {'data_source': ['API monitoring']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['API monitoring']}]
```

## Potential Queries

```json

```

## Raw Dataset

```json

```

# Tactics


* [Defense Evasion](../tactics/Defense-Evasion.md)


# Mitigations

None

# Actors

None
