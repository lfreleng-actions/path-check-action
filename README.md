<!--
# SPDX-License-Identifier: Apache-2.0
# SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# ✅ Check path exists in repository

Check if a given path exists in the repository.

Sets an output 'exists' to either true or false.

Also reports 'type' as either:

- file
- directory
- invalid

Sets the 'symlink' output to true or false if the given path is a symbolic link.

## Usage Example

<!-- markdownlint-disable MD046 -->

```yaml
steps:
    - name: 'Test repository path: pyproject.toml'
      id: path-to-check
      uses: lfreleng-actions/path-check-action@main
      with:
          path: 'pyproject.toml'
```

<!-- markdownlint-enable MD046 -->

## Inputs

<!-- markdownlint-disable MD013 -->

| Variable Name    | Required | Description                       |
| ---------------- | -------- | --------------------------------- |
| path             | True     | Path to check in local repository |
| exit_on_invalid  | False    | Exit with error if path invalid   |

<!-- markdownlint-enable MD013 -->

## Outputs

<!-- markdownlint-disable MD013 -->

| Variable Name | Mandatory | Description                                        |
| ------------- | --------- | -------------------------------------------------- |
| type          | True      | Either file, directory, or invalid                 |
| symlink       | True      | Set to either: true or false                       |
| exists        | True      | Set to true if path exists, false otherwise        |

<!-- markdownlint-enable MD013 -->

## Broken Symlink Handling

Broken symlinks (symlinks pointing to non-existent targets) return:

- `type: invalid`
- `symlink: true`
- `exists: false`

You can detect broken symlinks by checking if `symlink` is `true` while
both `type` and `exists` show the path is invalid/unusable.
