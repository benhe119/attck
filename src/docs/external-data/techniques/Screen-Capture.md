
# Screen Capture

## Description

### MITRE Description

> Adversaries may attempt to take screen captures of the desktop to gather information over the course of an operation. Screen capturing functionality may be included as a feature of a remote access tool used in post-compromise operations.

### Mac

On OSX, the native command <code>screencapture</code> is used to capture screenshots.

### Linux

On Linux, there is the native command <code>xwd</code>. (Citation: Antiquated Mac Malware)

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: None
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1113

## Potential Commands

```
screencapture /tmp/T1113_desktop.png

screencapture -x /tmp/T1113_desktop.png

xwd -root -out /tmp/T1113_desktop.xwd
xwud -in /tmp/T1113_desktop.xwd

import -window root /tmp/T1113_desktop.png

{'darwin': {'sh': {'command': 'for i in {1..5}; do screencapture -t png screen-$i.png; echo "$(cd "$(dirname "$1")"; pwd -P)/$(basename "screen-$i.png")"; sleep 5; done;\n'}}, 'windows': {'psh,pwsh': {'command': '[Reflection.Assembly]::LoadWithPartialName("System.Drawing");\nfunction screenshot([Drawing.Rectangle]$bounds, $path) {\n   $bmp = New-Object Drawing.Bitmap $bounds.width, $bounds.height;\n   $graphics = [Drawing.Graphics]::FromImage($bmp);\n   $graphics.CopyFromScreen($bounds.Location, [Drawing.Point]::Empty, $bounds.size);\n   $bmp.Save($path);\n   $graphics.Dispose();\n   $bmp.Dispose();\n}\n$bounds = [Drawing.Rectangle]::FromLTRB(0, 0, 1000, 900);\nscreenshot $bounds "$HOME\\Desktop\\screenshot.png";\n'}}}
powershell/collection/screenshot
powershell/collection/screenshot
python/collection/osx/native_screenshot
python/collection/osx/native_screenshot
python/collection/osx/native_screenshot_mss
python/collection/osx/native_screenshot_mss
python/collection/osx/screenshot
python/collection/osx/screenshot
```

## Commands Dataset

```
[{'command': 'screencapture /tmp/T1113_desktop.png\n',
  'name': None,
  'source': 'atomics/T1113/T1113.yaml'},
 {'command': 'screencapture -x /tmp/T1113_desktop.png\n',
  'name': None,
  'source': 'atomics/T1113/T1113.yaml'},
 {'command': 'xwd -root -out /tmp/T1113_desktop.xwd\n'
             'xwud -in /tmp/T1113_desktop.xwd\n',
  'name': None,
  'source': 'atomics/T1113/T1113.yaml'},
 {'command': 'import -window root /tmp/T1113_desktop.png\n',
  'name': None,
  'source': 'atomics/T1113/T1113.yaml'},
 {'command': {'darwin': {'sh': {'command': 'for i in {1..5}; do screencapture '
                                           '-t png screen-$i.png; echo "$(cd '
                                           '"$(dirname "$1")"; pwd '
                                           '-P)/$(basename "screen-$i.png")"; '
                                           'sleep 5; done;\n'}},
              'windows': {'psh,pwsh': {'command': '[Reflection.Assembly]::LoadWithPartialName("System.Drawing");\n'
                                                  'function '
                                                  'screenshot([Drawing.Rectangle]$bounds, '
                                                  '$path) {\n'
                                                  '   $bmp = New-Object '
                                                  'Drawing.Bitmap '
                                                  '$bounds.width, '
                                                  '$bounds.height;\n'
                                                  '   $graphics = '
                                                  '[Drawing.Graphics]::FromImage($bmp);\n'
                                                  '   '
                                                  '$graphics.CopyFromScreen($bounds.Location, '
                                                  '[Drawing.Point]::Empty, '
                                                  '$bounds.size);\n'
                                                  '   $bmp.Save($path);\n'
                                                  '   $graphics.Dispose();\n'
                                                  '   $bmp.Dispose();\n'
                                                  '}\n'
                                                  '$bounds = '
                                                  '[Drawing.Rectangle]::FromLTRB(0, '
                                                  '0, 1000, 900);\n'
                                                  'screenshot $bounds '
                                                  '"$HOME\\Desktop\\screenshot.png";\n'}}},
  'name': 'capture the contents of the screen',
  'source': 'data/abilities/collection/316251ed-6a28-4013-812b-ddf5b5b007f8.yml'},
 {'command': 'powershell/collection/screenshot',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'powershell/collection/screenshot',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'python/collection/osx/native_screenshot',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'python/collection/osx/native_screenshot',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'python/collection/osx/native_screenshot_mss',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'python/collection/osx/native_screenshot_mss',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'python/collection/osx/screenshot',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'python/collection/osx/screenshot',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'}]
```

