# fix-digits changelog

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
            2024-06-28
        </td>
        <td>
            <p>
               Fixed a bug that prevented renaming of identically numbered files. This currently does not work when reordering (<code>-o, --reorder</code>). If such a reordering is attempted, an error message suggesting a workaround is shown: <code>Reordering identically numbered files is not supported. To work around this, split the file set into batches in which numbers do not repeat, and reorder each batch separately.</code>. Then the program exits.
            </p>
        </td>
    </tr>
    <tr>
        <td>
            <a href='https://github.com/linguisticmind/fix-digits/releases/tag/v0.2.1'>0.2.1</a>
        </td>
        <td>
            2024-06-17
        </td>
        <td>
            <p>
               Fixed the default prompt reply not working (when <code>-x, --reorder-file-clear-temporary</code> is set to <code>prompt</code>). 
            </p>
        </td>
    </tr>
    <tr>
        <td>
            <a href='https://github.com/linguisticmind/fix-digits/releases/tag/v0.2.0'>0.2.0</a>
        </td>
        <td>
            2024-06-12
        </td>
        <td>
            <p>
                <b>NEW</b>: Added the following major functionality:
                <ul>
                    <li>Reordering</li>
                    <li>Incrementing or decrementing numbers</li>
                    <li>Removing gaps in numbers</li>
                </ul>
            </p>
            <p>
                Added the following new options:
                <ul>
                    <li><code>-p, --print-cmd / -P, --no-print-cmd</code></li>
                    <li><code>-g, --preserve-gaps / -G, --no-preserve-gaps</code></li>
                    <li><code>-s, --shift / -S, --no-shift</code></li>
                    <li><code>-z, --zero-pad / -Z, --no-zero-pad</code>, <code>-n, --zero-pad-normalize / -N, --zero-pad-no-normalize</code></li>
                    <li><code>-o, --reorder / -O, --reorder</code>, <code>-f, --reorder-file</code>, <code>-k, --reorder-file-keep-temporary / -K, --reorder-file-no-keep-temporary</code>, <code>-e, --reorder-file-edit / -E, --reorder-file-no-edit</code>, <code>-m, --reorder-file-gaps-compact / -M, --reorder-file-gaps-no-compact</code>, <code>--editor</code></li>
                    <li><code>--match-sign / --no-match-sign</code></li>
                </ul>
            </p>
            <p>
                <b>BREAKING</b>: Some options were renamed:
                <ul>
                    <li>Renamed <code>-r, --rename</code> to <code>-r, --run</code> (for consistency with <a href='https://github.com/linguisticmind/reln'><code>reln</code></a> and <a href='https://github.com/linguisticmind/unln'><code>unln</code></a>).</li>
                    <li>Renamed <code>-b, --before</code> to <code>-b, --match-before</code>, and <code>-b, --after</code> to <code>-b, --match-after</code> for clarity and consistency in organization of option names.</li>
                </ul>
            </p>
            <p>
                GNU sed is now again a dependency, but with a different purpose compared to when it was removed in v0.1.2.<br>
                The <code>Not renaming &lt;old&gt; -> &lt;new&gt;. &lt;new&gt; already exists</code> and <code>Some files were not renamed because other files with the same name already existed.</code> warning messages are now error messages, and the latter now also lists the files that stood in the way.
            </p>
        </td>
    </tr>
    <tr>
        <td>
            <a href='https://github.com/linguisticmind/fix-digits/releases/tag/v0.1.3'>0.1.3</a>
        </td>
        <td>
            2024-06-09
        </td>
        <td>
            <p>
                Specified end of options (<code>--</code>) for the <code>mv</code> command to prevent problems renaming files whose name starts with a hyphen.
            </p>
            <p>
                Updated copyright year.
            </p>
        </td>
    </tr>
    <tr>
        <td>
            <a href='https://github.com/linguisticmind/fix-digits/releases/tag/v0.1.2'>0.1.2</a>
        </td>
        <td>
            2024-06-01
        </td>
        <td>
            <p>
                Eliminated the limitation on using capture groups in regular expressions set with <code>-b, --before</code> and <code>-a, --after</code>.
            </p>
            <p>
                Removed a redundancy in the regular expression for matching filenames.
            </p>
        </td>
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
    <tr>
        <td>
            <a href='https://github.com/linguisticmind/fix-digits/releases/tag/v0.1.0'>0.1.0</a>
        </td>
        <td>
            2024-02-07
        </td>
        <td>
            <p>
                Initial release.
            </p>
        </td>
    </tr>
</table>
