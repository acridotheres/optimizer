# AO-HTML

Acridotheres Optimized Hypertext Markup Language is a binary format to store HTML code efficiently.

Use inside [HSSP](https://github.com/acridotheres/hssp)v8 files for best results. 

## File structure

- `AO---HTML5` at the very beginning of the file
- All the encoded content

## Encoding

### HTML tags

A HTML element tag can be opened using a byte in this range: `0x80`-`0xFF` (128 allowed HTML tags, 127 are used).

It can be closed by either `0x00` (closes without any attributes) or `0x01` (close with attributes).
