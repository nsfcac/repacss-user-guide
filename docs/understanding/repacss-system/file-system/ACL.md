# Access Control Lists (ACLs) - Sharing File Access

## Overview

This document provides an overview of Access Control Lists (ACLs), which allow fine-grained control over file and directory permissions beyond the standard owner, group, and other model. ACLs are commonly used on REPACSS systems to define access for specific users or groups.

---

## What Are ACLs?

ACLs extend the basic permissions by enabling you to:

- Grant different permissions to multiple users or groups.
- Control access without changing a file's primary ownership or group.
- Define default permissions for newly created files within a directory.

Each file or directory can have:

- A set of **access ACLs** (current permissions)
- Optional **default ACLs** (inherited by new items created inside a directory)

---

## Viewing ACLs

To see the ACL entries of a file or directory, use the `getfacl` command:

```bash
getfacl filename
```

**Example output:**

```
# file: example.txt
# owner: bsencer
# group: discl
user::rw-
user:userid:rw-
group::r--
mask::rw-
other::---
```

**Explanation of fields:**

| Field        | Description                                                |
|--------------|------------------------------------------------------------|
| user::       | Permissions for the file owner                            |
| user:userid   | Permissions granted to user `userid`                       |
| group::      | Permissions for the owning group                          |
| mask::       | Maximum effective permissions for named users and groups  |
| other::      | Permissions for all other users                           |

!!! note
  The `mask` acts as an upper limit. For example, if a user has `rwx` permissions but the mask is `rw-`, the effective permissions are `rw-`.

---

## Modifying ACLs

ACLs are modified using the `setfacl` command.

---

### Adding or Modifying Permissions

To grant read and write access to a specific user:

```bash
setfacl -m u:userid:rw filename
```

**Options:**

- `u:USERNAME:PERMISSIONS` — set permissions for a user
- `g:GROUPNAME:PERMISSIONS` — set permissions for a group

**Examples:**

- Grant read-only access to group `research`:

  ```bash
  setfacl -m g:research:r filename
  ```

- Update the mask (limit effective permissions):

  ```bash
  setfacl -m m:rw filename
  ```

---

### Removing ACL Entries

To remove permissions granted to a user:

```bash
setfacl -x u:userid filename
```

To remove group permissions:

```bash
setfacl -x g:research filename
```

---

### Setting Default ACLs

Default ACLs apply automatically to new files and directories created within a directory.

**Example:**

Grant default read and write access to user `userid` for all new files in `project_data`:

```bash
setfacl -d -m u:userid:rw project_data/
```

!tip
  Use `-R` to apply ACLs recursively to all existing files and directories:

```bash
setfacl -R -m u:userid:rw project_data/
```

---

### Removing All ACLs

To remove all extended ACL entries and revert to standard permissions:

```bash
setfacl -b filename
```

---

## Verifying Effective Permissions

After modifying ACLs, use `getfacl` to confirm the changes:

```bash
getfacl filename
```

Review the `mask` entry to ensure the permissions are effective as intended.

---

## Best Practices

- Use ACLs to manage collaborative access to project directories without changing ownership.
- Always verify permissions with `getfacl`.
- Remove unnecessary ACL entries to maintain security and clarity.
- Consider setting default ACLs when multiple users create files in shared directories.

---

## Summary

- **`getfacl`** displays current ACLs.
- **`setfacl -m`** adds or modifies ACL entries.
- **`setfacl -x`** removes specific ACL entries.
- **`setfacl -d`** defines default ACLs for directories.
- **`setfacl -b`** clears all ACLs.

For assistance managing ACLs, please contact REPACSS support.
