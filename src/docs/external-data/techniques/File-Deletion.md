
# File Deletion

## Description

### MITRE Description

> Malware, tools, or other non-native files dropped or created on a system by an adversary may leave traces behind as to what was done within a network and how. Adversaries may remove these files over the course of an intrusion to keep their footprint low or remove them at the end as part of the post-intrusion cleanup process.

There are tools available from the host operating system to perform cleanup, but adversaries may use other tools as well. Examples include native [cmd](https://attack.mitre.org/software/S0106) functions such as DEL, secure deletion tools such as Windows Sysinternals SDelete, or other third-party file deletion tools. (Citation: Trend Micro APT Attack Tools)

## Aliases

```

```

## Additional Attributes

* Bypass: ['Host forensic analysis']
* Effective Permissions: None
* Network: None
* Permissions: ['User']
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1107

## Potential Commands

```
rm -f /tmp/victim-files/a

rm -rf /tmp/victim-files

shred -u /tmp/victim-shred.txt

del /f %temp%\deleteme_T1107

rmdir /s /q %temp%\deleteme_T1107

Remove-Item -path $env:TEMP\deleteme_T1107

Remove-Item -Path $env:TEMP\deleteme_folder_T1107 -Recurse

rm -rf / --no-preserve-root > /dev/null 2> /dev/null

Remove-Item -Path (Join-Path "$Env:SystemRoot\prefetch\" (Get-ChildItem -Path "$Env:SystemRoot\prefetch\*.pf" -Name)[0])

Remove-Item $env:TEMP\TeamViewer_54.log

{'darwin': {'sh': {'command': '> $HOME/.bash_history && unset HISTFILE\n'}}, 'linux': {'sh': {'command': '> $HOME/.bash_history && unset HISTFILE\n'}}, 'windows': {'psh': {'command': 'Clear-History;Clear'}}}
```
rm -rf test1.text
```
```
rm -f test1.txt
```
```
shred -u test1.txt
```
```

## Commands Dataset

```
[{'command': 'rm -f /tmp/victim-files/a\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': 'rm -rf /tmp/victim-files\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': 'shred -u /tmp/victim-shred.txt\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': 'del /f %temp%\\deleteme_T1107\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': 'rmdir /s /q %temp%\\deleteme_T1107\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': 'Remove-Item -path $env:TEMP\\deleteme_T1107\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': 'Remove-Item -Path $env:TEMP\\deleteme_folder_T1107 -Recurse\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': 'rm -rf / --no-preserve-root > /dev/null 2> /dev/null\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': 'Remove-Item -Path (Join-Path "$Env:SystemRoot\\prefetch\\" '
             '(Get-ChildItem -Path "$Env:SystemRoot\\prefetch\\*.pf" '
             '-Name)[0])\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': 'Remove-Item $env:TEMP\\TeamViewer_54.log\n',
  'name': None,
  'source': 'atomics/T1107/T1107.yaml'},
 {'command': {'darwin': {'sh': {'command': '> $HOME/.bash_history && unset '
                                           'HISTFILE\n'}},
              'linux': {'sh': {'command': '> $HOME/.bash_history && unset '
                                          'HISTFILE\n'}},
              'windows': {'psh': {'command': 'Clear-History;Clear'}}},
  'name': 'Stop terminal from logging history',
  'source': 'data/abilities/defense-evasion/43b3754c-def4-4699-a673-1d85648fda6a.yml'},
 {'command': '```', 'name': None, 'source': 'Kirtar22/Litmus_Test'},
 {'command': 'rm -rf test1.text',
  'name': None,
  'source': 'Kirtar22/Litmus_Test'},
 {'command': '```', 'name': None, 'source': 'Kirtar22/Litmus_Test'},
 {'command': '```', 'name': None, 'source': 'Kirtar22/Litmus_Test'},
 {'command': 'rm -f test1.txt', 'name': None, 'source': 'Kirtar22/Litmus_Test'},
 {'command': '```', 'name': None, 'source': 'Kirtar22/Litmus_Test'},
 {'command': '```', 'name': None, 'source': 'Kirtar22/Litmus_Test'},
 {'command': 'shred -u test1.txt',
  'name': None,
  'source': 'Kirtar22/Litmus_Test'},
 {'command': '```', 'name': None, 'source': 'Kirtar22/Litmus_Test'}]
