# 🔐 Unix File Permissions

## 📘 Overview

Every file and directory in a Unix system has:

- An **owner**
- A set of **permission flags**
- Permissions for:
  - the **user** (owner)
  - **other** (everyone else)

You can view permissions using the `ls -l` command:

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

### 🔎 Understanding the Permission Flags

| Position | Meaning                                 |
|----------|------------------------------------------|
| 1        | `d` if directory, `-` if regular file     |
| 2–4      | Read (`r`), Write (`w`), Execute (`x`) for **user** (owner) |
| 5–7      | Read, Write, Execute for **group** (removed from scope) |
| 8–10     | Read, Write, Execute for **other** (world) |

Flag meanings:

- `-` = flag is not set
- `r` = readable
- `w` = writable
- `x` = executable
- `s` = setgid (not used in simplified form)

### 🧠 Interpreting Examples

- `drwx------`: directory, full access for owner, no access for others.
- `-rw-------`: regular file, readable and writable by owner only.
- `-rwx------`: executable file, accessible only by owner.
- `drwxr-xr-x`: directory, readable/executable by everyone, writable by owner.

---

## 🛠 Useful File Permission Commands

### 🧰 umask

Controls default permissions for new files. Common values:

| umask | File Perms | Dir Perms   |
|-------|------------|-------------|
| 002   | `rw-rw-r--`| `rwxrwxr-x` |
| 007   | `rw-rw----`| `rwxrwx---` |
| 022   | `rw-r--r--`| `rwxr-xr-x` |
| 027   | `rw-r-----`| `rwxr-x---` |
| 077   | `rw-------`| `rwx------` |

Set this in `.bash_profile` for it to persist.

### 🔧 chmod (Change Mode)

Used to change permissions.

#### Using Octal Notation

| Octal | Meaning         |
|-------|------------------|
| 0     | --- (none)       |
| 1     | --x (execute)    |
| 2     | -w- (write)      |
| 3     | -wx (write+exec) |
| 4     | r-- (read)       |
| 5     | r-x (read+exec)  |
| 6     | rw- (read+write) |
| 7     | rwx (all)        |

Example:

```bash
chmod 755 file
# Sets: rwxr-xr-x
```

#### Using Symbolic Notation

```bash
chmod u+x,go+rx file
# Adds execute to user, read+execute to others
```

| Class | Description              |
|-------|--------------------------|
| u     | user (owner)             |
| o     | other (world)            |
| a     | all (user + other)       |

| Operator | Meaning                 |
|----------|--------------------------|
| `+`      | Add permission           |
| `-`      | Remove permission        |
| `=`      | Set exact permission     |

| Mode | Description                              |
|------|------------------------------------------|
| r    | read                                     |
| w    | write                                    |
| x    | execute                                  |
| X    | special execute (only if already set)    |

Example:

```bash
chmod -R o+rX directory/
```

Adds read and execute to others for all directories and executable files within.

---

## ✅ Summary

- Use `ls -l` to check permissions.
- Use `chmod` to modify them.
- Use `umask` to control defaults for new files.
- Keep sensitive files private with `chmod 600 file`.