## Potential Detections

```json
[{'data_source': ['4688', 'Process Execution']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['API monitoring']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['API monitoring']}]
```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Screen Capture': {'atomic_tests': [{'auto_generated_guid': '0f47ceb1-720f-4275-96b8-21f0562217ac',
                                                              'description': 'Use '
                                                                             'screencapture '
                                                                             'command '
                                                                             'to '
                                                                             'collect '
                                                                             'a '
                                                                             'full '
                                                                             'desktop '
                                                                             'screenshot\n',
                                                              'executor': {'cleanup_command': 'rm '
                                                                                              '#{output_file}\n',
                                                                           'command': 'screencapture '
                                                                                      '#{output_file}\n',
                                                                           'elevation_required': False,
                                                                           'name': 'bash'},
                                                              'input_arguments': {'output_file': {'default': '/tmp/T1113_desktop.png',
                                                                                                  'description': 'Output '
                                                                                                                 'file '
                                                                                                                 'path',
                                                                                                  'type': 'Path'}},
                                                              'name': 'Screencapture',
                                                              'supported_platforms': ['macos']},
                                                             {'auto_generated_guid': 'deb7d358-5fbd-4dc4-aecc-ee0054d2d9a4',
                                                              'description': 'Use '
                                                                             'screencapture '
                                                                             'command '
                                                                             'to '
                                                                             'collect '
                                                                             'a '
                                                                             'full '
                                                                             'desktop '
                                                                             'screenshot\n',
                                                              'executor': {'cleanup_command': 'rm '
                                                                                              '#{output_file}\n',
                                                                           'command': 'screencapture '
                                                                                      '-x '
                                                                                      '#{output_file}\n',
                                                                           'elevation_required': False,
                                                                           'name': 'bash'},
                                                              'input_arguments': {'output_file': {'default': '/tmp/T1113_desktop.png',
                                                                                                  'description': 'Output '
                                                                                                                 'file '
                                                                                                                 'path',
                                                                                                  'type': 'Path'}},
                                                              'name': 'Screencapture '
                                                                      '(silent)',
                                                              'supported_platforms': ['macos']},
                                                             {'auto_generated_guid': '8206dd0c-faf6-4d74-ba13-7fbe13dce6ac',
                                                              'description': 'Use '
                                                                             'xwd '
                                                                             'command '
                                                                             'to '
                                                                             'collect '
                                                                             'a '
                                                                             'full '
                                                                             'desktop '
                                                                             'screenshot '
                                                                             'and '
                                                                             'review '
                                                                             'file '
                                                                             'with '
                                                                             'xwud\n',
                                                              'executor': {'cleanup_command': 'rm '
                                                                                              '#{output_file}\n',
                                                                           'command': 'xwd '
                                                                                      '-root '
                                                                                      '-out '
                                                                                      '#{output_file}\n'
                                                                                      'xwud '
                                                                                      '-in '
                                                                                      '#{output_file}\n',
                                                                           'name': 'bash'},
                                                              'input_arguments': {'output_file': {'default': '/tmp/T1113_desktop.xwd',
                                                                                                  'description': 'Output '
                                                                                                                 'file '
                                                                                                                 'path',
                                                                                                  'type': 'Path'}},
                                                              'name': 'X '
                                                                      'Windows '
                                                                      'Capture',
                                                              'supported_platforms': ['linux']},
                                                             {'auto_generated_guid': '9cd1cccb-91e4-4550-9139-e20a586fcea1',
                                                              'description': 'Use '
                                                                             'import '
                                                                             'command '
                                                                             'to '
                                                                             'collect '
                                                                             'a '
                                                                             'full '
                                                                             'desktop '
                                                                             'screenshot\n',
                                                              'executor': {'cleanup_command': 'rm '
                                                                                              '#{output_file}\n',
                                                                           'command': 'import '
                                                                                      '-window '
                                                                                      'root '
                                                                                      '#{output_file}\n',
                                                                           'name': 'bash'},
                                                              'input_arguments': {'output_file': {'default': '/tmp/T1113_desktop.png',
                                                                                                  'description': 'Output '
                                                                                                                 'file '
                                                                                                                 'path',
                                                                                                  'type': 'Path'}},
                                                              'name': 'Import',
                                                              'supported_platforms': ['linux']}],
                                            'attack_technique': 'T1113',
                                            'display_name': 'Screen Capture'}},
 {'Mitre Stockpile - capture the contents of the screen': {'description': 'capture '
                                                                          'the '
                                                                          'contents '
                                                                          'of '
                                                                          'the '
                                                                          'screen',
                                                           'id': '316251ed-6a28-4013-812b-ddf5b5b007f8',
                                                           'name': 'Screen '
                                                                   'Capture',
                                                           'platforms': {'darwin': {'sh': {'command': 'for '
                                                                                                      'i '
                                                                                                      'in '
                                                                                                      '{1..5}; '
                                                                                                      'do '
                                                                                                      'screencapture '
                                                                                                      '-t '
                                                                                                      'png '
                                                                                                      'screen-$i.png; '
                                                                                                      'echo '
                                                                                                      '"$(cd '
                                                                                                      '"$(dirname '
                                                                                                      '"$1")"; '
                                                                                                      'pwd '
                                                                                                      '-P)/$(basename '
                                                                                                      '"screen-$i.png")"; '
                                                                                                      'sleep '
                                                                                                      '5; '
                                                                                                      'done;\n'}},
                                                                         'windows': {'psh,pwsh': {'command': '[Reflection.Assembly]::LoadWithPartialName("System.Drawing");\n'
                                                                                                             'function '
                                                                                                             'screenshot([Drawing.Rectangle]$bounds, '
                                                                                                             '$path) '
                                                                                                             '{\n'
                                                                                                             '   '
                                                                                                             '$bmp '
                                                                                                             '= '
                                                                                                             'New-Object '
                                                                                                             'Drawing.Bitmap '
                                                                                                             '$bounds.width, '
                                                                                                             '$bounds.height;\n'
                                                                                                             '   '
                                                                                                             '$graphics '
                                                                                                             '= '
                                                                                                             '[Drawing.Graphics]::FromImage($bmp);\n'
                                                                                                             '   '
                                                                                                             '$graphics.CopyFromScreen($bounds.Location, '
                                                                                                             '[Drawing.Point]::Empty, '
                                                                                                             '$bounds.size);\n'
                                                                                                             '   '
                                                                                                             '$bmp.Save($path);\n'
                                                                                                             '   '
                                                                                                             '$graphics.Dispose();\n'
                                                                                                             '   '
                                                                                                             '$bmp.Dispose();\n'
                                                                                                             '}\n'
                                                                                                             '$bounds '
                                                                                                             '= '
                                                                                                             '[Drawing.Rectangle]::FromLTRB(0, '
                                                                                                             '0, '
                                                                                                             '1000, '
                                                                                                             '900);\n'
                                                                                                             'screenshot '
                                                                                                             '$bounds '
                                                                                                             '"$HOME\\Desktop\\screenshot.png";\n'}}},
                                                           'tactic': 'collection',
                                                           'technique': {'attack_id': 'T1113',
                                                                         'name': 'Screen '
                                                                                 'Capture'}}},
 {'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1113',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"powershell/collection/screenshot":  '
                                                                                 '["T1113"],',
                                            'Empire Module': 'powershell/collection/screenshot',
                                            'Technique': 'Screen Capture'}},
 {'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1113',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"python/collection/osx/native_screenshot":  '
                                                                                 '["T1113"],',
                                            'Empire Module': 'python/collection/osx/native_screenshot',
                                            'Technique': 'Screen Capture'}},
 {'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1113',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"python/collection/osx/native_screenshot_mss":  '
                                                                                 '["T1113"],',
                                            'Empire Module': 'python/collection/osx/native_screenshot_mss',
                                            'Technique': 'Screen Capture'}},
 {'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1113',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"python/collection/osx/screenshot":  '
                                                                                 '["T1113"],',
                                            'Empire Module': 'python/collection/osx/screenshot',
                                            'Technique': 'Screen Capture'}}]
```

# Tactics


* [Collection](../tactics/Collection.md)


# Mitigations

None

# Actors


* [OilRig](../actors/OilRig.md)

* [APT28](../actors/APT28.md)
    
* [Group5](../actors/Group5.md)
    
* [BRONZE BUTLER](../actors/BRONZE-BUTLER.md)
    
* [MuddyWater](../actors/MuddyWater.md)
    
* [Dragonfly 2.0](../actors/Dragonfly-2.0.md)
    
* [Dark Caracal](../actors/Dark-Caracal.md)
    
* [FIN7](../actors/FIN7.md)
    
* [Magic Hound](../actors/Magic-Hound.md)
    
* [Silence](../actors/Silence.md)
    