```

## Potential Detections

```json
[{'data_source': 'auditlogs (audit.rules)'},
 {'data_source': 'bash_history logs'},
 {'data_source': {'author': 'Florian Roth (rule), Tom U. @c_APT_ure '
                            '(collection)',
                  'description': 'Detects backup catalog deletions',
                  'detection': {'condition': 'selection',
                                'selection': {'EventID': 524,
                                              'Source': 'Backup'}},
                  'falsepositives': ['Unknown'],
                  'id': '9703792d-fd9a-456d-a672-ff92efe4806a',
                  'level': 'medium',
                  'logsource': {'product': 'windows', 'service': 'application'},
                  'references': ['https://technet.microsoft.com/en-us/library/cc742154(v=ws.11).aspx',
                                 'https://www.hybrid-analysis.com/sample/ed01ebfbc9eb5bbea545af4d01bf5f1071661840480439c6e5babe8e080e41aa?environmentId=100'],
                  'status': 'experimental',
                  'tags': ['attack.defense_evasion', 'attack.t1107'],
                  'title': 'Backup Catalog Deleted'}},
 {'data_source': ['4688 ', 'Process CMD Line']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['B9', 'Binary file metadata']},
 {'data_source': ['4688 ', 'Process CMD Line']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['LOG-MD - B9', 'Binary file metadata']}]
```

## Potential Queries

```json
[{'name': 'File Deletion',
  'product': 'Azure Sentinel',
  'query': 'Sysmon| where EventID == 1 and (process_command_line contains '
           '"*remove-item*"or process_command_line contains "vssadmin*Delete '
           'Shadows /All /Q*"or process_command_line contains '
           '"*wmic*shadowcopy delete*"or process_command_line contains '
           '"*wbdadmin* delete catalog -q*"or process_command_line contains '
           '"*bcdedit*bootstatuspolicy ignoreallfailures*"or '
           'process_command_line contains "*bcdedit*recoveryenabled no*")'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None,
  'product': 'Splunk',
  'query': 'index=linux sourcetype=linux_audit syscall=59 comm=shred | table '
           'host,auid,msg'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None,
  'product': 'Splunk',
  'query': 'index=linux sourcetype=linux_audit type=execve shred .bash_history '
           '| table host,msg,a0,a2'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None,
  'product': 'Splunk',
  'query': 'index=linux sourcetype=linux_audit syscall=263 | table '
           'host,auid,uid,eid,exe'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None,
  'product': 'Splunk',
  'query': 'index=linux sourcetype=linux_audit syscall=82 exe=/usr/bin/shred | '
           'table host,auid,uid,eid,exe'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None,
  'product': 'Splunk',
  'query': '-a always,exit -F arch=b64 -S execve,execveat -F auid>=1000 -F '
           'auid!=-1 -F key=program_execution'},
 {'name': None,
  'product': 'Splunk',
  'query': '-w /home/ec2-user/.bash_history -p rwa -k bash_history_changes'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None,
  'product': 'Splunk',
  'query': 'index=linux sourcetype="bash_history" bash_command="rm *"'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None, 'product': 'Splunk', 'query': '```'},
 {'name': None,
  'product': 'Splunk',
  'query': 'index=linux sourcetype="bash_history" bash_command="shred -u *"'},
 {'name': None, 'product': 'Splunk', 'query': '```'}]
