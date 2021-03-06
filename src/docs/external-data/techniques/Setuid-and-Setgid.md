
# Setuid and Setgid

## Description

### MITRE Description

> When the setuid or setgid bits are set on Linux or macOS for an application, this means that the application will run with the privileges of the owning user or group respectively  (Citation: setuid man page). Normally an application is run in the current user’s context, regardless of which user or group owns the application. There are instances where programs need to be executed in an elevated context to function properly, but the user running them doesn’t need the elevated privileges. Instead of creating an entry in the sudoers file, which must be done by root, any user can specify the setuid or setgid flag to be set for their own applications. These bits are indicated with an "s" instead of an "x" when viewing a file's attributes via <code>ls -l</code>. The <code>chmod</code> program can set these bits with via bitmasking, <code>chmod 4777 [file]</code> or via shorthand naming, <code>chmod u+s [file]</code>.

An adversary can take advantage of this to either do a shell escape or exploit a vulnerability in an application with the setsuid or setgid bits to get code running in a different user’s context. Additionally, adversaries can use this mechanism on their own malware to make sure they're able to execute in elevated contexts in the future  (Citation: OSX Keydnap malware).

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: ['Administrator', 'root']
* Network: None
* Permissions: ['User']
* Platforms: ['Linux', 'macOS']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1166

## Potential Commands

```
cp PathToAtomicsFolder/T1166/src/hello.c /tmp/hello.c
sudo chown root /tmp/hello.c
sudo make /tmp/hello
sudo chown root /tmp/hello
sudo chmod u+s /tmp/hello
/tmp/hello

sudo touch /tmp/evilBinary
sudo chown root /tmp/evilBinary
sudo chmod u+s /tmp/evilBinary

sudo touch /tmp/evilBinary
sudo chown root /tmp/evilBinary
sudo chmod g+s /tmp/evilBinary

sudo chmod u+s hello
sudo chmod u+s #{file_to_setuid}
sudo chmod g+s #{file_to_setuid}
```

## Commands Dataset

```
[{'command': 'cp PathToAtomicsFolder/T1166/src/hello.c /tmp/hello.c\n'
             'sudo chown root /tmp/hello.c\n'
             'sudo make /tmp/hello\n'
             'sudo chown root /tmp/hello\n'
             'sudo chmod u+s /tmp/hello\n'
             '/tmp/hello\n',
  'name': None,
  'source': 'atomics/T1166/T1166.yaml'},
 {'command': 'sudo touch /tmp/evilBinary\n'
             'sudo chown root /tmp/evilBinary\n'
             'sudo chmod u+s /tmp/evilBinary\n',
  'name': None,
  'source': 'atomics/T1166/T1166.yaml'},
 {'command': 'sudo touch /tmp/evilBinary\n'
             'sudo chown root /tmp/evilBinary\n'
             'sudo chmod g+s /tmp/evilBinary\n',
  'name': None,
  'source': 'atomics/T1166/T1166.yaml'},
 {'command': 'sudo chmod u+s hello',
  'name': None,
  'source': 'Kirtar22/Litmus_Test'},
 {'command': 'sudo chmod u+s #{file_to_setuid}',
  'name': None,
  'source': 'Kirtar22/Litmus_Test'},
 {'command': 'sudo chmod g+s #{file_to_setuid}',
  'name': None,
  'source': 'Kirtar22/Litmus_Test'}]
```

## Potential Detections

```json
[{'data_source': 'bash_history'}, {'data_source': 'scripted_input'}]
```

## Potential Queries

```json
[{'name': None,
  'product': 'Splunk',
  'query': 'index=linux sourcetype=bash_history "chmod 4***" OR "chmod 2***" '
           'OR "chmod u+s" OR "chmod g+s" | table host,user_name,bash_command'},
 {'name': None,
  'product': 'Splunk',
  'query': 'find Setuid: find / -type f -perm /4000 OR find / -type f -perm '
           '/u+s'},
 {'name': None,
  'product': 'Splunk',
  'query': 'find Setgid: find / -type f -perm /2000 OR find / -type f -perm '
           '/g+s'},
 {'name': None,
  'product': 'Splunk',
  'query': 'Create a scripted input to ingest the files with Setuid and Setgid '
           'bits set and compare it with the expectde whitelist.'}]
```

## Raw Dataset

