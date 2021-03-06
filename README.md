This forked repo of https://github.com/nostrademons/keycode.js adapts
Keycode.js to an AMD module.

-----

This is a library for normalizing JavaScript key codes across browsers.  It's based on the article "JavaScript Madness: Keyboard Events" by Jan Wolter:

http://unixpapa.com/js/key.html

The normalized keycodes it generates obey the following rules:

- For alphabetic characters, the ASCII code of the uppercase version
- For codes that are identical across all browsers (this includes all modifiers, esc, delete, arrows, etc.), the common keycode
- For numeric keypad keys, the value returned by numkey(). (Usually 96 + the number)
- For symbols, the ASCII code of the character that appears when shift is not held down, EXCEPT for '" => 222 (conflicts with right-arrow/pagedown), .> => 190 (conflicts with Delete) and `~ => 126 (conflicts with Num0).

This library works with key objects, which are { Int code, bool shift, bool alt, bool ctrl } JavaScript objects that record the key code along with any modifiers pressed.  translate_event() returns one of these; hot_key() takes one of these and returns a string suitable for the JQuery HotKey plugin or Binny V A's shortcut.js library.

So far, I've tested it on:

- Firefox 2.0.0.12 for Linux
- Konqueror 3.5.8 for Linux
- Opera 10 for Linux
- Firefox 2.0.0.16 for Windows
- Firefox 3.0.3 for Windows
- Google Chrome 0.2.149.30 for Windows
- IE 6.0 for Windows
- IE 7.0 for Windows
- Opera 9.5.1 for Windows
- Safari 3.0 for Windows

Known bugs include:

- There's no way to generate a keycode for the PrintScreen key: most browsers don't even fire a keyboard event for it.
- Safari/Windows does not fire keydown events for modifier keys (shift/ctrl/alt/capslock)
- Num- comes out as _ on Firefox, and Num+ appears as = (those are the unshifted keys of -/+, respectively).  There's no way to avoid this; the keycodes are exactly identical.  Similarly, all the keypad arithmetic keys act like their non-keypad equivalents on Konqueror/Opera 8.5, since the keycodes don't distinguish between them.

Patches are welcome; that's what GitHub is for.
