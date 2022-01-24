# xkb-mathy

A US QUERTY math keyboard layout for Xkeyboard.

This keyboard is intended for programming with unicode characters. It is not a replacement for LaTex

xkb-mathy mostly intended for typing math characters in a plain-text setting (e.g. programming with unicode operators). It's *not* a replacement for LaTeX. To reach its maximum potential. There are no dead keys on this keyboard.                                       

## Layout Changes:

The layout is your typical four level keyboard. By default holding AltGr (the right Alt key), the keys are 'shifted' to Level 3. Holding AltGr and Shift brings the keys Level 4. 

The true power of this requires use of the "Compose Key". This, coupled with my hatred of Caps Lock, compelled me to replace Caps Lock with Compose. Further down this file ~~are~~ will be suggested configuration change if you happen to hate this or any other default.

// TODO: Create a visual of the layout. Keybindings can be seen in code comments. 

The layout is a heavy modification of the standard Greek layout (which mercifully is already organized to be similar to QUERTY). All punctuation keys, number keys, and arrow keys are replaced at Levels 3 and 4. Rough explanation of significant changes:

- ∂ and ∇ are on the Q key. On the Greek layout, this is the colon and semicolon keys.
- Greek Capital Letters which appear identical to their Latin counterparts are replaced alternate letterforms that hopefully make sense (e.g. A becomes ∀, R becomes ℝ, H becomes ℏ).
- the o and O key is now the 'circles' key, ∘ and ○.
- Pressing an Arrow key at Level 3 produces an arrow character → ↑ ← ↓, and Level 4 ⇒ ⇑ ⇐ ⇓
 
The Compose Key carries with it many useful defaults. For this reason, I've eschewed placing some very popular keys if they are extremely easly to blindly guess with the Compose key. For example, in this layout the ≠ key is only accessible via Compose(=/) and ÷ is accessible from Compose(-:).

## Current version:

I literally *just* made this, so I'm definitely going to shuffle things around. 

## Install Instructions:

1. Find the directory on your system which contains xkb. Possible locations include: 
  - /etc/X11/xkb
  - /usr/share/X11/xkb

\[My limited understanding of xkb is that... \] Configuring the keyboard *requires* updating the files outside of your home directory. **Please make backups of every file you edit, such that you revert back easily if something goes awry.**

2. Copy the contents of *us_mathy* and paste it to the bottom of your **xkb/symbols/us** file. 

3. In your **xkb/rules/evdev.lst** file, in the *! variant* section, add the following line: 

```
mathy   us: English (US Mathy)
```

4. In your **xkb/rules/evdev.xml** file, in the \<layoutList\> section, find the \<layout\> whose \<configItem\> \<name\> is "us". Then add the following code to the \<layout\>'s \<variantList\>:
```
<variant>
  <configItem>
    <name>mathy</name>
    <description>English (US Mathy)</description>
   </configItem>
</variant>
```

5. xkb needs to be reconfigured for it to recognize your changes. In a terminal shell run the following command:

```
sudo dpkg-reconfigure xkb-data
```

Failing this, restarting your X-session on your system should suffice. 

## To do:

1. Properly package this code for easy install
2. Iterate upon key placement. 
3. Variants upon this: 
  - Preferring "Math" characters vs "Greek" characters (e.g. ∑ vs Σ). Aesthetically I prefer the latter for plain text, as the characters are more likely to be rendered more consistently, but the unicode semantics underneath beg for the former. Maybe use Compose to get the math/big versions of characters?
  - To many, the numpad is useless. These keys could be reworked to be a huge 'Arrow' pad. 
4. The Compose Key is good, but could be much more powerful. The Compose key is largely focused on combining ASCII keys to create symbols, especially for adding diacritics to characters. On browsing various unicode blocks, most of the math characters are diacritics upon some root symbol (e.g. ⊆, which can currently be composed with ⊂ and \_). Would love to rework it with a wholly redone set of custom mappings.
5. Some kind of hotkey combination to change letter variants? There are 10 different character sets for 'math' variants of characters in Unicode. The most common such characters (e.g. ℤ, ℝ, ℬ) have been separated into their own block. It'd be fun to have a hotkey combination to swap among the various forms. 
6. Probably lots of other stuff. 
