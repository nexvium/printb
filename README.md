# printb

printb is a small program to view integers in binary format for easier human consumption. Bits may be grouped (e.g. to better visualize bitfields), numbered (e.g. to easily identify specific bits), or highlighted (e.g. to emphasize the flags that are on).

The program is implemented in a single file with (AFAIK) no dependencies other than perl. There is no need to install or configure anything to use it.

### Usage

    printb [opts] <arg1> [arg2 ...]

Arguments may be decimal, octal with a leading `0`, hexadecimal with a leading `0x`, or binary with a leading `0b`.

### Options

The options below are supported by the program.

* `-h` `--help`

  Output a summary of usage and options and exit.

* `-v` `--version`

  Output the version number, currently v2.2.x, and exit.

* `-wN` `--width=N`

  Specify the width of the numbers. Defaults to the smallest of 8, 16, 32, or 64 bits that is wide enough for the largest argument.

* `-gSPEC` `--group=SPEC`

  Change the way bits are grouped in the output. Default is to group by 8 bits (i.e. bytes). If SPEC is `0`, not grouping is done at all. If SPEC is an integer, bits are grouped into groups of that many bits.

  SPEC may also specify groups of non-uniform widths. For example:

  * `3:4:5` = 12 bits in three groups of 3, 4, and 5, respectively
  * `:3:4:5` = 12+ bits in four groups, first group has all bits not in other three
  * `3:4:5:` = 12+ bits in four groups, last group has all bits not in other three
  * `3:4::5` = 12+ bits in four groups, third groups has all bits not in other three

* `--values`

  Interpret each bit group as an integer and output its value.

* `-c` `--color`

  With `-g`, use colors instead of spaces to identify different groups.

* `-n` `--number`

  Number all the bits. By default the least-significant bit is numbered 0.

* `-NN` `--number-from=N`

  Number all the bits, with the least-significant bit numbered N.

* `-r` `--reverse`

  With `-n` or `-N`, number the bits starting with the most-significant bit instead of the least.

* `-1` `--on`

  Highlight the bits that are on (i.e. 1, true, set, ...).

* `-0` `--off`

  Highlight the bits that are off (i.e. 0, false, not set, ...)

### Examples

Output a 24-bit value as four fields of 10, 6, 3, and 5 bits.

```
$ printb -n -w24 -g:6:3:5 --values 0xc0ded
   2          1            
3210987654 321098 765 43210
---------- ------ --- -----
0000110000 001101 111 01101
     |        |    |    |  
     |        |    |    +-- 13 / 0xD
     |        |    +-- 7
     |        +-- 13 / 0xD
     +-- 48 / 0x30
```

### Disclaimer

Copyright (C) 2010 by Javier Alvarado.

This program was written for personal use by the author. Permission is hereby granted to study, use, copy, and/or modify for non-commercial use.

***THE SOFTWARE IS PROVIDED "AS IS" AND WITHOUT WARRANTY OF ANY KIND. THE AUTHOR IS IN NO WAY LIABLE FOR ANY DAMAGES OR LOSS OF DATA.***
