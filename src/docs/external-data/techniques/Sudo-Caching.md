
# Sudo Caching

## Description

### MITRE Description

> The <code>sudo</code> command "allows a system administrator to delegate authority to give certain users (or groups of users) the ability to run some (or all) commands as root or another user while providing an audit trail of the commands and their arguments." (Citation: sudo man page 2018) Since sudo was made for the system administrator, it has some useful configuration features such as a <code>timestamp_timeout</code> that is the amount of time in minutes between instances of <code>sudo</code> before it will re-prompt for a password. This is because <code>sudo</code> has the ability to cache credentials for a period of time. Sudo creates (or touches) a file at <code>/var/db/sudo</code> with a timestamp of when sudo was last run to determine this timeout. Additionally, there is a <code>tty_tickets</code> variable that treats each new tty (terminal session) in isolation. This means that, for example, the sudo timeout of one tty will not affect another tty (you will have to type the password again).

Adversaries can abuse poor configurations of this to escalate privileges without needing the user's password. <code>/var/db/sudo</code>'s timestamp can be monitored to see if it falls within the <code>timestamp_timeout</code> range. If it does, then malware can execute sudo commands without needing to supply the user's password. When <code>tty_tickets</code> is disabled, adversaries can do this from any tty for that user. 

The OSX Proton Malware has disabled <code>tty_tickets</code> to potentially make scripting easier by issuing <code>echo \'Defaults !tty_tickets\' >> /etc/sudoers</code>  (Citation: cybereason osx proton). In order for this change to be reflected, the Proton malware also must issue <code>killall Terminal</code>. As of macOS Sierra, the sudoers file has <code>tty_tickets</code> enabled by default.

## Additional Attributes

* Bypass: None
* Effective Permissions: ['root']
* Network: intentionally left blank
* Permissions: ['User']
* Platforms: ['Linux', 'macOS']
* Remote: intentionally left blank
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1206

## Potential Commands

```
sudo sed -i 's/env_reset.*$/env_reset,timestamp_timeout=-1/' /etc/sudoers
sudo visudo -c -f /etc/sudoers

sudo sh -c "echo Defaults "'!'"tty_tickets >> /etc/sudoers"
sudo visudo -c -f /etc/sudoers

sudo sed -i 's/env_reset.*$/env_reset,timestamp_timeout=-1/' /etc/sudoers
sudo sh -c "echo Defaults "'!'"tty_tickets >> /etc/sudoers"
```

## Commands Dataset

```
[{'command': "sudo sed -i 's/env_reset.*$/env_reset,timestamp_timeout=-1/' "
             '/etc/sudoers\n'
             'sudo visudo -c -f /etc/sudoers\n',
  'name': None,
  'source': 'atomics/T1206/T1206.yaml'},
 {'command': 'sudo sh -c "echo Defaults "\'!\'"tty_tickets >> /etc/sudoers"\n'
             'sudo visudo -c -f /etc/sudoers\n',
  'name': None,
  'source': 'atomics/T1206/T1206.yaml'},
 {'command': "sudo sed -i 's/env_reset.*$/env_reset,timestamp_timeout=-1/' "
             '/etc/sudoers',
  'name': None,
  'source': 'Kirtar22/Litmus_Test'},
 {'command': 'sudo sh -c "echo Defaults "\'!\'"tty_tickets >> /etc/sudoers"',
  'name': None,
  'source': 'Kirtar22/Litmus_Test'}]
```

## Potential Detections

```json
[{'data_source': 'auditlogs (audit.rules)'},
 {'data_source': 'bash_history logs'}]
```

## Potential Queries

```json
[{'name': None,
  'product': 'Splunk',
  'query': 'index=linux sourcetype="linux_audit" sudoers_change'},
 {'name': None,
  'product': 'Splunk',
  'query': 'Audit Rule : -w /etc/sudoers -p wa -k sudoers_change'}]
```

## Raw Dataset

```json
[{'Atomic Red Team Test - Sudo Caching': {'atomic_tests': [{'description': 'Sets '
                                                                           'sudo '
                                                                           'caching '
                                                                           'timestamp_timeout '
                                                                           'to '
                                                                           'a '
                                                                           'value '
                                                                           'for '
                                                                           'unlimited. '
                                                                           'This '
                                                                           'is '
                                                                           'dangerous '
                                                                           'to '
                                                                           'modify '
                                                                           'without '
                                                                           'using '
                                                                           "'visudo', "
                                                                           'do '
                                                                           'not '
                                                                           'do '
                                                                           'this '
                                                                           'on '
                                                                           'a '
                                                                           'production '
                                                                           'system.\n',
                                                            'executor': {'command': 'sudo '
                                                                                    'sed '
                                                                                    '-i '
                                                                                    "'s/env_reset.*$/env_reset,timestamp_timeout=-1/' "
                                                                                    '/etc/sudoers\n'
                                                                                    'sudo '
                                                                                    'visudo '
                                                                                    '-c '
                                                                                    '-f '
                                                                                    '/etc/sudoers\n',
                                                                         'name': 'sh'},
                                                            'name': 'Unlimited '
                                                                    'sudo '
                                                                    'cache '
                                                                    'timeout',
                                                            'supported_platforms': ['macos',
                                                                                    'linux']},
                                                           {'description': 'Sets '
                                                                           'sudo '
                                                                           'caching '
                                                                           'tty_tickets '
                                                                           'value '
                                                                           'to '
                                                                           'disabled. '
                                                                           'This '
                                                                           'is '
                                                                           'dangerous '
                                                                           'to '
                                                                           'modify '
                                                                           'without '
                                                                           'using '
                                                                           "'visudo', "
                                                                           'do '
                                                                           'not '
                                                                           'do '
                                                                           'this '
                                                                           'on '
                                                                           'a '
                                                                           'production '
                                                                           'system.\n',
                                                            'executor': {'command': 'sudo '
                                                                                    'sh '
                                                                                    '-c '
                                                                                    '"echo '
                                                                                    'Defaults '
                                                                                    '"\'!\'"tty_tickets '
                                                                                    '>> '
                                                                                    '/etc/sudoers"\n'
                                                                                    'sudo '
                                                                                    'visudo '
                                                                                    '-c '
                                                                                    '-f '
                                                                                    '/etc/sudoers\n',
                                                                         'name': 'sh'},
                                                            'name': 'Disable '
                                                                    'tty_tickets '
                                                                    'for sudo '
                                                                    'caching',
                                                            'supported_platforms': ['macos',
                                                                                    'linux']}],
                                          'attack_technique': 'T1206',
                                          'display_name': 'Sudo Caching'}}]
```

# Tactics


* [Privilege Escalation](../tactics/Privilege-Escalation.md)


# Mitigations

None

# Actors

None
