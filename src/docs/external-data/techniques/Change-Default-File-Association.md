
# Change Default File Association

## Description

### MITRE Description

> When a file is opened, the default program used to open the file (also called the file association or handler) is checked. File association selections are stored in the Windows Registry and can be edited by users, administrators, or programs that have Registry access (Citation: Microsoft Change Default Programs) (Citation: Microsoft File Handlers) or by administrators using the built-in assoc utility. (Citation: Microsoft Assoc Oct 2017) Applications can modify the file association for a given file extension to call an arbitrary program when a file with the given extension is opened.

System file associations are listed under <code>HKEY_CLASSES_ROOT\.[extension]</code>, for example <code>HKEY_CLASSES_ROOT\.txt</code>. The entries point to a handler for that extension located at <code>HKEY_CLASSES_ROOT\[handler]</code>. The various commands are then listed as subkeys underneath the shell key at <code>HKEY_CLASSES_ROOT\[handler]\shell\[action]\command</code>. For example:
* <code>HKEY_CLASSES_ROOT\txtfile\shell\open\command</code>
* <code>HKEY_CLASSES_ROOT\txtfile\shell\print\command</code>
* <code>HKEY_CLASSES_ROOT\txtfile\shell\printto\command</code>

The values of the keys listed are commands that are executed when the handler opens the file extension. Adversaries can modify these values to continually execute arbitrary commands. (Citation: TrendMicro TROJ-FAKEAV OCT 2012)

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['User', 'Administrator', 'SYSTEM']
* Platforms: ['Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1042

## Potential Commands

```
assoc .hta=#{target_extension_handler}

assoc #{extension_to_change}=txtfile

\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\FileExts|HKCR\\.+\\shell\\open\\commandWindows\Explorer.EXE
assoc.exe
```

## Commands Dataset

```
[{'command': 'assoc .hta=#{target_extension_handler}\n',
  'name': None,
  'source': 'atomics/T1042/T1042.yaml'},
 {'command': 'assoc #{extension_to_change}=txtfile\n',
  'name': None,
  'source': 'atomics/T1042/T1042.yaml'},
 {'command': '\\\\Software\\\\Microsoft\\\\Windows\\\\CurrentVersion\\\\Explorer\\\\FileExts|HKCR\\\\.+\\\\shell\\\\open\\\\commandWindows\\Explorer.EXE',
  'name': None,
  'source': 'SysmonHunter - Change Default File Association'},
 {'command': 'assoc.exe',
  'name': None,
  'source': 'SysmonHunter - Change Default File Association'}]
```

## Potential Detections

```json
[{'data_source': {'author': 'Timur Zinniatullin, oscd.community',
                  'date': '2019/10/21',
                  'description': 'When a file is opened, the default program '
                                 'used to open the file (also called the file '
                                 'association or handler) is checked. File '
                                 'association selections are stored in the '
                                 'Windows Registry and can be edited by users, '
                                 'administrators, or programs that have '
                                 'Registry access or by administrators using '
                                 'the built-in assoc utility. Applications can '
                                 'modify the file association for a given file '
                                 'extension to call an arbitrary program when '
                                 'a file with the given extension is opened.',
                  'detection': {'condition': 'selection',
                                'selection': {'CommandLine|contains|all': ['cmd',
                                                                           '/c',
                                                                           'assoc']}},
                  'falsepositives': ['Admin activity'],
                  'fields': ['Image',
                             'CommandLine',
                             'User',
                             'LogonGuid',
                             'Hashes',
                             'ParentProcessGuid',
                             'ParentCommandLine'],
                  'id': '3d3aa6cd-6272-44d6-8afc-7e88dfef7061',
                  'level': 'low',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'modified': '2019/11/04',
                  'references': ['https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1042/T1042.yaml'],
                  'status': 'experimental',
                  'tags': ['attack.persistence', 'attack.t1042'],
                  'title': 'Change Default File Association'}},
 {'data_source': ['4657', 'Windows Registry']},
 {'data_source': ['4688 ', 'Process CMD Line']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['4657', 'Windows Registry']},
 {'data_source': ['4688 ', 'Process CMD Line']},
 {'data_source': ['4688', 'Process Execution']}]
```

## Potential Queries

```json
[{'name': 'Change Default File Association',
  'product': 'Azure Sentinel',
  'query': 'Sysmon| where (EventID == 12 or EventID == 13 or EventID == 14)and '
           '(registry_key_path contains "\\\\SOFTWARE\\\\Classes\\\\"or '
           'registry_key_path contains '
           '"\\\\SOFTWARE\\\\Microsoft\\\\Windows\\\\CurrentVersion\\\\Explorer\\\\GlobalAssocChangedCounter")'}]
```

## Raw Dataset

```json
[{'Atomic Red Team Test - Change Default File Association': {'atomic_tests': [{'auto_generated_guid': '10a08978-2045-4d62-8c42-1957bbbea102',
                                                                               'description': 'Change '
                                                                                              'Default '
                                                                                              'File '
                                                                                              'Association '
                                                                                              'From '
                                                                                              'cmd.exe '
                                                                                              'of '
                                                                                              'hta '
                                                                                              'to '
                                                                                              'notepad.\n'
                                                                                              '\n'
                                                                                              'Upon '
                                                                                              'successful '
                                                                                              'execution, '
                                                                                              'cmd.exe '
                                                                                              'will '
                                                                                              'change '
                                                                                              'the '
                                                                                              'file '
                                                                                              'association '
                                                                                              'of '
                                                                                              '.hta '
                                                                                              'to '
                                                                                              'notepad.exe. \n',
                                                                               'executor': {'cleanup_command': 'assoc '
                                                                                                               '.hta=htafile\n',
                                                                                            'command': 'assoc '
                                                                                                       '#{extension_to_change}=#{target_extension_handler}\n',
                                                                                            'elevation_required': False,
                                                                                            'name': 'command_prompt'},
                                                                               'input_arguments': {'extension_to_change': {'default': '.hta',
                                                                                                                           'description': 'File '
                                                                                                                                          'Extension '
                                                                                                                                          'To '
                                                                                                                                          'Hijack',
                                                                                                                           'type': 'String'},
                                                                                                   'target_extension_handler': {'default': 'txtfile',
                                                                                                                                'description': 'txtfile '
                                                                                                                                               'maps '
                                                                                                                                               'to '
                                                                                                                                               'notepad.exe',
                                                                                                                                'type': 'Path'}},
                                                                               'name': 'Change '
                                                                                       'Default '
                                                                                       'File '
                                                                                       'Association',
                                                                               'supported_platforms': ['windows']}],
                                                             'attack_technique': 'T1042',
                                                             'display_name': 'Change '
                                                                             'Default '
                                                                             'File '
                                                                             'Association'}},
 {'SysmonHunter - T1042': {'description': None,
                           'level': 'medium',
                           'name': 'Change Default File Association',
                           'phase': 'Persistence',
                           'query': [{'op': 'and',
                                      'process': {'image': {'op': 'not',
                                                            'pattern': 'Windows\\Explorer.EXE'}},
                                      'reg': {'path': {'flag': 'regex',
                                                       'pattern': '\\\\Software\\\\Microsoft\\\\Windows\\\\CurrentVersion\\\\Explorer\\\\FileExts|HKCR\\\\.+\\\\shell\\\\open\\\\command'}},
                                      'type': 'reg'},
                                     {'process': {'any': {'pattern': 'assoc.exe'}},
                                      'type': 'process'}]}}]
```

# Tactics


* [Persistence](../tactics/Persistence.md)


# Mitigations

None

# Actors


* [Kimsuky](../actors/Kimsuky.md)

