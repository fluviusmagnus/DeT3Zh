# DeT3Zh - German keyboard layout optimized for Simplified Chinese keyboard

## Why?

Typical Chinese keyboards lack the `<` key between LShift and Y, which appears commonly on European keyboards. As a result, Germanists in China have to keep switching frequently from one keyboard layout to another. Therefore, I tried to create a special modified German keyboard layout for those who are using a Chinese keyboard. All the modification works fine on my Manjaro machine, and should work also on Archlinux or other Linux systems.

## What has been changed?

This customized keyboard layout is modified on the basis of T3 (Tastaturbelegung 3, „Expertentastatur“), which is the most powerful and also compatible with T1 and T2. For more information about German keyboard please see [Tastaturbelegung](https://de.wikipedia.org/wiki/Tastaturbelegung#Deutschland_und_.C3.96sterreich) on Wikipedia or [Karl Pentzlin: Vorschlag zur Erweiterung der deutschen PC-Standardtastatur (PDF; 1,2 MB)](http://www.pentzlin.com/ErweiterungDeutscheTastatur2.pdf). There are also illustrations showing the position of each key in both links.

My modification is simple. Group 1 i.e. `< > |` on the `<` key is moved to Group 2 of key `ß`, and Group 2 i.e. `ŉ ¦ ♪` on it is moved to Group 2 of key `+`. This should be safe because the overwritten groups are actually duplicate.

## How to use?

For Manjaro or Archlinux, place the layout file `de_zhkb` into `/usr/share/X11/xkb/symbols/`. And then modify `base.lst`, `evdev.lst` and `evdev.xml` in `/usr/share/X11/xkb/rules/`. This won't be difficult as these files are quite self-explanatory. After a reboot the German (T3 Modified for ZhKB) layout should appear on the list of a selector.

__Honestly speaking, I do not know very well how to deal with these files. So please tell me if there is anything wrong.__