```

## Raw Dataset

```json
[{'Atomic Red Team Test - File Deletion': {'atomic_tests': [{'auto_generated_guid': '562d737f-2fc6-4b09-8c2a-7f8ff0828480',
                                                             'description': 'Delete '
                                                                            'a '
                                                                            'single '
                                                                            'file '
                                                                            'from '
                                                                            'the '
                                                                            'temporary '
                                                                            'directory\n',
                                                             'executor': {'command': 'rm '
                                                                                     '-f '
                                                                                     '#{file_to_delete}\n',
                                                                          'name': 'sh'},
                                                             'input_arguments': {'file_to_delete': {'default': '/tmp/victim-files/a',
                                                                                                    'description': 'Path '
                                                                                                                   'of '
                                                                                                                   'file '
                                                                                                                   'to '
                                                                                                                   'delete',
                                                                                                    'type': 'Path'}},
                                                             'name': 'Delete a '
                                                                     'single '
                                                                     'file - '
                                                                     'Linux/macOS',
                                                             'supported_platforms': ['linux',
                                                                                     'macos']},
                                                            {'auto_generated_guid': 'a415f17e-ce8d-4ce2-a8b4-83b674e7017e',
                                                             'description': 'Recursively '
                                                                            'delete '
                                                                            'the '
                                                                            'temporary '
                                                                            'directory '
                                                                            'and '
                                                                            'all '
                                                                            'files '
                                                                            'contained '
                                                                            'within '
                                                                            'it\n',
                                                             'executor': {'command': 'rm '
                                                                                     '-rf '
                                                                                     '#{folder_to_delete}\n',
                                                                          'name': 'sh'},
                                                             'input_arguments': {'folder_to_delete': {'default': '/tmp/victim-files',
                                                                                                      'description': 'Path '
                                                                                                                     'of '
                                                                                                                     'folder '
                                                                                                                     'to '
                                                                                                                     'delete',
                                                                                                      'type': 'Path'}},
                                                             'name': 'Delete '
                                                                     'an '
                                                                     'entire '
                                                                     'folder - '
                                                                     'Linux/macOS',
                                                             'supported_platforms': ['linux',
                                                                                     'macos']},
                                                            {'auto_generated_guid': '039b4b10-2900-404b-b67f-4b6d49aa6499',
                                                             'description': 'Use '
                                                                            'the '
                                                                            '`shred` '
                                                                            'command '
                                                                            'to '
                                                                            'overwrite '
                                                                            'the '
                                                                            'temporary '
                                                                            'file '
                                                                            'and '
                                                                            'then '
                                                                            'delete '
                                                                            'it\n',
                                                             'executor': {'command': 'shred '
                                                                                     '-u '
                                                                                     '#{file_to_shred}\n',
                                                                          'name': 'sh'},
                                                             'input_arguments': {'file_to_shred': {'default': '/tmp/victim-shred.txt',
                                                                                                   'description': 'Path '
                                                                                                                  'of '
                                                                                                                  'file '
                                                                                                                  'to '
                                                                                                                  'shred',
                                                                                                   'type': 'Path'}},
                                                             'name': 'Overwrite '
                                                                     'and '
                                                                     'delete a '
                                                                     'file '
                                                                     'with '
                                                                     'shred',
                                                             'supported_platforms': ['linux']},
                                                            {'auto_generated_guid': '861ea0b4-708a-4d17-848d-186c9c7f17e3',
                                                             'dependencies': [{'description': 'The '
                                                                                              'file '
                                                                                              'to '
                                                                                              'delete '
                                                                                              'must '
                                                                                              'exist '
                                                                                              'on '
                                                                                              'disk '
                                                                                              'at '
                                                                                              'specified '
                                                                                              'location '
                                                                                              '(#{file_to_delete})\n',
                                                                               'get_prereq_command': 'echo '
                                                                                                     'deleteme_T1107 '
                                                                                                     '>> '
                                                                                                     '#{file_to_delete}\n',
                                                                               'prereq_command': 'IF '
                                                                                                 'EXIST '
                                                                                                 '"#{file_to_delete}" '
                                                                                                 '( '
                                                                                                 'EXIT '
                                                                                                 '0 '
                                                                                                 ') '
                                                                                                 'ELSE '
                                                                                                 '( '
                                                                                                 'EXIT '
                                                                                                 '1 '
                                                                                                 ')\n'}],
                                                             'dependency_executor_name': 'command_prompt',
                                                             'description': 'Delete '
                                                                            'a '
                                                                            'single '
                                                                            'file '
                                                                            'from '
                                                                            'the '
                                                                            'temporary '
                                                                            'directory '
                                                                            'using '
                                                                            'cmd.exe.\n'
                                                                            'Upon '
                                                                            'execution, '
                                                                            'no '
                                                                            'output '
                                                                            'will '
                                                                            'be '
                                                                            'displayed. '
                                                                            'Use '
                                                                            'File '
                                                                            'Explorer '
                                                                            'to '
                                                                            'verify '
                                                                            'the '
                                                                            'file '
                                                                            'was '
                                                                            'deleted.\n',
                                                             'executor': {'command': 'del '
                                                                                     '/f '
                                                                                     '#{file_to_delete}\n',
                                                                          'elevation_required': False,
                                                                          'name': 'command_prompt'},
                                                             'input_arguments': {'file_to_delete': {'default': '%temp%\\deleteme_T1107',
                                                                                                    'description': 'File '
                                                                                                                   'to '
                                                                                                                   'delete. '
                                                                                                                   'Run '
                                                                                                                   'the '
                                                                                                                   'prereq '
                                                                                                                   'command '
                                                                                                                   'to '
                                                                                                                   'create '
                                                                                                                   'it '
                                                                                                                   'if '
                                                                                                                   'it '
                                                                                                                   'does '
                                                                                                                   'not '
                                                                                                                   'exist.',
                                                                                                    'type': 'string'}},
                                                             'name': 'Delete a '
                                                                     'single '
                                                                     'file - '
                                                                     'Windows '
                                                                     'cmd',
                                                             'supported_platforms': ['windows']},
                                                            {'auto_generated_guid': 'ded937c4-2add-42f7-9c2c-c742b7a98698',
                                                             'dependencies': [{'description': 'The '
                                                                                              'file '
                                                                                              'to '
                                                                                              'delete '
                                                                                              'must '
                                                                                              'exist '
                                                                                              'on '
                                                                                              'disk '
                                                                                              'at '
                                                                                              'specified '
                                                                                              'location '
                                                                                              '(#{folder_to_delete})\n',
                                                                               'get_prereq_command': 'mkdir '
                                                                                                     '#{folder_to_delete}\n',
                                                                               'prereq_command': 'IF '
                                                                                                 'EXIST '
                                                                                                 '"#{folder_to_delete}" '
                                                                                                 '( '
                                                                                                 'EXIT '
                                                                                                 '0 '
                                                                                                 ') '
                                                                                                 'ELSE '
                                                                                                 '( '
                                                                                                 'EXIT '
                                                                                                 '1 '
                                                                                                 ')\n'}],
                                                             'dependency_executor_name': 'command_prompt',
                                                             'description': 'Recursively '
                                                                            'delete '
                                                                            'a '
                                                                            'folder '
                                                                            'in '
                                                                            'the '
                                                                            'temporary '
                                                                            'directory '
                                                                            'using '
                                                                            'cmd.exe.\n'
                                                                            'Upon '
                                                                            'execution, '
                                                                            'no '
                                                                            'output '
                                                                            'will '
                                                                            'be '
                                                                            'displayed. '
                                                                            'Use '
                                                                            'File '
                                                                            'Explorer '
                                                                            'to '
                                                                            'verify '
                                                                            'the '
                                                                            'folder '
                                                                            'was '
                                                                            'deleted.\n',
                                                             'executor': {'command': 'rmdir '
                                                                                     '/s '
                                                                                     '/q '
                                                                                     '#{folder_to_delete}\n',
                                                                          'elevation_required': False,
                                                                          'name': 'command_prompt'},
                                                             'input_arguments': {'folder_to_delete': {'default': '%temp%\\deleteme_T1107',
                                                                                                      'description': 'Folder '
                                                                                                                     'to '
                                                                                                                     'delete. '
                                                                                                                     'Run '
                                                                                                                     'the '
                                                                                                                     'prereq '
                                                                                                                     'command '
                                                                                                                     'to '
                                                                                                                     'create '
                                                                                                                     'it '
                                                                                                                     'if '
                                                                                                                     'it '
                                                                                                                     'does '
                                                                                                                     'not '
                                                                                                                     'exist.',
                                                                                                      'type': 'string'}},
                                                             'name': 'Delete '
                                                                     'an '
                                                                     'entire '
                                                                     'folder - '
                                                                     'Windows '
                                                                     'cmd',
                                                             'supported_platforms': ['windows']},
                                                            {'auto_generated_guid': '9dee89bd-9a98-4c4f-9e2d-4256690b0e72',
                                                             'dependencies': [{'description': 'The '
                                                                                              'file '
                                                                                              'to '
                                                                                              'delete '
                                                                                              'must '
                                                                                              'exist '
                                                                                              'on '
                                                                                              'disk '
                                                                                              'at '
                                                                                              'specified '
                                                                                              'location '
                                                                                              '(#{file_to_delete})\n',
                                                                               'get_prereq_command': 'New-Item '
                                                                                                     '-Path '
                                                                                                     '#{file_to_delete} '
                                                                                                     '| '
                                                                                                     'Out-Null\n',
                                                                               'prereq_command': 'if '
                                                                                                 '(Test-Path '
                                                                                                 '#{file_to_delete}) '
                                                                                                 '{exit '
                                                                                                 '0} '
                                                                                                 'else '
                                                                                                 '{exit '
                                                                                                 '1}\n'}],
                                                             'dependency_executor_name': 'powershell',
                                                             'description': 'Delete '
                                                                            'a '
                                                                            'single '
                                                                            'file '
                                                                            'from '
                                                                            'the '
                                                                            'temporary '
                                                                            'directory '
                                                                            'using '
                                                                            'Powershell. '
                                                                            'Upon '
                                                                            'execution, '
                                                                            'no '
                                                                            'output '
                                                                            'will '
                                                                            'be '
                                                                            'displayed. '
                                                                            'Use '
                                                                            'File '
                                                                            'Explorer '
                                                                            'to '
                                                                            'verify '
                                                                            'the '
                                                                            'file '
                                                                            'was '
                                                                            'deleted.\n',
                                                             'executor': {'command': 'Remove-Item '
                                                                                     '-path '
                                                                                     '#{file_to_delete}\n',
                                                                          'elevation_required': False,
                                                                          'name': 'powershell'},
                                                             'input_arguments': {'file_to_delete': {'default': '$env:TEMP\\deleteme_T1107',
                                                                                                    'description': 'File '
                                                                                                                   'to '
                                                                                                                   'delete. '
                                                                                                                   'Run '
                                                                                                                   'the '
                                                                                                                   'prereq '
                                                                                                                   'command '
                                                                                                                   'to '
                                                                                                                   'create '
                                                                                                                   'it '
                                                                                                                   'if '
                                                                                                                   'it '
                                                                                                                   'does '
                                                                                                                   'not '
                                                                                                                   'exist.',
                                                                                                    'type': 'string'}},
                                                             'name': 'Delete a '
                                                                     'single '
                                                                     'file - '
                                                                     'Windows '
                                                                     'PowerShell',
                                                             'supported_platforms': ['windows']},
                                                            {'auto_generated_guid': 'edd779e4-a509-4cba-8dfa-a112543dbfb1',
                                                             'dependencies': [{'description': 'The '
                                                                                              'folder '
                                                                                              'to '
                                                                                              'delete '
                                                                                              'must '
                                                                                              'exist '
                                                                                              'on '
                                                                                              'disk '
                                                                                              'at '
                                                                                              'specified '
                                                                                              'location '
                                                                                              '(#{folder_to_delete})\n',
                                                                               'get_prereq_command': 'New-Item '
                                                                                                     '-Path '
                                                                                                     '#{folder_to_delete} '
                                                                                                     '-Type '
                                                                                                     'Directory '
                                                                                                     '| '
                                                                                                     'Out-Null\n',
                                                                               'prereq_command': 'if '
                                                                                                 '(Test-Path '
                                                                                                 '#{folder_to_delete}) '
                                                                                                 '{exit '
                                                                                                 '0} '
                                                                                                 'else '
                                                                                                 '{exit '
                                                                                                 '1}\n'}],
                                                             'dependency_executor_name': 'powershell',
                                                             'description': 'Recursively '
                                                                            'delete '
                                                                            'a '
                                                                            'folder '
                                                                            'in '
                                                                            'the '
                                                                            'temporary '
                                                                            'directory '
                                                                            'using '
                                                                            'Powershell. '
                                                                            'Upon '
                                                                            'execution, '
                                                                            'no '
                                                                            'output '
                                                                            'will '
                                                                            'be '
                                                                            'displayed. '
                                                                            'Use '
                                                                            'File '
                                                                            'Explorer '
                                                                            'to '
                                                                            'verify '
                                                                            'the '
                                                                            'folder '
                                                                            'was '
                                                                            'deleted.\n',
                                                             'executor': {'command': 'Remove-Item '
                                                                                     '-Path '
                                                                                     '#{folder_to_delete} '
                                                                                     '-Recurse\n',
                                                                          'elevation_required': False,
                                                                          'name': 'powershell'},
                                                             'input_arguments': {'folder_to_delete': {'default': '$env:TEMP\\deleteme_folder_T1107',
                                                                                                      'description': 'Folder '
                                                                                                                     'to '
                                                                                                                     'delete. '
                                                                                                                     'Run '
                                                                                                                     'the '
                                                                                                                     'prereq '
                                                                                                                     'command '
                                                                                                                     'to '
                                                                                                                     'create '
                                                                                                                     'it '
                                                                                                                     'if '
                                                                                                                     'it '
                                                                                                                     'does '
                                                                                                                     'not '
                                                                                                                     'exist.',
                                                                                                      'type': 'string'}},
                                                             'name': 'Delete '
                                                                     'an '
                                                                     'entire '
                                                                     'folder - '
                                                                     'Windows '
                                                                     'PowerShell',
                                                             'supported_platforms': ['windows']},
                                                            {'auto_generated_guid': 'f3aa95fe-4f10-4485-ad26-abf22a764c52',
                                                             'description': 'This '
                                                                            'test '
                                                                            'deletes '
                                                                            'the '
                                                                            'entire '
                                                                            'root '
                                                                            'filesystem '
                                                                            'of '
                                                                            'a '
                                                                            'Linux '
                                                                            'system. '
                                                                            'This '
                                                                            'technique '
                                                                            'was '
                                                                            'used '
                                                                            'by '
                                                                            'Amnesia '
                                                                            'IoT '
                                                                            'malware '
                                                                            'to '
                                                                            'avoid '
                                                                            'analysis. '
                                                                            'This '
                                                                            'test '
                                                                            'is '
                                                                            'dangerous '
                                                                            'and '
                                                                            'destructive, '
                                                                            'do '
                                                                            'NOT '
                                                                            'use '
                                                                            'on '
                                                                            'production '
                                                                            'equipment.\n',
                                                             'executor': {'command': 'rm '
                                                                                     '-rf '
                                                                                     '/ '
                                                                                     '--no-preserve-root '
                                                                                     '> '
                                                                                     '/dev/null '
                                                                                     '2> '
                                                                                     '/dev/null\n',
                                                                          'name': 'bash'},
                                                             'name': 'Delete '
                                                                     'Filesystem '
                                                                     '- Linux',
                                                             'supported_platforms': ['linux']},
                                                            {'auto_generated_guid': '36f96049-0ad7-4a5f-8418-460acaeb92fb',
                                                             'description': 'Delete '
                                                                            'a '
                                                                            'single '
                                                                            'prefetch '
                                                                            'file.  '
                                                                            'Deletion '
                                                                            'of '
                                                                            'prefetch '
                                                                            'files '
                                                                            'is '
                                                                            'a '
                                                                            'known '
                                                                            'anti-forensic '
                                                                            'technique. '
                                                                            'To '
                                                                            'verify '
                                                                            'execution, '
                                                                            'Run '
                                                                            '"(Get-ChildItem '
                                                                            '-Path '
                                                                            '"$Env:SystemRoot\\prefetch\\*.pf" '
                                                                            '| '
                                                                            'Measure-Object).Count"\n'
                                                                            'before '
                                                                            'and '
                                                                            'after '
                                                                            'the '
                                                                            'test '
                                                                            'to '
                                                                            'verify '
                                                                            'that '
                                                                            'the '
                                                                            'number '
                                                                            'of '
                                                                            'prefetch '
                                                                            'files '
                                                                            'decreases '
                                                                            'by '
                                                                            '1.\n',
                                                             'executor': {'command': 'Remove-Item '
                                                                                     '-Path '
                                                                                     '(Join-Path '
                                                                                     '"$Env:SystemRoot\\prefetch\\" '
                                                                                     '(Get-ChildItem '
                                                                                     '-Path '
                                                                                     '"$Env:SystemRoot\\prefetch\\*.pf" '
                                                                                     '-Name)[0])\n',
                                                                          'elevation_required': True,
                                                                          'name': 'powershell'},
                                                             'name': 'Delete-PrefetchFile',
                                                             'supported_platforms': ['windows']},
                                                            {'auto_generated_guid': '69f50a5f-967c-4327-a5bb-e1a9a9983785',
                                                             'dependencies': [{'description': 'The '
                                                                                              'folder '
                                                                                              'to '
                                                                                              'delete '
                                                                                              'must '
                                                                                              'exist '
                                                                                              'on '
                                                                                              'disk '
                                                                                              'at '
                                                                                              'specified '
                                                                                              'location '
                                                                                              '(#{teamviewer_log_file})\n',
                                                                               'get_prereq_command': 'New-Item '
                                                                                                     '-Path '
                                                                                                     '#{teamviewer_log_file} '
                                                                                                     '| '
                                                                                                     'Out-Null\n',
                                                                               'prereq_command': 'if '
                                                                                                 '(Test-Path '
                                                                                                 '#{teamviewer_log_file}) '
                                                                                                 '{exit '
                                                                                                 '0} '
                                                                                                 'else '
                                                                                                 '{exit '
                                                                                                 '1}\n'}],
                                                             'dependency_executor_name': 'powershell',
                                                             'description': 'Adversaries '
                                                                            'may '
                                                                            'delete '
                                                                            'TeamViewer '
                                                                            'log '
                                                                            'files '
                                                                            'to '
                                                                            'hide '
                                                                            'activity. '
                                                                            'This '
                                                                            'should '
                                                                            'provide '
                                                                            'a '
                                                                            'high '
                                                                            'true-positive '
                                                                            'alert '
                                                                            'ration.\n'
                                                                            'This '
                                                                            'test '
                                                                            'just '
                                                                            'places '
                                                                            'the '
                                                                            'files '
                                                                            'in '
                                                                            'a '
                                                                            'non-TeamViewer '
                                                                            'folder, '
                                                                            'a '
                                                                            'detection '
                                                                            'would '
                                                                            'just '
                                                                            'check '
                                                                            'for '
                                                                            'a '
                                                                            'deletion '
                                                                            'event '
                                                                            'matching '
                                                                            'the '
                                                                            'TeamViewer\n'
                                                                            'log '
                                                                            'file '
                                                                            'format '
                                                                            'of '
                                                                            'TeamViewer_##.log. '
                                                                            'Upon '
                                                                            'execution, '
                                                                            'no '
                                                                            'output '
                                                                            'will '
                                                                            'be '
                                                                            'displayed. '
                                                                            'Use '
                                                                            'File '
                                                                            'Explorer '
                                                                            'to '
                                                                            'verify '
                                                                            'the '
                                                                            'folder '
                                                                            'was '
                                                                            'deleted.\n'
                                                                            '\n'
                                                                            'https://twitter.com/SBousseaden/status/1197524463304290305?s=20\n',
                                                             'executor': {'command': 'Remove-Item '
                                                                                     '#{teamviewer_log_file}\n',
                                                                          'elevation_required': False,
                                                                          'name': 'powershell'},
                                                             'input_arguments': {'teamviewer_log_file': {'default': '$env:TEMP\\TeamViewer_54.log',
                                                                                                         'description': 'Teamviewer '
                                                                                                                        'log '
                                                                                                                        'file '
                                                                                                                        'to '
                                                                                                                        'delete. '
                                                                                                                        'Run '
                                                                                                                        'the '
                                                                                                                        'prereq '
                                                                                                                        'command '
                                                                                                                        'to '
                                                                                                                        'create '
                                                                                                                        'it '
                                                                                                                        'if '
                                                                                                                        'it '
                                                                                                                        'does '
                                                                                                                        'not '
                                                                                                                        'exist.',
                                                                                                         'type': 'string'}},
                                                             'name': 'Delete '
                                                                     'TeamViewer '
                                                                     'Log '
                                                                     'Files',
                                                             'supported_platforms': ['windows']}],
                                           'attack_technique': 'T1107',
                                           'display_name': 'File Deletion'}},
 {'Mitre Stockpile - Stop terminal from logging history': {'description': 'Stop '
                                                                          'terminal '
                                                                          'from '
                                                                          'logging '
                                                                          'history',
                                                           'id': '43b3754c-def4-4699-a673-1d85648fda6a',
                                                           'name': 'Avoid logs',
                                                           'platforms': {'darwin': {'sh': {'command': '> '
                                                                                                      '$HOME/.bash_history '
                                                                                                      '&& '
                                                                                                      'unset '
                                                                                                      'HISTFILE\n'}},
                                                                         'linux': {'sh': {'command': '> '
                                                                                                     '$HOME/.bash_history '
                                                                                                     '&& '
                                                                                                     'unset '
                                                                                                     'HISTFILE\n'}},
                                                                         'windows': {'psh': {'command': 'Clear-History;Clear'}}},
                                                           'tactic': 'defense-evasion',
                                                           'technique': {'attack_id': 'T1107',
                                                                         'name': 'File '
                                                                                 'Deletion'}}}]
