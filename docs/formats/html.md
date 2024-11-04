# AO-HTML

Acridotheres Optimized Hypertext Markup Language is a binary format to store HTML code efficiently.

Use inside [HSSP](https://github.com/acridotheres/hssp)v8 files for best results. 

## File structure

- `AO---HTML5` at the very beginning of the file
- All the encoded content

## Encoding

### HTML tags

A HTML element tag can be opened using a byte in this range: `0x80`-`0xFF` (128 allowed HTML tags, 127 are used by the w3 spec (including deprecated ones), `0xFF` introduces a custom tag).

It can be closed with `0x00`.

If this is a custom tag, there has to be a `0x00` at the end of the name.

HTML:

```html
<h1>Hello</h1>
<div>
  <p>
    hello
  </p>
</div>
<hello-world />
```

AO-HTML (whitespaces and code points added for better readability):

```
\x80Hello\x00
\xA0
\x86
hello
\x00
\x00
\xFFhello-world\x00\x00
```

### Attributes

As elements can have attributes, an attribute can be introduced after `0x01`, followed by the attribute ID (`0x80`-`0xFF`). The end of an attribute section has to be declared with `0x00`, this closes the current HTML tag too. Note that some elements automatically introduce attribute mode if it can't have any content (e. g. `img`, `hr`, `br`).

HTML:

```html
<a href="/target">click me!</a>
<img src="/img.png" id="myimg">
```

AO-HTML (whitespaces and code points added for better readability):

```
\x90click me!\x01\x80/target\x00
\x91/img.png\xE0my-id\x00
```
