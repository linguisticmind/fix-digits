# fix-digits

`fix-digits` is a Bash script that allows you to add leading zeros to numbers in filenames to ensure their correct sorting.

For example:

```
1-name.ext     ->   001-name.ext
2-name.ext     ->   002-name.ext
3-name.ext     ->   003-name.ext
4-name.ext     ->   004-name.ext
5-name.ext     ->   005-name.ext
6-name.ext     ->   006-name.ext
7-name.ext     ->   007-name.ext
8-name.ext     ->   008-name.ext
9-name.ext     ->   009-name.ext
10-name.ext    ->   010-name.ext
11-name.ext    ->   011-name.ext
12-name.ext    ->   012-name.ext
...
99-name.ext    ->   099-name.ext
100-name.ext   ->   100-name.ext
```

Video tutorial:

[![Mindful Technology - fix digits: add leading zeros to numbers in filenames](https://img.youtube.com/vi/ksyw7mit6g4/0.jpg)](https://www.youtube.com/watch?v=ksyw7mit6g4)

## Changelog

<table>
    <tr>
        <th>Version</th>
        <th>Date</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>
            <a href='https://github.com/linguisticmind/fix-digits/releases/tag/v0.1.1'>0.1.1</a>
        </td>
        <td>
            2024-05-26
        </td>
        <td>
            <p>
                <b>CRITICAL</b>: Fixed a bug where the check for already existing files was only performed for regular files, but not directories.<br>
                Fixed a bug which would result in incorrect handling of files located in the root directory (<code>/</code>) if passed as absolute paths (<code>/1-file /2-file ...</code>).<br>
                Duplicate forward slashes in paths are now removed as appropriate.
            </p>
            <p>
                Improved the method of quoting strings for displaying them in messages. All instances of using <code>\'"${parameter//\'/\'\\\'\'}"\'</code> were replaced with <code>"${parameter@Q}"</code>.<br>
                Improved code for the <code>Use of capture groups in regular expressions set with `-b, --before` and `-a, --after` is not allowed</code> error message. Removed <code>sed</code> dependency.
            </p>
            <p>
                Improved formatting of the built-in help message.<br>
                Added information about dependencies to README.<br>
                Added a changelog.
            </p>
            <p>
                Removed a superfluous <code>IFS=' '</code> from the <code>getopt</code> line.<br>
                Removed a superfluous <code>:</code> on the line preceding the <code>mv</code> command.
            </p>
        </td>
    </tr>
</table>

[Read more](CHANGELOG.md)

## Dependencies

`search-in-subs` requires that [`mpv`](https://mpv.io/), [`ffmpeg`](https://ffmpeg.org/) and [`lua`](https://www.lua.org/) (v5.4) be installed to use [mpv EDL](https://github.com/mpv-player/mpv/blob/master/DOCS/edl-mpv.rst) generation functionality.

On Debian, run `sudo apt install mpv ffmpeg lua5.4` to install these dependencies.

`lua` 5.4 is the version of `lua` that `search-in-subs` was tested with. `search-in-subs` first checks `PATH` for a binary called `lua5.4`, and if that is not available, it uses `lua` as a fallback binary name.

`search-in-subs` was written and tested on Debian 12, and takes advantage of standard utilities that come with the system. In order to run `search-in-subs` on other systems, make sure that the following are installed and available on system's `PATH`:

* Bash >= 5.2.15
* Enhanced getopt
* GNU coreutils
* GNU sed

## Installation

1. Clone this repository to a directory of your choice (e.g. `~/repos`):

    ```bash
    cd ~/repos
    git clone https://github.com/linguisticmind/fix-digits.git
    ```

2. Symlink or copy the [script file](fix-digits) to a directory on your `PATH` (e.g. `~/bin`):

    ```bash
    cd ~/bin
    # To symlink:
    ln -sv ../repos/fix-digits/fix-digits
    # To copy:
    cp -av ../repos/fix-digits/fix-digits .
    ```

3. (OPTIONAL) Symlink or copy the [man page](man/man1/fix-digits.1) to a directory on your `MANPATH` (e.g. `~/man`):

    ```bash
    cd ~/man/man1 # The `man` directory should contain subdirectories for different manual sections: `man1`, `man2` etc.
    # To symlink:
    ln -sv ../../repos/fix-digits/man/man1/fix-digits.1
    # To copy:
    cp -av ../../repos/fix-digits/man/man1/fix-digits.1 .
    ```

    A copy of the manual page is also [included in this README file](#manual).

4. (OPTIONAL) Copy the [example config file](config.bash) to the config directory:

    ```bash
    mkdir -v ~/.config/fix-digits
    cp -v ~/repos/fix-digits/config.bash ~/.config/fix-digits
    ```

## Manual

```plain
FIX-DIGITS(1)               General Commands Manual              FIX-DIGITS(1)

NAME
       fix-digits - add leading zeros to numbers in filenames

SYNOPSIS
        fix-digits [<options>] [<file> ...]

DESCRIPTION
       fix-digits allows the user to bulk-rename files by zero-padding numbers
       in filenames such that all numbers in those  filenames  have  an  equal
       number of digits.

       For example:

              1-name.ext     ->   001-name.ext
              2-name.ext     ->   002-name.ext
              3-name.ext     ->   003-name.ext
              4-name.ext     ->   004-name.ext
              5-name.ext     ->   005-name.ext
              6-name.ext     ->   006-name.ext
              7-name.ext     ->   007-name.ext
              8-name.ext     ->   008-name.ext
              9-name.ext     ->   009-name.ext
              10-name.ext    ->   010-name.ext
              11-name.ext    ->   011-name.ext
              12-name.ext    ->   012-name.ext
              ...
              99-name.ext    ->   099-name.ext
              100-name.ext   ->   100-name.ext

       This ensures that the files are always sorted in the intended numerical
       order - whether or not a given program supports a sorting  method  that
       would allow for such a sort order without the numbers in filenames hav‐
       ing leading zeros added.

       Renaming is done by matching parts of the  filenames  that  immediately
       precede and follow the numeric part, with regular expressions. This al‐
       lows fix-digits to identify the part that contains the numbers, and re‐
       name  the  files.  These  regular  expressions are set by using the -b,
       --before and -a, --after options.

       By default, fix-digits does not rename the files,  but  only  simulates
       the  renaming,  providing  the user with a preview of the changes to be
       made. The actual renaming can then be done by  running  `fix-digits  -r
       [<file> ...]`.

       If  no  <file> argument is passed to fix-digits, it performs the opera‐
       tion on all files in the current  working  directory  (except  for  the
       files  whose  names  start  with  a dot). This is equivalent to running
       `fix-digits [<options>] *` (with `shopt dotglob` set to `off`).

       If a file with the same name already exists, it will not be renamed,  a
       warning message will appear, and fix-digits will exit with exit code 2.

OPTIONS
       -b, --before=<regex>
              Regular  expression  to  match the part of the filenames immedi‐
              ately preceding the numbers. Note  that  matching  is  performed
              only  on  the  basename  of  the file (i.e. not on the path that
              might precede the filename).

              The default value is `^`.

              Also see REGULAR EXPESSIONS below.

       -a, --after=<regex>
              Regular expression to match the part of  the  filenames  immedi‐
              ately following the numbers.

              The default value is `-.*$`.

              Also see REGULAR EXPESSIONS below.

       -r, --rename
              Rename the files instead of simulating the renaming.

       -R, --no-rename
              Do not rename the files, only simulate the renaming. This is the
              default.

       -c, --color
              Colorize the output. This is the default.

       -C, --no-color
              Disable colorization of the output.

       -h, --help
              Print help.

       -V, --version
              Print version information.

REGULAR EXPRESSIONS
       The regular expressions used are POSIX Extended Regular Expressions  as
       used  in Bash, in the `[[ <value> =~ <regex> ]]` construct. More infor‐
       mation   on   POSIX   Regular   Expressions    can    be    found    at
       <https://www.gnu.org/software/grep/manual/html_node/Regular-Expres‐
       sions.html>.

       Using capture groups in regular expressions passed  with  -b,  --before
       and -a, --after options is not allowed as that would break the matching
       of parts of filenames that is required for the rename operation.

FILES
       A configuration file can be used to set default options.

       The configuration file's location  is  $XDG_CONFIG_HOME/fix-digits/con‐
       fig.bash. If XDG_CONFIG_HOME is not set, it defaults to ~/.config.

EXIT CODES
       fix-digits returns the following exit codes:

       0   Success. No errors have occured.

       1   A general error has occured.
       2   Renaming failed. File with the same name already exists. See output for more details.

AUTHOR
       Alex Rogers <https://github.com/linguisticmind>

HOMEPAGE
       <https://github.com/linguisticmind/fix-digits>

COPYRIGHT
       Copyright  ©  2023  Alex  Rogers.  License GPLv3+: GNU GPL version 3 or
       later <https://gnu.org/licenses/gpl.html>.

       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

FIX-DIGITS 0.1.1                     2023                        FIX-DIGITS(1)
```

## License

[GNU General Public License v3.0](LICENSE)
