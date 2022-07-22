# xkb-us-mathy

A US QUERTY keyboard layout for Xkeyboard, intended for quickly typing mathematical symbols in plain-text settings, such as message boards or programming with unicode operators.                                        

## Layout Changes:

The layout is a modification of the standard Greek keyboard, replacing punctuation and look-alike Greek characters with somewhat-sensible replacements. You can access the new keys by holding the Level 3 Modifier key, and additional keys via the Compose key (Ref: https://en.wikipedia.org/wiki/Compose_key). This layout also changes how CapsLock functions. 

### Modifier Key Changes:

- The Level 3 shift key (henceforth referred to as "AltGr") are mapped to the *Right Alt* and *Caps Lock* keys.
- Holding *Shift* and *AltGr* brings up Level 4 keys
- Caps Lock can be toggled by pressing both *Shift* keys at the same time. 
- The Compose key is mapped to the *Right Super* key (option in source for *Right Ctrl*)

### Layout:

![Visual of keyboard layout](/xkb_us_mathy_layout.png)

#### Notes: 

- Vague, handwavey explanations for questionable keybinding choices are found in the source code.
- The standard Greek keyboard layout is modeled after QUERTY, so you can often reasonably guess the character location.
- ∂ and ∇ are on the Q key. On the Greek layout, this is the colon/semicolon key.
- All Greek characters are their "Greek" versions (e.g. "Σ"), and not their "Math" versions. (e.g. "∑").
- Hebrew letters ℵ and ℶ are their "math" versions, so they won't reverse your text.
- Pressing an Arrow key at Level 3 produces an arrow character → ↑ ← ↓, and Level 4 ⇒ ⇑ ⇐ ⇓
- Some popular characters are absent, such as ≠ and ÷, as they can sensibly be created via the Compose key: (e.g. Compose(=/) → ≠, and Compose(-:) → ÷)
- Notable new lookalike keys: 
  - "AltGr"+"3" → Greek epsilon "ϵ", whereas "AltGr"+"=" → Element-of "∈"
  - "AltGr"+"Shift"+"L" → Capital lambda "Λ", whereas "AltGr"+";" → Logican And "∧"

## Current version:

Version 0.0.2 -- lots of changes.

## Install Instructions:

### Install as root:

**Please make backups of every file you edit. Misconfigured xkb rules can be troublesome to resolve. I am not responsible for your system.**

1. Find the directory on your system which contains xkb. Possible locations include: 

- /etc/X11/xkb
- /usr/share/X11/xkb

2. Append the contents of the *us_mathy* file to your *xkb/symbols/us* file

```
sudo echo us_mathy >> **path/to/**xkb/symbols/us
```

3. In your *xkb/rules/evdev.lst* file, under the `! variant` section, add the following line: 

```
mathy   us: English (US Mathy)
```

4. In your *xkb/rules/evdev.xml* file, in the `<layoutList>` section, find the `<layout>` whose `<configItem>` `<name>` is "us". Then add the following code to the `<layout>`'s `<variantList>`:
```
<variant>
  <configItem>
    <name>mathy</name>
    <shortDescription>mathy</shortDescription>
    <description>English (US Mathy)</description>
    <languageList>
      <iso639Id>eng</iso639Id>
    </languageList>
  </configItem>
</variant>
```

5. xkb needs to be reconfigured for it to recognize your changes. In a terminal shell run the following command:

```
sudo dpkg-reconfigure xkb-data
```

If this doesn't work, you can log-out/log-in or restart your X-session.

6. Activate the keyboard layout in your system settings, or by whatever means you prefer. 

### Install as user:

See: **TODO**

## TODO:

* Better installation method.
* Instructions for user install.
* Change a few of the poorer keybindings I regret to have made
* Variant to default to Math versions of Greek letters
* Extend Compose Key characters. Obvious things like:
  - Compose(ΣΣ) → ∑
  - Compose(h-) → ℏ
* Add Levels 3 and 4 to the Numpad. More Arrows? Box-drawing characters?
* I don't have that extra key between "Left Shift" and "Z", so it went unmodified. Could put something fun there.
* Probably lots of other stuff. 
