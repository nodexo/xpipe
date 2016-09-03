
xpipe<sup>[1]</sup>
===================

Use cross-platform IPC paths in node.

Usage
-----

```javascript
const xpipe = require('xpipe');

let prefix = xpipe.prefix;
console.log( `prefix:  ${prefix}` );
/*
  [empty string] on Linux and OS X
  "//./pipe/" on Windows
*/

let ipcPath = xpipe.eq('/tmp/my.sock');
console.log( `ipcPath: ${ipcPath}` );
/*
  "/tmp/my.sock" on Linux and OS X
  "//./pipe/tmp/my.sock" on Windows
*/
```

When did Windows start accepting forward slash as a path separator?
-------------------------------------------------------------------

Every Windows API/kernel ever has accepted "/" as a path separator.
So has every version of MS-DOS beginning with DOS 2.0 (the first version 
to support subdirectories).

It's only been in command lines that "/" was not allowed when it had
already been used as a switch delimiter in MS-DOS 1.0 (introduced by IBM).

This behaviour could be bypassed (at least on modern Windows systems) by including 
the path in double quotation marks:
- **cd c:/Windows** and **cd /Windows** work<sup>[2]</sup>
- **dir ./ /B** fails but **dir "./" /B** works

Further articles: 
- https://en.m.wikipedia.org/wiki/Path_(computing)

  
  
  
[1]: xpipe stands for **xp (cross-platform) IPC path equalizer**  
[2]: on Windows "/" without a leading drive letter represents the root of the current drive  
