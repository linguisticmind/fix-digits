# fix-digits changelog

<table>
    <tr>
        <th>Version</th>
        <th>Date</th>
        <th>Description</th>
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
