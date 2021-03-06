
# Scripting

## Description

### MITRE Description

> Adversaries may use scripts to aid in operations and perform multiple actions that would otherwise be manual. Scripting is useful for speeding up operational tasks and reducing the time required to gain access to critical resources. Some scripting languages may be used to bypass process monitoring mechanisms by directly interacting with the operating system at an API level instead of calling other programs. Common scripting languages for Windows include VBScript and [PowerShell](https://attack.mitre.org/techniques/T1086) but could also be in the form of command-line batch scripts.

Scripts can be embedded inside Office documents as macros that can be set to execute when files used in [Spearphishing Attachment](https://attack.mitre.org/techniques/T1193) and other types of spearphishing are opened. Malicious embedded macros are an alternative means of execution than software exploitation through [Exploitation for Client Execution](https://attack.mitre.org/techniques/T1203), where adversaries will rely on macros being allowed or that the user will accept to activate them.

Many popular offensive frameworks exist which use forms of scripting for security testers and adversaries alike. Metasploit (Citation: Metasploit_Ref), Veil (Citation: Veil_Ref), and PowerSploit (Citation: Powersploit) are three examples that are popular among penetration testers for exploit and post-compromise operations and include many features for evading defenses. Some adversaries are known to use PowerShell. (Citation: Alperovitch 2014)

## Aliases

```

```

## Additional Attributes

* Bypass: ['Process whitelisting', 'Data Execution Prevention', 'Exploit Prevention']
* Effective Permissions: None
* Network: None
* Permissions: ['User']
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1064

## Potential Commands

```
sh -c "echo 'echo Hello from the Atomic Red Team' > /tmp/art.sh"
sh -c "echo 'ping -c 4 8.8.8.8' >> /tmp/art.sh"
chmod +x /tmp/art.sh
sh /tmp/art.sh

Start-Process #{script_path}

Start-Process $env:TEMP\T1064_script.bat

{'windows': {'psh': {'command': 'Set-ItemProperty -Path HKLM:\\Software\\Policies\\Microsoft\\Windows\\PowerShell -Name ExecutionPolicy -Value ByPass;\n        $shell = New-Object -ComObject Wscript.Shell\n        Set-ExecutionPolicy Bypass | echo $shell.sendkeys("Y`r`n")'}}}
{'windows': {'psh': {'command': "$job = Start-Job -ScriptBlock {\n  $username = '#{host.user.name}';\n  $password = '#{host.user.password}';\n  $securePassword = ConvertTo-SecureString $password -AsPlainText -Force;\n  $credential = New-Object System.Management.Automation.PSCredential $username, $securePassword;\n  Start-Process Notepad.exe -NoNewWindow -PassThru -Credential $credential;\n};\nReceive-Job -Job $job -Wait;\n"}}}
cscript.exe
*.jse
cscript.exe
*.vbe
cscript.exe
*.js
cscript.exe
*.vba
cscript.exe
*.vbs
excel.exe
cmd.exe
excel.exe
cscript.exe
excel.exe
wscript.exe
excel.exe
sh.exe
excel.exe
bash.exe
mshta.exe
cscript.exe
mshta.exe
wscript.exe
powerpoint.exe
cmd.exe
powerpoint.exe
cscript.exe
powerpoint.exe
wscript.exe
powerpoint.exe
sh.exe
powerpoint.exe
bash.exe
winword.exe
cmd.exe
powershell.exe
winword.exe
cmd.exe
winword.exe
cscript.exe
winword.exe
wscript.exe
winword.exe
sh.exe
winword.exe
bash.exe
winword.exe
csc.exe
cvtres.exe
wscript.exe
wscript.exe
*.jse
wscript.exe
*.vbe
wscript.exe
*.js
wscript.exe
*.vba
wscript.exe
*.vbs
winword.exe
javaw.exe
java.exe
wscript.exe|cscript.exe
powershell/code_execution/invoke_metasploitpayload
powershell/code_execution/invoke_metasploitpayload
powershell/management/invoke_script
powershell/management/invoke_script
Creates and executes a simple bash script.
```

## Commands Dataset

```
[{'command': 'sh -c "echo \'echo Hello from the Atomic Red Team\' > '
             '/tmp/art.sh"\n'
             'sh -c "echo \'ping -c 4 8.8.8.8\' >> /tmp/art.sh"\n'
             'chmod +x /tmp/art.sh\n'
             'sh /tmp/art.sh\n',
  'name': None,
  'source': 'atomics/T1064/T1064.yaml'},
 {'command': 'Start-Process #{script_path}\n',
  'name': None,
  'source': 'atomics/T1064/T1064.yaml'},
 {'command': 'Start-Process $env:TEMP\\T1064_script.bat\n',
  'name': None,
  'source': 'atomics/T1064/T1064.yaml'},
 {'command': {'windows': {'psh': {'command': 'Set-ItemProperty -Path '
                                             'HKLM:\\Software\\Policies\\Microsoft\\Windows\\PowerShell '
                                             '-Name ExecutionPolicy -Value '
                                             'ByPass;\n'
                                             '        $shell = New-Object '
                                             '-ComObject Wscript.Shell\n'
                                             '        Set-ExecutionPolicy '
                                             'Bypass | echo '
                                             '$shell.sendkeys("Y`r`n")'}}},
  'name': 'Ensure the ExecutionPolicy is turned to Bypass',
  'source': 'data/abilities/defense-evasion/3864fd22-5c63-41c9-bdbc-a66b5ffa3f5e.yml'},
 {'command': {'windows': {'psh': {'command': '$job = Start-Job -ScriptBlock {\n'
                                             '  $username = '
                                             "'#{host.user.name}';\n"
                                             '  $password = '
                                             "'#{host.user.password}';\n"
                                             '  $securePassword = '
                                             'ConvertTo-SecureString $password '
                                             '-AsPlainText -Force;\n'
                                             '  $credential = New-Object '
                                             'System.Management.Automation.PSCredential '
                                             '$username, $securePassword;\n'
                                             '  Start-Process Notepad.exe '
                                             '-NoNewWindow -PassThru '
                                             '-Credential $credential;\n'
                                             '};\n'
                                             'Receive-Job -Job $job '
                                             '-Wait;\n'}}},
  'name': 'Run an application as a different user',
  'source': 'data/abilities/execution/3796a00b-b11d-4731-b4ca-275a07d83299.yml'},
 {'command': 'cscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.jse',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'cscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.vbe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'cscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.js',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'cscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.vba',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'cscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.vbs',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'excel.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'cmd.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'excel.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'cscript.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'excel.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'excel.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'sh.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'excel.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'bash.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'mshta.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'cscript.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'mshta.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'powerpoint.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'cmd.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'powerpoint.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'cscript.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'powerpoint.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'powerpoint.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'sh.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'powerpoint.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'bash.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'winword.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'cmd.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'powershell.exe',
  'name': 'sub_process_2',
  'source': 'Threat Hunting Tables'},
 {'command': 'winword.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'cmd.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'winword.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'cscript.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'winword.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'winword.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'sh.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'winword.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'bash.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'winword.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'csc.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'cvtres.exe',
  'name': 'sub_process_2',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.jse',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.vbe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.js',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.vba',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.vbs',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'winword.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': 'javaw.exe',
  'name': 'sub_process_1',
  'source': 'Threat Hunting Tables'},
 {'command': 'java.exe',
  'name': 'sub_process_2',
  'source': 'Threat Hunting Tables'},
 {'command': 'wscript.exe|cscript.exe',
  'name': None,
  'source': 'SysmonHunter - Scripting'},
 {'command': 'powershell/code_execution/invoke_metasploitpayload',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'powershell/code_execution/invoke_metasploitpayload',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'powershell/management/invoke_script',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'powershell/management/invoke_script',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'Creates and executes a simple bash script.',
  'name': None,
  'source': 'Kirtar22/Litmus_Test'}]
```

## Potential Detections

```json
[{'data_source': 'auditlogs (audit.rules)'},
 {'data_source': {'author': 'Florian Roth',
                  'description': 'Detects suspicious file execution by wscript '
                                 'and cscript',
                  'detection': {'condition': 'selection',
                                'selection': {'CommandLine': '*.vbs /shell *',
                                              'Image': '*\\cscript.exe'}},
                  'falsepositives': ['Unlikely'],
                  'fields': ['CommandLine', 'ParentCommandLine'],
                  'id': '966e4016-627f-44f7-8341-f394905c361f',
                  'level': 'critical',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'references': ['https://www.pwc.co.uk/cyber-security/pdf/cloud-hopper-annex-b-final.pdf'],
                  'tags': ['attack.execution', 'attack.g0045', 'attack.t1064'],
                  'title': 'WMIExec VBS Script'}},
 {'data_source': {'author': '@SBousseaden (detection), Thomas Patzke (rule)',
                  'description': 'Detects remote thread creation from '
                                 'CACTUSTORCH as described in references.',
                  'detection': {'condition': 'selection',
                                'selection': {'EventID': 8,
                                              'SourceImage': ['*\\System32\\cscript.exe',
                                                              '*\\System32\\wscript.exe',
                                                              '*\\System32\\mshta.exe',
                                                              '*\\winword.exe',
                                                              '*\\excel.exe'],
                                              'StartModule': None,
                                              'TargetImage': '*\\SysWOW64\\\\*'}},
                  'falsepositives': ['unknown'],
                  'id': '2e4e488a-6164-4811-9ea1-f960c7359c40',
                  'level': 'high',
                  'logsource': {'product': 'windows', 'service': 'sysmon'},
                  'references': ['https://twitter.com/SBousseaden/status/1090588499517079552',
                                 'https://github.com/mdsecactivebreach/CACTUSTORCH'],
                  'status': 'experimental',
                  'tags': ['attack.execution', 'attack.t1055', 'attack.t1064'],
                  'title': 'CACTUSTORCH Remote Thread Creation'}},
 {'data_source': {'author': 'Markus Neis',
                  'date': '2018/11/22',
                  'description': 'Detects Executables without '
                                 'FileVersion,Description,Product,Company '
                                 'likely created with py2exe',
                  'detection': {'condition': '1 of them',
                                'selection1': {'Description': '\\?',
                                               'FileVersion': '\\?'},
                                'selection2': {'Description': '\\?',
                                               'Product': '\\?'},
                                'selection3': {'Company': '\\?',
                                               'Description': '\\?'}},
                  'falsepositives': ['Unknown'],
                  'fields': ['CommandLine', 'ParentCommandLine'],
                  'id': '9637e8a5-7131-4f7f-bdc7-2b05d8670c43',
                  'level': 'medium',
                  'logsource': {'product': 'windows', 'service': 'sysmon'},
                  'modified': '2019/11/09',
                  'references': ['https://securelist.com/muddywater/88059/',
                                 'https://www.virustotal.com/#/file/276a765a10f98cda1a38d3a31e7483585ca3722ecad19d784441293acf1b7beb/detection'],
                  'status': 'experimental',
                  'tags': ['attack.defense_evasion',
                           'attack.execution',
                           'attack.t1064'],
                  'title': 'Suspicious File Characteristics due to Missing '
                           'Fields'}},
 {'data_source': {'action': 'global',
                  'author': 'Florian Roth, Tom Ueltschi',
                  'date': '2017/11/10',
                  'description': 'Detects javaw.exe in AppData folder as used '
                                 'by Adwind / JRAT',
                  'detection': {'condition': 'selection'},
                  'id': '1fac1481-2dbc-48b2-9096-753c49b4ec71',
                  'level': 'high',
                  'modified': '2018/12/11',
                  'references': ['https://www.hybrid-analysis.com/sample/ba86fa0d4b6af2db0656a88b1dd29f36fe362473ae8ad04255c4e52f214a541c?environmentId=100',
                                 'https://www.first.org/resources/papers/conf2017/Advanced-Incident-Detection-and-Threat-Hunting-using-Sysmon-and-Splunk.pdf'],
                  'status': 'experimental',
                  'tags': ['attack.execution', 'attack.t1064'],
                  'title': 'Adwind RAT / JRAT'}},
 {'data_source': {'detection': {'selection': {'CommandLine': ['*\\AppData\\Roaming\\Oracle*\\java*.exe '
                                                              '*',
                                                              '*cscript.exe '
                                                              '*Retrive*.vbs '
                                                              '*']}},
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'}}},
 {'data_source': {'detection': {'selection': {'EventID': 11,
                                              'TargetFilename': ['*\\AppData\\Roaming\\Oracle\\bin\\java*.exe',
                                                                 '*\\Retrive*.vbs']}},
                  'logsource': {'product': 'windows', 'service': 'sysmon'}}},
 {'data_source': {'detection': {'selection': {'Details': '%AppData%\\Roaming\\Oracle\\bin\\\\*',
                                              'EventID': 13,
                                              'TargetObject': '\\REGISTRY\\MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Run*'}},
                  'logsource': {'product': 'windows', 'service': 'sysmon'}}},
 {'data_source': {'author': 'Margaritis Dimitrios (idea), Florian Roth (rule)',
                  'description': 'Detects wscript/cscript executions of '
                                 'scripts located in user directories',
                  'detection': {'condition': 'selection and not falsepositive',
                                'falsepositive': {'ParentImage': '*\\winzip*'},
                                'selection': {'CommandLine': ['* '
                                                              'C:\\Users\\\\*.jse '
                                                              '*',
                                                              '* '
                                                              'C:\\Users\\\\*.vbe '
                                                              '*',
                                                              '* '
                                                              'C:\\Users\\\\*.js '
                                                              '*',
                                                              '* '
                                                              'C:\\Users\\\\*.vba '
                                                              '*',
                                                              '* '
                                                              'C:\\Users\\\\*.vbs '
                                                              '*',
                                                              '* '
                                                              'C:\\ProgramData\\\\*.jse '
                                                              '*',
                                                              '* '
                                                              'C:\\ProgramData\\\\*.vbe '
                                                              '*',
                                                              '* '
                                                              'C:\\ProgramData\\\\*.js '
                                                              '*',
                                                              '* '
                                                              'C:\\ProgramData\\\\*.vba '
                                                              '*',
                                                              '* '
                                                              'C:\\ProgramData\\\\*.vbs '
                                                              '*'],
                                              'Image': ['*\\wscript.exe',
                                                        '*\\cscript.exe']}},
                  'falsepositives': ['Winzip', 'Other self-extractors'],
                  'fields': ['CommandLine', 'ParentCommandLine'],
                  'id': 'cea72823-df4d-4567-950c-0b579eaf0846',
                  'level': 'high',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'status': 'experimental',
                  'tags': ['attack.defense_evasion',
                           'attack.execution',
                           'attack.t1064'],
                  'title': 'WScript or CScript Dropper'}},
 {'data_source': {'author': 'Florian Roth',
                  'date': '2018/04/06',
                  'description': 'Detects a suspicious child process of a '
                                 'Windows shell',
                  'detection': {'condition': 'selection and not falsepositives',
                                'falsepositives': {'CurrentDirectory': '*\\ccmcache\\\\*'},
                                'selection': {'Image': ['*\\schtasks.exe',
                                                        '*\\nslookup.exe',
                                                        '*\\certutil.exe',
                                                        '*\\bitsadmin.exe',
                                                        '*\\mshta.exe'],
                                              'ParentImage': ['*\\mshta.exe',
                                                              '*\\powershell.exe',
                                                              '*\\rundll32.exe',
                                                              '*\\cscript.exe',
                                                              '*\\wscript.exe',
                                                              '*\\wmiprvse.exe']}},
                  'falsepositives': ['Administrative scripts',
                                     'Microsoft SCCM'],
                  'fields': ['CommandLine', 'ParentCommandLine'],
                  'id': '3a6586ad-127a-4d3b-a677-1e6eacdf8fde',
                  'level': 'high',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'modified': '2019/02/05',
                  'references': ['https://mgreen27.github.io/posts/2018/04/02/DownloadCradle.html'],
                  'status': 'experimental',
                  'tags': ['attack.execution',
                           'attack.defense_evasion',
                           'attack.t1064'],
                  'title': 'Windows Shell Spawning Suspicious Program'}},
 {'data_source': {'author': 'juju4',
                  'description': 'Detects suspicious process related to '
                                 'rasdial.exe',
                  'detection': {'condition': 'selection',
                                'selection': {'CommandLine': ['rasdial']}},
                  'falsepositives': ['False positives depend on scripts and '
                                     'administrative tools used in the '
                                     'monitored environment'],
                  'id': '6bba49bf-7f8c-47d6-a1bb-6b4dece4640e',
                  'level': 'medium',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'references': ['https://twitter.com/subTee/status/891298217907830785'],
                  'status': 'experimental',
                  'tags': ['attack.defense_evasion',
                           'attack.execution',
                           'attack.t1064'],
                  'title': 'Suspicious RASdial Activity'}},
 {'data_source': {'author': 'Michael Haag',
                  'description': 'Detects suspicious file execution by wscript '
                                 'and cscript',
                  'detection': {'condition': 'selection',
                                'selection': {'CommandLine': ['*.jse',
                                                              '*.vbe',
                                                              '*.js',
                                                              '*.vba'],
                                              'Image': ['*\\wscript.exe',
                                                        '*\\cscript.exe']}},
                  'falsepositives': ['Will need to be tuned. I recommend '
                                     'adding the user profile path in '
                                     'CommandLine if it is getting too noisy.'],
                  'fields': ['CommandLine', 'ParentCommandLine'],
                  'id': '1e33157c-53b1-41ad-bbcc-780b80b58288',
                  'level': 'medium',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'status': 'experimental',
                  'tags': ['attack.execution', 'attack.t1064'],
                  'title': 'WSF/JSE/JS/VBA/VBE File Execution'}},
 {'data_source': {'author': 'Markus Neis / @Karneades',
                  'date': '2019/04/03',
                  'description': 'Detects WMI spawning PowerShell',
                  'detection': {'condition': 'selection',
                                'selection': {'Image': ['*\\powershell.exe'],
                                              'ParentImage': ['*\\wmiprvse.exe']}},
                  'falsepositives': ['AppvClient', 'CCM'],
                  'id': '692f0bec-83ba-4d04-af7e-e884a96059b6',
                  'level': 'high',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'references': ['https://github.com/Neo23x0/sigma/blob/master/rules/windows/process_creation/win_shell_spawn_susp_program.yml',
                                 'https://any.run/report/68bc255f9b0db6a0d30a8f2dadfbee3256acfe12497bf93943bc1eab0735e45e/a2385d6f-34f7-403c-90d3-b1f9d2a90a5e'],
                  'status': 'experimental',
                  'tags': ['attack.execution',
                           'attack.defense_evasion',
                           'attack.t1064'],
                  'title': 'WMI Spawning Windows PowerShell'}},
 {'data_source': ['4688 ', 'Process CMD Line']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['LMD - Hash Compare']},
 {'data_source': ['4688 ', 'Process CMD Line']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['LOG-MD - Hash Compare']}]
```

## Potential Queries

```json
[{'name': None,
  'product': 'Splunk',
  'query': 'index=linux sourcetype=linux_audit syscall=59 OR syscall=322  | '
           'table host,syscall,syscall_name,exe,auid'},
 {'name': None,
  'product': 'Splunk',
  'query': 'This could be very overwhelming if whitelisting is not done.'}]
```

## Raw Dataset

```json
[{'Atomic Red Team Test - Scripting': {'atomic_tests': [{'auto_generated_guid': '7e7ac3ed-f795-4fa5-b711-09d6fbe9b873',
                                                         'description': 'Creates '
                                                                        'and '
                                                                        'executes '
                                                                        'a '
                                                                        'simple '
                                                                        'bash '
                                                                        'script.\n',
                                                         'executor': {'command': 'sh '
                                                                                 '-c '
                                                                                 '"echo '
                                                                                 "'echo "
                                                                                 'Hello '
                                                                                 'from '
                                                                                 'the '
                                                                                 'Atomic '
                                                                                 'Red '
                                                                                 "Team' "
                                                                                 '> '
                                                                                 '/tmp/art.sh"\n'
                                                                                 'sh '
                                                                                 '-c '
                                                                                 '"echo '
                                                                                 "'ping "
                                                                                 '-c '
                                                                                 '4 '
                                                                                 "8.8.8.8' "
                                                                                 '>> '
                                                                                 '/tmp/art.sh"\n'
                                                                                 'chmod '
                                                                                 '+x '
                                                                                 '/tmp/art.sh\n'
                                                                                 'sh '
                                                                                 '/tmp/art.sh\n',
                                                                      'elevation_required': False,
                                                                      'name': 'sh'},
                                                         'name': 'Create and '
                                                                 'Execute Bash '
                                                                 'Shell Script',
                                                         'supported_platforms': ['macos',
                                                                                 'linux']},
                                                        {'auto_generated_guid': '9e8894c0-50bd-4525-a96c-d4ac78ece388',
                                                         'dependencies': [{'description': 'Batch '
                                                                                          'file '
                                                                                          'must '
                                                                                          'exist '
                                                                                          'on '
                                                                                          'disk '
                                                                                          'at '
                                                                                          'specified '
                                                                                          'location '
                                                                                          '(#{script_path})\n',
                                                                           'get_prereq_command': 'New-Item '
                                                                                                 '#{script_path} '
                                                                                                 '-Force '
                                                                                                 '| '
                                                                                                 'Out-Null\n'
                                                                                                 'Set-Content '
                                                                                                 '-Path '
                                                                                                 '#{script_path} '
                                                                                                 '-Value '
                                                                                                 '"#{command_to_execute}"\n',
                                                                           'prereq_command': 'if '
                                                                                             '(Test-Path '
                                                                                             '#{script_path}) '
                                                                                             '{exit '
                                                                                             '0} '
                                                                                             'else '
                                                                                             '{exit '
                                                                                             '1}\n'}],
                                                         'dependency_executor_name': 'powershell',
                                                         'description': 'Creates '
                                                                        'and '
                                                                        'executes '
                                                                        'a '
                                                                        'simple '
                                                                        'batch '
                                                                        'script. '
                                                                        'Upon '
                                                                        'execution, '
                                                                        'CMD '
                                                                        'will '
                                                                        'briefly '
                                                                        'launh '
                                                                        'to '
                                                                        'run '
                                                                        'the '
                                                                        'batch '
                                                                        'script '
                                                                        'then '
                                                                        'close '
                                                                        'again.\n',
                                                         'executor': {'cleanup_command': 'Remove-Item '
                                                                                         '#{script_path} '
                                                                                         '-Force '
                                                                                         '-ErrorAction '
                                                                                         'Ignore\n',
                                                                      'command': 'Start-Process '
                                                                                 '#{script_path}\n',
                                                                      'elevation_required': False,
                                                                      'name': 'powershell'},
                                                         'input_arguments': {'command_to_execute': {'default': 'dir',
                                                                                                    'description': 'Command '
                                                                                                                   'to '
                                                                                                                   'execute '
                                                                                                                   'within '
                                                                                                                   'script.',
                                                                                                    'type': 'string'},
                                                                             'script_path': {'default': '$env:TEMP\\T1064_script.bat',
                                                                                             'description': 'Path '
                                                                                                            'of '
                                                                                                            'script '
                                                                                                            'to '
                                                                                                            'create.',
                                                                                             'type': 'path'}},
                                                         'name': 'Create and '
                                                                 'Execute '
                                                                 'Batch Script',
                                                         'supported_platforms': ['windows']}],
                                       'attack_technique': 'T1064',
                                       'display_name': 'Scripting'}},
 {'Mitre Stockpile - Ensure the ExecutionPolicy is turned to Bypass': {'description': 'Ensure '
                                                                                      'the '
                                                                                      'ExecutionPolicy '
                                                                                      'is '
                                                                                      'turned '
                                                                                      'to '
                                                                                      'Bypass',
                                                                       'id': '3864fd22-5c63-41c9-bdbc-a66b5ffa3f5e',
                                                                       'name': 'Bypass '
                                                                               'ExecutionPolicy',
                                                                       'platforms': {'windows': {'psh': {'command': 'Set-ItemProperty '
                                                                                                                    '-Path '
                                                                                                                    'HKLM:\\Software\\Policies\\Microsoft\\Windows\\PowerShell '
                                                                                                                    '-Name '
                                                                                                                    'ExecutionPolicy '
                                                                                                                    '-Value '
                                                                                                                    'ByPass;\n'
                                                                                                                    '        '
                                                                                                                    '$shell '
                                                                                                                    '= '
                                                                                                                    'New-Object '
                                                                                                                    '-ComObject '
                                                                                                                    'Wscript.Shell\n'
                                                                                                                    '        '
                                                                                                                    'Set-ExecutionPolicy '
                                                                                                                    'Bypass '
                                                                                                                    '| '
                                                                                                                    'echo '
                                                                                                                    '$shell.sendkeys("Y`r`n")'}}},
                                                                       'tactic': 'defense-evasion',
                                                                       'technique': {'attack_id': 'T1064',
                                                                                     'name': 'Scripting'}}},
 {'Mitre Stockpile - Run an application as a different user': {'description': 'Run '
                                                                              'an '
                                                                              'application '
                                                                              'as '
                                                                              'a '
                                                                              'different '
                                                                              'user',
                                                               'id': '3796a00b-b11d-4731-b4ca-275a07d83299',
                                                               'name': 'Impersonate '
                                                                       'user',
                                                               'platforms': {'windows': {'psh': {'command': '$job '
                                                                                                            '= '
                                                                                                            'Start-Job '
                                                                                                            '-ScriptBlock '
                                                                                                            '{\n'
                                                                                                            '  '
                                                                                                            '$username '
                                                                                                            '= '
                                                                                                            "'#{host.user.name}';\n"
                                                                                                            '  '
                                                                                                            '$password '
                                                                                                            '= '
                                                                                                            "'#{host.user.password}';\n"
                                                                                                            '  '
                                                                                                            '$securePassword '
                                                                                                            '= '
                                                                                                            'ConvertTo-SecureString '
                                                                                                            '$password '
                                                                                                            '-AsPlainText '
                                                                                                            '-Force;\n'
                                                                                                            '  '
                                                                                                            '$credential '
                                                                                                            '= '
                                                                                                            'New-Object '
                                                                                                            'System.Management.Automation.PSCredential '
                                                                                                            '$username, '
                                                                                                            '$securePassword;\n'
                                                                                                            '  '
                                                                                                            'Start-Process '
                                                                                                            'Notepad.exe '
                                                                                                            '-NoNewWindow '
                                                                                                            '-PassThru '
                                                                                                            '-Credential '
                                                                                                            '$credential;\n'
                                                                                                            '};\n'
                                                                                                            'Receive-Job '
                                                                                                            '-Job '
                                                                                                            '$job '
                                                                                                            '-Wait;\n'}}},
                                                               'requirements': [{'plugins.stockpile.app.requirements.paw_provenance': [{'source': 'host.user.name'}]},
                                                                                {'plugins.stockpile.app.requirements.basic': [{'edge': 'has_password',
                                                                                                                               'source': 'host.user.name',
                                                                                                                               'target': 'host.user.password'}]}],
                                                               'tactic': 'execution',
                                                               'technique': {'attack_id': 'T1064',
                                                                             'name': 'Scripting'}}},
 {'Threat Hunting Tables': {'chain_id': '100016',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': 'ed01ebfbc9eb5bbea545af4d01bf5f1071661840480439c6e5babe8e080e41aa',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'cscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.jse',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100017',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': 'ed01ebfbc9eb5bbea545af4d01bf5f1071661840480439c6e5babe8e080e41aa',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'cscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.vbe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100018',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '4bcc2af66d843614f1a8ef0daeb1987c08ff6a5c4a9930f9307f65b07f0888bd',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'cscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.js',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100019',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': 'ed01ebfbc9eb5bbea545af4d01bf5f1071661840480439c6e5babe8e080e41aa',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'cscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.vba',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100020',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'high',
                            'itw_sample': '9feb89d55680071ce79f32529591bd3d51536f9e08672cb79d0ab81b57cf905d',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'cscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.vbs',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100026',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'excel.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'cmd.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100027',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'excel.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'cscript.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100028',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'powershell',
                            'os': 'windows',
                            'parent_process': 'excel.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'wscript.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100030',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'excel.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'sh.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100031',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'excel.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'bash.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100043',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '6707264f01730f55c79379d75d29000fb44c92de99b8a1d58588e05963f3dea6',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'mshta.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'cscript.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100044',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': 'aab57e55b04eb09ef97c7bc0c79d5c0ffeda557c7333777cd178adced03676cc',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'mshta.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'wscript.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100057',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'powerpoint.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'cmd.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100058',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'powerpoint.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'cscript.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100059',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'powerpoint.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'wscript.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100061',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'powerpoint.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'sh.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100062',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'powerpoint.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'bash.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100088',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '1d20934083558bc5a23e57b4f14ec1147f19d23807e8956714b256ae64f9692c',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'powershell',
                            'os': 'windows',
                            'parent_process': 'winword.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'cmd.exe',
                            'sub_process_2': 'powershell.exe'}},
 {'Threat Hunting Tables': {'chain_id': '100089',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'winword.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'cmd.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100090',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'winword.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'cscript.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100091',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'winword.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'wscript.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100093',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'winword.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'sh.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100094',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'winword.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'bash.exe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100097',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '947ce5214919e4395a2454375972d37756e1162890c62b0bb30e2a4be9ddaf54',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'winword.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'csc.exe',
                            'sub_process_2': 'cvtres.exe'}},
 {'Threat Hunting Tables': {'chain_id': '100103',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'wscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100104',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'wscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.jse',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100105',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'wscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.vbe',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100106',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'wscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.js',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100107',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'wscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.vba',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100108',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'wscript.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '*.vbs',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100126',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': 'https://www.joesandbox.com/analysis/35201/0/html',
                            'loaded_dll': '',
                            'mitre_attack': 'T1064',
                            'mitre_caption': 'scripting',
                            'os': 'windows',
                            'parent_process': 'winword.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': 'javaw.exe',
                            'sub_process_2': 'java.exe'}},
 {'SysmonHunter - T1064': {'description': None,
                           'level': 'high',
                           'name': 'Scripting',
                           'phase': 'Execution',
                           'query': [{'process': {'any': {'pattern': 'wscript.exe|cscript.exe'}},
                                      'type': 'process'}]}},
 {'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1064',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"powershell/code_execution/invoke_metasploitpayload":  '
                                                                                 '["T1064"],',
                                            'Empire Module': 'powershell/code_execution/invoke_metasploitpayload',
                                            'Technique': 'Scripting'}},
 {'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1064',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"powershell/management/invoke_script":  '
                                                                                 '["T1064"],',
                                            'Empire Module': 'powershell/management/invoke_script',
                                            'Technique': 'Scripting'}}]
```

# Tactics


* [Defense Evasion](../tactics/Defense-Evasion.md)

* [Execution](../tactics/Execution.md)
    

# Mitigations

None

# Actors


* [APT29](../actors/APT29.md)

* [Dark Caracal](../actors/Dark-Caracal.md)
    
* [Lazarus Group](../actors/Lazarus-Group.md)
    
* [Magic Hound](../actors/Magic-Hound.md)
    
* [MuddyWater](../actors/MuddyWater.md)
    
* [APT1](../actors/APT1.md)
    
* [Stealth Falcon](../actors/Stealth-Falcon.md)
    
* [OilRig](../actors/OilRig.md)
    
* [menuPass](../actors/menuPass.md)
    
* [FIN10](../actors/FIN10.md)
    
* [Deep Panda](../actors/Deep-Panda.md)
    
* [Leviathan](../actors/Leviathan.md)
    
* [APT3](../actors/APT3.md)
    
* [APT19](../actors/APT19.md)
    
* [FIN8](../actors/FIN8.md)
    
* [Dragonfly 2.0](../actors/Dragonfly-2.0.md)
    
* [Honeybee](../actors/Honeybee.md)
    
* [FIN6](../actors/FIN6.md)
    
* [BRONZE BUTLER](../actors/BRONZE-BUTLER.md)
    
* [Leafminer](../actors/Leafminer.md)
    
* [Rancor](../actors/Rancor.md)
    
* [FIN5](../actors/FIN5.md)
    
* [TA459](../actors/TA459.md)
    
* [Gamaredon Group](../actors/Gamaredon-Group.md)
    
* [Ke3chang](../actors/Ke3chang.md)
    
* [APT37](../actors/APT37.md)
    
* [Darkhotel](../actors/Darkhotel.md)
    
* [Cobalt Group](../actors/Cobalt-Group.md)
    
* [APT28](../actors/APT28.md)
    
* [APT32](../actors/APT32.md)
    
* [FIN4](../actors/FIN4.md)
    
* [Patchwork](../actors/Patchwork.md)
    
* [FIN7](../actors/FIN7.md)
    
* [Gallmaker](../actors/Gallmaker.md)
    
* [Gorgon Group](../actors/Gorgon-Group.md)
    
* [APT39](../actors/APT39.md)
    
* [WIRTE](../actors/WIRTE.md)
    
* [Silence](../actors/Silence.md)
    
* [TA505](../actors/TA505.md)
    
* [Turla](../actors/Turla.md)
    
* [Machete](../actors/Machete.md)
    
