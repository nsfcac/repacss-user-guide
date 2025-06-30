# Unix File Permissions

## Overview

This document provides an overview of the Unix file permission model, which governs access to files and directories on REPACSS systems. Each object in the file system is associated with an owner and permission flags that define read, write, and execute privileges for different user classes.

Permissions are typically reviewed using the `ls -l` command:

```bash
ls -l
```

Example output:

```bash
drwx------ 2 bsencer bsencer  2048 Jun 12 2012 private
-rw------- 1 bsencer bsencer  1327 Apr  9 2012 try.f90
-rwx------ 1 bsencer bsencer 12040 Apr  9 2012 a.out
drwxr-xr-x 3 bsencer bsencer  2048 Nov 13 2011 public
```

---

## File Permission Structure

Each line of output in `ls -l` contains a 10-character string representing the file type and permission bits:

| Position | Description                                 |
|----------|---------------------------------------------|
| 1        | File type: `d` (directory) or `-` (regular file) |
| 2–4      | Permissions for the user (owner)            |
| 5–7      | Permissions for the group (not evaluated in current REPACSS scope) |
| 8–10     | Permissions for others (i.e., all users)    |

Permission flags are defined as follows:

- `r`: Read permission
- `w`: Write permission
- `x`: Execute permission
- `-`: Permission not granted

Special flags such as `s` (setgid) are not used in standard user scenarios on REPACSS.

### Interpreting Permission Strings

- `drwx------`: A directory accessible only by the owner
- `-rw-------`: A file readable and writable only by the owner
- `-rwx------`: An executable file restricted to the owner
- `drwxr-xr-x`: A directory accessible to all users for reading and execution, but writable only by the owner

---

## Managing Default Permissions: `umask`

The `umask` command controls the default permission settings for newly created files and directories. The following table outlines common `umask` values and their corresponding default permissions:

| `umask` | File Permissions | Directory Permissions |
|---------|------------------|------------------------|
| 002     | `rw-rw-r--`       | `rwxrwxr-x`            |
| 007     | `rw-rw----`       | `rwxrwx---`            |
| 022     | `rw-r--r--`       | `rwxr-xr-x`            |
| 027     | `rw-r-----`       | `rwxr-x---`            |
| 077     | `rw-------`       | `rwx------`            |

Users may configure their preferred `umask` value by adding the command to their `.bash_profile`.

---

## Modifying Permissions: `chmod`

The `chmod` utility is used to alter file and directory permissions. This can be done using either octal or symbolic notation.

### Octal Notation

| Octal Value | Permission Bits | Description         |
|-------------|------------------|---------------------|
| 0           | `---`            | No permissions      |
| 1           | `--x`            | Execute only        |
| 2           | `-w-`            | Write only          |
| 3           | `-wx`            | Write and execute   |
| 4           | `r--`            | Read only           |
| 5           | `r-x`            | Read and execute    |
| 6           | `rw-`            | Read and write      |
| 7           | `rwx`            | All permissions     |

Example:

```bash
chmod 755 file
```

This sets the file to be fully accessible by the owner, and readable and executable by others (`rwxr-xr-x`).

### Symbolic Notation

Users may also modify permissions with symbolic notation:

```bash
chmod u+x,go+rx file
```

This command grants execute permission to the user, and read/execute permissions to group and others.

| Class | Definition         |
|-------|--------------------|
| `u`   | User (owner)       |
| `o`   | Other (non-owners) |
| `a`   | All users          |

| Operator | Meaning            |
|----------|--------------------|
| `+`      | Add permission      |
| `-`      | Remove permission   |
| `=`      | Set exact permission |

| Mode | Action                    |
|------|---------------------------|
| `r`  | Read                      |
| `w`  | Write                     |
| `x`  | Execute                   |
| `X`  | Conditional execute (directories or if already executable) |

Recursive operations may be executed as follows:

```bash
chmod -R o+rX directory/
```

This command grants read and execute access to others for all applicable files and directories within the specified directory.

---

## Summary

- Use `ls -l` to audit file and directory permissions.
- Apply `chmod` to update access control.
- Configure `umask` to enforce default file security.
- Sensitive files should be explicitly protected using:

```bash
chmod 600 sensitive_file
```

This ensures exclusive read/write access to the owner and denies access to all other users.

---
_Last updated: June 2025_
