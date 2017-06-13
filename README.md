# DeT3Zh - German keyboard layout optimized for Simplified Chinese keyboard

## Why?

Typical Chinese keyboards lack the `<` key between LShift and Y, which appears commonly on European keyboards. As a result, Germanists in China have to keep switching frequently from one keyboard layout to another. Therefore, I tried to create a special modified German keyboard layout for those who are using a Chinese keyboard. All the modification works fine on my Manjaro machine, and should work also on Archlinux or other Linux systems.

## What has been changed?

This customized keyboard layout is modified on the basis of T3 (Tastaturbelegung 3, „Expertentastatur“), which is the most powerful and also compatible with T1 and T2. For more information about German keyboard please see [Tastaturbelegung](https://de.wikipedia.org/wiki/Tastaturbelegung#Deutschland_und_.C3.96sterreich) on Wikipedia or [Karl Pentzlin: Vorschlag zur Erweiterung der deutschen PC-Standardtastatur (PDF; 1,2 MB)](http://www.pentzlin.com/ErweiterungDeutscheTastatur2.pdf). There are also illustrations showing the position of each key in both links.

My modification is simple. Group 1 i.e. `< > |` on the `<` key is moved to Group 2 of key `ß`, and Group 2 i.e. `ŉ ¦ ♪` on it is moved to Group 2 of key `+`. This should be safe because the overwritten groups are actually duplicate.

## How to use?

~~For Manjaro or Archlinux, place the layout file `de_zhkb` into `/usr/share/X11/xkb/symbols/`. And then modify `base.lst`, `evdev.lst` and `evdev.xml` in `/usr/share/X11/xkb/rules/`. This won't be difficult as these files are quite self-explanatory. After a reboot the German (T3 Modified for ZhKB) layout should appear on the list of a selector.~~ This is not the best way to configure. Just ignore it.

1. Add these lines after `/usr/share/X11/xkb/symbols/de`:

   ```
   partial alphanumeric_keys
   xkb_symbols "de_zhkb" {
       name[Group1]="German (Chinese keyboard)";

       // Keyboard for Simplified Chinese lacks the key between Left_Shift and Y,
       // so Group 1 on it is moved to Group 2 of key AE11,
       // and Group 2 on it is moved to Group 2 of key AD12.
       // This is safe because the overwritten groups are actually duplicate. 

       include "de(T3)"

       // key <AE11> { [          ssharp,        question,       backslash,        NoSymbol,       backslash,      questiondown,           U02BB,        NoSymbol ] };
       key <AE11> { [          ssharp,        question,       backslash,        NoSymbol,            less,           greater,             bar,        NoSymbol ] };

       // key <AD12> { [            plus,        asterisk,      asciitilde,        NoSymbol,      dead_tilde,     dead_macron,              at,        NoSymbol ] };
       key <AD12> { [            plus,        asterisk,      asciitilde,        NoSymbol,           U0149,       brokenbar,           U266A,        NoSymbol ] };

   };
   ```

2. Add lines to a specific place in `/usr/share/X11/xkb/rules/base.extra.xml`:

   Find lines in this file like:

   ```
       <layout>
         <configItem>
           <name>de</name>
           <shortDescription>de</shortDescription>
           <description>German</description>
           <languageList>
             <iso639Id>ger</iso639Id>
           </languageList>
         </configItem>
         <variantList>
   ```

   Add these after them:

   ```
           <variant>
             <configItem>
               <name>de_zhkb</name>
               <description>German (Chinese keyboard)</description>
             </configItem>
           </variant>
   ```

3. Add lines to a specific place in `/usr/share/X11/xkb/rules/evdev.extra.xml`:

   Find lines in this file like:

   ```
       <layout>
         <configItem>
           <name>de</name>
           <shortDescription>de</shortDescription>
           <description>German</description>
           <languageList>
             <iso639Id>ger</iso639Id>
           </languageList>
         </configItem>
         <variantList>
   ```

   Add these after them:

   ```
           <variant>
             <configItem>
               <name>de_zhkb</name>
               <description>German (Chinese keyboard)</description>
             </configItem>
           </variant>
   ```

4. Configure the desktop environment settings somewhere.

## Known Problem(s)

These modified files could be overwritten after a system update. Do not directly overwrite the new files using backuped old ones to recover the function, unless you are sure that the changes made in the update to the unmodified parts are absolutely meaningless to you.

__Please tell me if there is anything wrong.__