```

# Tactics


* [Defense Evasion](../tactics/Defense-Evasion.md)


# Mitigations

None

# Actors


* [OilRig](../actors/OilRig.md)

* [Honeybee](../actors/Honeybee.md)
    
* [Group5](../actors/Group5.md)
    
* [FIN5](../actors/FIN5.md)
    
* [Patchwork](../actors/Patchwork.md)
    
* [Lazarus Group](../actors/Lazarus-Group.md)
    
* [FIN10](../actors/FIN10.md)
    
* [BRONZE BUTLER](../actors/BRONZE-BUTLER.md)
    
* [FIN8](../actors/FIN8.md)
    
* [Threat Group-3390](../actors/Threat-Group-3390.md)
    
* [Cobalt Group](../actors/Cobalt-Group.md)
    
* [APT29](../actors/APT29.md)
    
* [Dragonfly 2.0](../actors/Dragonfly-2.0.md)
    
* [APT28](../actors/APT28.md)
    
* [Magic Hound](../actors/Magic-Hound.md)
    
* [menuPass](../actors/menuPass.md)
    
* [APT3](../actors/APT3.md)
    
* [APT38](../actors/APT38.md)
    
* [APT18](../actors/APT18.md)
    
* [APT32](../actors/APT32.md)
    
* [TEMP.Veles](../actors/TEMP.Veles.md)
    
* [The White Company](../actors/The-White-Company.md)
    
* [Silence](../actors/Silence.md)
    
* [Kimsuky](../actors/Kimsuky.md)
    
* [APT41](../actors/APT41.md)
    
