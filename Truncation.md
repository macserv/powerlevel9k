# P9K_DIR_SHORTEN_STRATEGY="en_vowel"


## Strategy
----------------------------------------------------
* Attempt to position delimiter at the last eligibile non-consonant character (see rules below).
    * Desired truncation point characters include [AaEeIiOoUu\W\_]
        * All vowels, all non-word characters, underscore (considered a "word character")
+ If no desired point is found, truncate before the last eligible character.
+ The truncation delimiter, P9K_DIR_SHORTEN_DELIMITER, must be at least one character.
    - If it is not set, or is empty, truncation will not occur at all.
- A minimum of one (1) character must always follow the truncation delimiter.

### If P9K_DIR_SHORTEN_KEEP_EXT is "true":
* Truncate name and extension separately, and include the "." separator.
* A minimum of two (2) characters must precede the truncation delimiter for the "name" part.
* A minimum of one (1) characters must precede the truncation delimiter for the "extension" part.
* P9K_DIR_SHORTEN_LENGTH is the desired maximum characters to be presented (including truncation delimiter) for the "name" part of the path component.
    * Default is 8
* P9K_DIR_SHORTEN_EXT_LENGTH is the desired maximum characters to be presented (including truncation delimiter) for the "extension" part of the path component.
    * Default is 4
    * If this is set to 0 (zero), the extension will never be truncated.
    
### Otherwise:
* Truncate entire path component as a single string.
* A minimum of two (2) characters must precede the truncation delimiter.
* P9K_DIR_SHORTEN_LENGTH is the desired maximum characters to be presented (including truncation delimiter) for the entire path component.
    * Default is 8


## Notes for Implementation
------------------------
* According to the above rules:
    * The lowest honored value for P9K_DIR_SHORTEN_LENGTH is 4
    * The lowest honored non-zero value for P9K_DIR_SHORTEN_EXT_LENGTH is 3.
* Truncation threshold = shortening length + delimiter length


## Samples (delimiter: "␣")
----------------------

### No Truncation
`/System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support`
`/Applications/Xcode.app/Contents/Applications/Instruments.app/Contents/Resources/DTracePlugin/fileactivity.instrument`


### P9K_DIR_SHORTEN_KEEP_EXT = false

#### 8
`/System/Library/Fram␣rks/CoreS␣rk/Versions/A/Fram␣rks/Launc␣rk/Versions/A/Support`
`/Appli␣ns/Xcode␣pp/Contents/Appli␣ns/Instr␣pp/Contents/Resour␣s/DTrace␣n/filea␣nt`

#### 7
`/System/Library/Fra␣rks/Core␣rk/Vers␣ns/A/Fra␣rks/Laun␣rk/Vers␣ns/A/Support`
`/Appl␣ns/Xcod␣pp/Con␣nts/Appl␣ns/Inst␣pp/Con␣nts/Resou␣s/DTrac␣n/file␣nt`

#### 6
`/System/Lib␣ry/Fr␣rks/Cor␣rk/Ver␣ns/A/Fr␣rks/Lau␣rk/Ver␣ns/A/Sup␣rt`
`/App␣ns/Xco␣pp/Co␣nts/App␣ns/Ins␣pp/Co␣nts/Reso␣s/DTra␣n/fil␣nt`

#### 5
`/Sys␣m/Li␣ry/Fr␣ks/Co␣rk/Ve␣ns/A/Fr␣ks/La␣rk/Ve␣ns/A/Su␣rt`
`/Ap␣ns/Xc␣pp/Co␣ts/Ap␣ns/In␣pp/Co␣ts/Res␣s/DTr␣n/fi␣nt`


### P9K_DIR_SHORTEN_KEEP_EXT = TRUE

#### 8, 4
`/System/Library/Fram␣rks/CoreSe␣s.f␣rk/Versions/A/Fram␣rks/Launch␣s.f␣rk/Versions/A/Support`
`/Appli␣ns/Xcode.app/Contents/Appli␣ns/Inst␣nts.app/Contents/Resour␣s/DTrace␣n/filea␣ty.i␣nt`

#### 7, 4
`/System/Library/Fra␣rks/CoreS␣s.f␣rk/Vers␣ns/A/Fra␣rks/LaunchSe␣s.f␣rk/Vers␣ns/A/Support`
`/Appl␣ns/Xcode.app/Con␣nts/Appl␣ns/Ins␣nts.app/Con␣nts/Resou␣s/DTrac␣n/file␣ty.i␣nt`

#### 6, 0
`/System/Lib␣ry/Fr␣rks/Core␣s.framework/Ver␣ns/A/Fr␣rks/Laun␣s.framework/Ver␣ns/A/Sup␣rt`
`/App␣ns/Xcode.app/Co␣nts/App␣ns/In␣nts.app/Co␣nts/Reso␣s/DTra␣n/fil␣ty.instrument`

#### 5, 3
`/Sys␣m/Li␣ry/Fr␣ks/Cor␣s.f␣k/Ve␣ns/A/Fr␣ks/Lau␣s.f␣k/Versions/A/Support`
`/Ap␣ns/Xcode.app/Co␣ts/Ap␣ns/I␣nts.app/Co␣ts/Res␣s/DTr␣n/fi␣ty.i␣t`
