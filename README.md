# fix-digits

`fix-digits` allows the user to perform various operations on numbered files that involve modifying the part of the filename containing the number. Those operations include zero-padding (`-z, --zero-pad`), reordering (`-o, --reorder`), incrementing or decrementing (`-s, --shift`), and removing gaps (`-g, --remove-gaps`).

Here is an example of zero-padding numbered files to ensure their correct sorting:

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

Reordering files is done by rearranging lines in a reorder file. A reorder file gets generated and opened in a text editor when `fix-digits` is run with `-o, --reorder`. Each line in the reorder file represents an input file. Rearranging the lines in the desired order, saving the reorder file, and closing the text editor will result in the numbers in filenames being adjusted according to the order specified in the reorder file.

For more information on other operations, see [Manual](#manual) below.

Video tutorials:

<table>
    <tr>
        <td align='center'>
            <b>v0.2.0</b>: reordering, incrementing or<br>decrementing, removing gaps
        </td>
        <td align='center'>
            <b>v0.1.0</b>: zero-padding numbers in filenames
        </td>
    </tr>
    <tr>
        <td>
            <a href='https://www.youtube.com/watch?v=<id>'>
                <img src='https://img.youtube.com/vi/RMeq_-NXrzw/0.jpg' alt='Mindful Technology - fix-digits v0.2.0: reorder numbered files & more (zero-pad, remove gaps, increment/decrement)' width='360'>
            </a>
        </td>
        <td>
            <a href='https://www.youtube.com/watch?v=ksyw7mit6g4'>
                <img src='https://img.youtube.com/vi/ksyw7mit6g4/0.jpg' alt='Mindful Technology - fix digits: add leading zeros to numbers in filenames' width='360'>
            </a>
        </td>
    </tr>
</table>

## Changelog

<table>
    <tr>
        <th>Version</th>
        <th>Date</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>
            <a href='https://github.com/linguisticmind/fix-digits/releases/tag/v0.2.2'>0.2.2</a>
        </td>
        <td>
            2024-06-27
        </td>
        <td>
            <p>
               Fixed a bug that prevented renaming of identically numbered files. 
            </p>
        </td>
    </tr>
</table>

[Read more](CHANGELOG.md)

## Dependencies

`fix-digits` was written and tested on Debian 12, and takes advantage of standard utilities that come with the system. In order to run `search-in-subs` on other systems, make sure that the following are installed and available on system's `PATH`:

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
       fix-digits - adjust numbers in filenames

SYNOPSIS
        fix-digits [<options>] [<file> ...]

DESCRIPTION
       fix-digits  allows  the  user to perform various operations on numbered
       files that involve modifying the part of the  filename  containing  the
       number.  Those  operations  include  zero-padding (-z, --zero-pad), re‐
       ordering (-o, --reorder), incrementing or decrementing  (-s,  --shift),
       and removing gaps (-g, --preserve-gaps).

       Here is an example of zero-padding numbered files:

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
       --match-before and -a, --match-after options.

       Reordering files is done by rearranging lines in a reorder file. A  re‐
       order  file  gets generated and opened in a text editor when fix-digits
       is run with -o, --reorder. Each line in the reorder file represents  an
       input  file. Rearranging the lines in the desired order, saving the re‐
       order file, and closing the text editor will result in the  numbers  in
       filenames  being  adjusted  according to the order specified in the re‐
       order file.

       For more information on other operations, see OPTIONS below.

       By default, fix-digits does not rename the files,  but  only  simulates
       the  renaming,  providing  the user with a preview of the changes to be
       made. The actual renaming can then be done by running  fix-digits  with
       -r, --run set.

       If  no  <file> argument is passed to fix-digits, it performs the opera‐
       tion on all files in the current  working  directory  (except  for  the
       files  whose  names  start  with  a dot). This is equivalent to running
       `fix-digits [<options>] *` (with `shopt dotglob` set to `off`).

       Files that don't match regular expressions set with -b,  --match-before
       and -a, --match-after are ignored.

       If  a file with the same name already exists, it will not be renamed, a
       warning message will appear, and fix-digits will exit with exit  status
       2.

OPTIONS
   Passing arguments to options
       Enhanced  getopt  syntax applies when passing options. There is one im‐
       portant point to highlight when it comes to passing  options  with  re‐
       quired vs optional arguments.

       In  case  of  a short option, if an option takes a *required* argument,
       the argument may be written as a separate parameter, *or* directly  af‐
       ter  the  option  character. If an option takes an *optional* argument,
       however, the argument *must* be written directly after the option char‐
       acter.

       In case of a long option, if an option takes a *required* argument, the
       argument may be written as a separate parameter,  *or*  directly  after
       the  option name, separated by an equals sign (`=`). If an option takes
       an *optional* argument, however, the argument *must*  be  writtent  di‐
       rectly after the option name, separated by an equals sign (`=`).

                           Short option   Long option
       Required argument   -o <value>     --option <value>
                           -o<value>      --option=<value>
       Optional argument   -o[<value>]    --option[=<value>]

       Options  that  take optional arguments can be recognized in the options
       list below by their <value> and the preceding  equals  sign  being  en‐
       closed in square brackets:

       -o, --option[=<value>]

   General
       -r, --run
              Rename the files instead of simulating the renaming.

       -R, --no-run
              Do not rename the files, only simulate the renaming. This is the
              default.

       -p, --print-cmd
              Print a preview of the commands to be executed.

       -P, --no-print-cmd
              Do not print a preview of the commands to be executed.  This  is
              the default.

       -b, --match-before=<regex>
              Regular  expression  to  match the part of the filenames immedi‐
              ately preceding the numbers. Note  that  matching  is  performed
              only  on  the  basename  of  the file (i.e. not on the path that
              might precede the filename).

              The default value is `^`.

              Also see REGULAR EXPESSIONS below.

       -a, --match-after=<regex>
              Regular expression to match the part of  the  filenames  immedi‐
              ately following the numbers.

              The default value is `-.*$`.

              Also see REGULAR EXPESSIONS below.

       --match-sign
              Match minus (-) signs preceding numbers in filenames.

       --no-match-sign
              Do  not  match  minus  (-) signs preceding numbers in filenames.
              This is the default.

       -g, --preserve-gaps
              Preserve gaps in numbering of files. This is the default.

       -G, --no-preserve-gaps
              Do not preserve gaps in numbering of files.

       -s, --shift=[+|-]<integer>
              Increment or decrement  numbers  in  filenames  by  a  specified
              value. The default value is `0`.

       -z, --zero-pad[={<integer>|auto}]
              Add  leading zeros to numbers in filenames. The default value is
              `auto`.

              The value can be an integer greater than or equal to 0,  `auto`,
              or no value. Omitting the value is equivalent to passing `auto`.

       -Z, --no-zero-pad
              Do  not add leading zeros to numbers in filenames. Equivalent to
              -z, --zero-pad set to `0`.

       -n, --zero-pad-normalize
              Remove existing leading zeros from numbers in filenames.

       -N, --zero-pad-no-normalize
              Do not remove existing leading zeros from numbers in  filenames.
              This is the default.

   Reordering
       -o, --reorder
              Change the order of files by modifying numbers in their names.

              Also see REORDER FILE.

       -O, --no-reorder
              Do  not  change the order of files by modifying numbers in their
              names. This is the default.

       -f, --reorder-file=<path>
              A custom path to a reorder file.

              If not set, a temporary file in the cache  directory  gets  cre‐
              ated. See FILES for more information.

       -k, --reorder-file-keep-temporary[={always|auto|never}]
              Whether  or when to keep the temporary reorder file after an op‐
              eration finishes. The default value is `auto`.

              NB: This option does not apply when a path to a reorder file  is
              set  with  -f,  --reorder-file. Such a file never gets automati‐
              cally deleted. See -f, --reorder-file for more information.

              [always]
                     Always keep the reorder file.

              auto (default)
                     Keep the reorder file when simulating the operation  (-R,
                     --no-run), but delete it when actually renaming the files
                     (-r, --run).

              never  Never keep the reorder file.

       -K, --reorder-file-no-keep-temporary
              Do not keep the reorder file after an operation finishes. Equiv‐
              alent to -k, --reorder-file-keep-temporary set to `never`.

       -x, --reorder-file-clear-temporary[={always|auto|prompt|never}]
              Whether  or when to delete the temporary reorder file before be‐
              ginning an operation. The default value is `never`.

              NB: This option does not apply when a path to a reorder file  is
              set  with  -f,  --reorder-file. Such a file never gets automati‐
              cally deleted. See -f, --reorder-file for more information.

              If this option is used while -o, --reorder is not set, the  file
              renaming  operation  does not run, and only attempting to delete
              the temporary reorder file takes place.

              [always]
                     Always delete the reorder file.

              auto (default)
                     Delete the reorder file if it does not match the  current
                     file set; otherwise, keep it.

              prompt Like  `auto`, but ask what to do if the reorder file does
                     not match the current file set.  Provides  an  option  to
                     view the file before making a decision.

              never  Never delete the reorder file.

       -X, --reorder-file-no-clear-temporary
              Do  not  delete  the reorder file before beginning an operation.
              Equivalent to -k, --reorder-file-clear-temporary set to `never`.

       -e, --reorder-file-edit[={always|auto|never}]
              Whether or when to edit the reorder file. The default  value  is
              `auto`.

              [always]
                     Always edit the reorder file.

              auto (default)
                     Edit  the  reorder  file when generating it for the first
                     time, but do not edit, and only load it if it already ex‐
                     isted.

              never  Never edit the reorder file.

       -E, --reorder-file-no-edit
              Do  not edit the reorder file. Equivalent to -k, --reorder-file-
              edit set to `never`.

       -m, --reorder-file-gaps-compact
              Represent gaps with ranges in reorder file instead of one number
              per line.

       -M, --reorder-file-gaps-no-compact
              Do  not represent gaps with ranges in reorder file, but one num‐
              ber per line. This is the default.

       --editor=<value>
              A text editor to use for reordering files  with  -o,  --reorder.
              The default value depends on the values of VISUAL and EDITOR en‐
              vironment variables. If neither is set,  the  default  value  is
              `nano`.

              See ENVIRONMENT for more information.

   Other
       -c, --color
              Colorize the output. This is the default.

       -C, --no-color
              Disable colorization of the output.

       -h, --help
              Print help.

       -V, --version
              Print version information.

EXIT STATUS
       0   Success. No errors have occured.
       1   A general error has occured.
       2   Renaming failed. File with the same name already exists.
       3   Reorder file is invalid.

ENVIRONMENT
   VISUAL / EDITOR
       The  values  of  VISUAL and EDITOR environment variables are checked if
       --editor is left at its default value. --editor determines the text ed‐
       itor to use for reordering files with -o, --reorder.

       VISUAL  is  evaluated  first. If not set, then EDITOR is evaluated. See
       --editor for more information.

REGULAR EXPRESSIONS
       The regular expressions used are POSIX Extended Regular Expressions  as
       used  in Bash, in the `[[ <value> =~ <regex> ]]` construct. More infor‐
       mation   on   POSIX   Regular   Expressions    can    be    found    at
       <https://www.gnu.org/software/grep/manual/html_node/Regular-Expres‐
       sions.html>.

REORDER FILE
       A reorder file is a plain text file used to represent a  new  order  of
       files according to which the part of the filenames that contains a num‐
       ber should be changed. See -o, --reorder, and --reorder-file-*  options
       for more information.

       Each  line in a reorder file can be a filename, a gap specification, or
       a comment. Generate a reorder file by running fix-digits with  the  -o,
       --reorder  option. Rearrange the lines in the file to specify a new or‐
       der.

       The file lines contain the original name of the file. To move a file to
       a new position, only move the line without modifying the filename.

       If  a filename contains a newline, it is represented as `\n` in the re‐
       order file. If a filename contains a backslash (`\`), it is represented
       with  a  double  backslash  (`\\`)  in  the reorder line. If a filename
       starts with a number sign (`#`), it must also be escaped with  a  back‐
       slash: `\#`.

       A  gap  specification  is a special comment line. Its format is `# gap:
       <start>[-<end>]` where <start> and <end> are  integers.  Whitespace  is
       optional.  The  -m, --reorder-file-gaps-compact option controls whether
       to generate gap specifications  with  one  number  per  line  (`#  gap:
       <start>`), or in the range format (`# gap: <start>-<end>`).

       Gaps behave just like filenames in terms of the effect that rearranging
       lines has on the new numbers in filenames. For example, you can  put  a
       file between two gaps, and the order will be respected.

       All  gaps  in the numerical sequence formed by the numbers in filenames
       must be specified in the reorder file. If that is not the case,  a  re‐
       order file validation check will fail. If filenames in the reorder file
       do not match the original filenames, the validation check will fail  as
       well. When this validation check fails, fix-digits exits with exit sta‐
       tus 3, and no renaming of files takes  place.  Error  messages  specify
       what the problem was.

       Any  line  that starts with a number sign (`#`), and does not match the
       gap specification format is a comment line.

FILES
       A configuration file can be used to set default options.

       The configuration file's location  is  $XDG_CONFIG_HOME/fix-digits/con‐
       fig.bash. If XDG_CONFIG_HOME is not set, it defaults to ~/.config.

       A  temporary reorder file that is generated when using -o, --reorder is
       stored in a cache directory.

       The  cache  directory's  location  is  $XDG_CACHE_HOME/fix-digits.   If
       XDG_CACHE_HOME is not set, it defaults to ~/.cache.

AUTHOR
       Alex Rogers <https://github.com/linguisticmind>

HOMEPAGE
       <https://github.com/linguisticmind/fix-digits>

COPYRIGHT
       Copyright  ©  2023  Alex  Rogers.  License GPLv3+: GNU GPL version 3 or
       later <https://gnu.org/licenses/gpl.html>.

       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

FIX-DIGITS 0.2.2                     2024                        FIX-DIGITS(1)
```

## License

[GNU General Public License v3.0](LICENSE)