```json
[{'Atomic Red Team Test - Setuid and Setgid': {'atomic_tests': [{'auto_generated_guid': '896dfe97-ae43-4101-8e96-9a7996555d80',
                                                                 'description': 'Make, '
                                                                                'change '
                                                                                'owner, '
                                                                                'and '
                                                                                'change '
                                                                                'file '
                                                                                'attributes '
                                                                                'on '
                                                                                'a '
                                                                                'C '
                                                                                'source '
                                                                                'code '
                                                                                'file\n',
                                                                 'executor': {'cleanup_command': 'sudo '
                                                                                                 'rm '
                                                                                                 '/tmp/hello\n'
                                                                                                 'sudo '
                                                                                                 'rm '
                                                                                                 '/tmp/hello.c\n',
                                                                              'command': 'cp '
                                                                                         '#{payload} '
                                                                                         '/tmp/hello.c\n'
                                                                                         'sudo '
                                                                                         'chown '
                                                                                         'root '
                                                                                         '/tmp/hello.c\n'
                                                                                         'sudo '
                                                                                         'make '
                                                                                         '/tmp/hello\n'
                                                                                         'sudo '
                                                                                         'chown '
                                                                                         'root '
                                                                                         '/tmp/hello\n'
                                                                                         'sudo '
                                                                                         'chmod '
                                                                                         'u+s '
                                                                                         '/tmp/hello\n'
                                                                                         '/tmp/hello\n',
                                                                              'elevation_required': True,
                                                                              'name': 'sh'},
                                                                 'input_arguments': {'payload': {'default': 'PathToAtomicsFolder/T1166/src/hello.c',
                                                                                                 'description': 'hello.c '
                                                                                                                'payload',
                                                                                                 'type': 'path'}},
                                                                 'name': 'Make '
                                                                         'and '
                                                                         'modify '
                                                                         'binary '
                                                                         'from '
                                                                         'C '
                                                                         'source',
                                                                 'supported_platforms': ['macos',
                                                                                         'linux']},
                                                                {'auto_generated_guid': '759055b3-3885-4582-a8ec-c00c9d64dd79',
                                                                 'description': 'This '
                                                                                'test '
                                                                                'sets '
                                                                                'the '
                                                                                'SetUID '
                                                                                'flag '
                                                                                'on '
                                                                                'a '
                                                                                'file '
                                                                                'in '
                                                                                'Linux '
                                                                                'and '
                                                                                'macOS.\n',
                                                                 'executor': {'cleanup_command': 'sudo '
                                                                                                 'rm '
                                                                                                 '#{file_to_setuid}\n',
                                                                              'command': 'sudo '
                                                                                         'touch '
                                                                                         '#{file_to_setuid}\n'
                                                                                         'sudo '
                                                                                         'chown '
                                                                                         'root '
                                                                                         '#{file_to_setuid}\n'
                                                                                         'sudo '
                                                                                         'chmod '
                                                                                         'u+s '
                                                                                         '#{file_to_setuid}\n',
                                                                              'elevation_required': True,
                                                                              'name': 'sh'},
                                                                 'input_arguments': {'file_to_setuid': {'default': '/tmp/evilBinary',
                                                                                                        'description': 'Path '
                                                                                                                       'of '
                                                                                                                       'file '
                                                                                                                       'to '
                                                                                                                       'set '
                                                                                                                       'SetUID '
                                                                                                                       'flag',
                                                                                                        'type': 'path'}},
                                                                 'name': 'Set '
                                                                         'a '
                                                                         'SetUID '
                                                                         'flag '
                                                                         'on '
                                                                         'file',
                                                                 'supported_platforms': ['macos',
                                                                                         'linux']},
                                                                {'auto_generated_guid': 'db55f666-7cba-46c6-9fe6-205a05c3242c',
                                                                 'description': 'This '
                                                                                'test '
                                                                                'sets '
                                                                                'the '
                                                                                'SetGID '
                                                                                'flag '
                                                                                'on '
                                                                                'a '
                                                                                'file '
                                                                                'in '
                                                                                'Linux '
                                                                                'and '
                                                                                'macOS.\n',
                                                                 'executor': {'cleanup_command': 'sudo '
                                                                                                 'rm '
                                                                                                 '#{file_to_setuid}\n',
                                                                              'command': 'sudo '
                                                                                         'touch '
                                                                                         '#{file_to_setuid}\n'
                                                                                         'sudo '
                                                                                         'chown '
                                                                                         'root '
                                                                                         '#{file_to_setuid}\n'
                                                                                         'sudo '
                                                                                         'chmod '
                                                                                         'g+s '
                                                                                         '#{file_to_setuid}\n',
                                                                              'elevation_required': True,
                                                                              'name': 'sh'},
                                                                 'input_arguments': {'file_to_setuid': {'default': '/tmp/evilBinary',
                                                                                                        'description': 'Path '
                                                                                                                       'of '
                                                                                                                       'file '
                                                                                                                       'to '
                                                                                                                       'set '
                                                                                                                       'SetGID '
                                                                                                                       'flag',
                                                                                                        'type': 'path'}},
                                                                 'name': 'Set '
                                                                         'a '
                                                                         'SetGID '
                                                                         'flag '
                                                                         'on '
                                                                         'file',
                                                                 'supported_platforms': ['macos',
                                                                                         'linux']}],
                                               'attack_technique': 'T1166',
                                               'display_name': 'Setuid and '
                                                               'Setgid'}}]
```

# Tactics


* [Persistence](../tactics/Persistence.md)

* [Privilege Escalation](../tactics/Privilege-Escalation.md)
    

# Mitigations

None

# Actors

None
