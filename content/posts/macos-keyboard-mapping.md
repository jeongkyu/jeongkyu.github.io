---
title: "macOS 한/영 변환키 매핑"
date: 2023-09-24T02:22:37+09:00
draft: true 
---

1. 키보드 매핑

- Input Source Shortcut 에서 F13 지정 후

- Internal Keyboard: right command -> F13
- RealForce Keyboard:
    - right option → F13
    - left command → left option
    - left option → left command

https://hidutil-generator.netlify.app


2. hidutil을 시작 프로그램(Launch Agent)으로 등록

```

jeongkyu@Jeongkyus-MacBook-Pro ~ % cat ~/Library/LaunchAgents/com.local.KeyRemapping.Internal.plist 
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.local.Internal.KeyRemapping</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/bin/hidutil</string>
        <string>property</string>
	<string>--matching</string>
	<string>{"ProductID":0x027c}</string>
        <string>--set</string>
        <string>{"UserKeyMapping":[
            {
              "HIDKeyboardModifierMappingSrc": 0x7000000E7,
              "HIDKeyboardModifierMappingDst": 0x700000068
            }
        ]}</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <true />
</dict>
</plist>


jeongkyu@Jeongkyus-MacBook-Pro ~ % cat ~/Library/LaunchAgents/com.local.KeyRemapping.RealForce.plist 
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.local.RealForce.KeyRemapping</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/bin/hidutil</string>
        <string>property</string>
	<string>--matching</string>
	<string>{"ProductID":0x0145}</string>
        <string>--set</string>
        <string>{"UserKeyMapping":[
            {
              "HIDKeyboardModifierMappingSrc": 0x7000000E6,
              "HIDKeyboardModifierMappingDst": 0x700000068
            },
            {
              "HIDKeyboardModifierMappingSrc": 0x7000000E2,
              "HIDKeyboardModifierMappingDst": 0x7000000E3
            },
            {
              "HIDKeyboardModifierMappingSrc": 0x7000000E3,
              "HIDKeyboardModifierMappingDst": 0x7000000E2
            }
        ]}</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>KeepAlive</key>
    <true />
</dict>
</plist>
```