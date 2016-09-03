
xpipe<sup>[1]</sup>
===================

Use cross-platform IPC<sup>[2]</sup> paths in node.

Background
----------

In node - instead of utilizing TCP - you can use IPC to communicate to other services like...

- web servers (NGINX)
- data structure stores (redis)
- databases (MongoDB, Cassandra)
- [place your own here :]

...or to interconnect node applications, Electron frontends/backends etc.  

**This can lead to large speed gains.**

On unixoid operating systems - e.g. Linux and OS X - this is achieved by using 
[Unix domain sockets](https://en.wikipedia.org/wiki/Unix_domain_socket) that 
are referred by file descriptors.

Unlike the former, Windows utilizes [named pipes](https://en.wikipedia.org/wiki/Named_pipe) living 
in the root directory of the NPFS<sup>[3]</sup>, mounted under the special path \\.\pipe\.

To mitigate these differences, xpipe was born...


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
- **cd c:/Windows** and **cd /Windows** work<sup>[4]</sup>
- **dir ./ /B** fails but **dir "./" /B** works

Further articles: 
- https://en.m.wikipedia.org/wiki/Path_(computing)

  
  
  
[1]: xpipe stands for **xp (cross-platform) IPC path equalizer**  
[2]: inter-process communication, see https://en.wikipedia.org/wiki/Inter-process_communication  
[3]: named pipe file system (in-memory)  
[4]: on Windows "/" without a leading drive letter represents the root of the current drive  
