# Unicode
Internally, modern windows uses 16 bit wide unicode characters (UTF16LE), but many application uses 8 bit ANSI (the ASCII extensions that windows uses).
Also, old windows (pre-NT) didn't support unicode.

Because of that, Windows functions with strings as parameters usually have two entry points:
- Unicode, wide, 16 bit (`CreateFileW`)
- ANSI, narrow, 8 bit. (`CreateFileA`)
	- input parameters converted from ANSI to unicode
	- output parameters converted from unicode to ANSI
	- small overhead for the conversion
Usually there's a macro that expands the base function name `CreateFile` into the unicode or ansi implementation based on the `UNICODE` compilation constant
