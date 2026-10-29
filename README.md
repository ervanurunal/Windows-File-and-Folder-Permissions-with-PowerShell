## Windows File and Folder Permissions

---

### Overview

This hands-on lab focused on managing user and group permissions on a Windows system using **PowerShell** and the **ICACLS** command.

The lab demonstrated how to:

* Access administrative privileges
* View file and folder permissions
* Grant permissions to users
* Remove permissions from users
* Modify permissions for groups
* Configure read and write access
* Verify permission changes

These are important Windows administration and IT Support skills, and they also provide a foundation for understanding access control in cybersecurity.

---

## Tools & Resources

### Tools Used

* Qwiklabs hands-on lab environment
* Windows Virtual Machine
* Windows PowerShell
* Windows Command Line Interface (CLI)
* `ICACLS`
* Windows File Explorer
* Windows user accounts
* Windows user groups

### Lab Type

Hands-on Windows File and Folder Permissions Lab

### Operating System

Windows

### Main Tool

#### ICACLS

`ICACLS` is a Windows command-line tool used to display and modify access control lists (ACLs) for files and directories.

It can be used to:

* View permissions
* Grant permissions
* Remove permissions
* Modify permissions
* Manage permissions for users and groups

---

### ICACLS Permission Basics

The lab used `ICACLS` to view and modify permissions.

A basic command for viewing permissions is:

```powershell
icacls "C:\Path\To\File"
```

This displays the access control entries associated with the file or directory.

Permissions can then be modified using ICACLS commands.

---
---

### Example 1 — Give a User Read-Only Access

#### Scenario

The file:

```text
C:\Users\Qwiklab\Documents\important_document
```

is currently accessible by the user **Kara** with both read and write permissions.

The goal is to change Kara's permissions so that she has **read-only access**.

---

#### Step 1 — View Existing Permissions

Use `ICACLS` to view the current permissions:

```powershell
icacls "C:\Users\Qwiklab\Documents\important_document"
```

The existing permissions showed that Kara had:

```text
Read
Write
```

![step1](https://i.imgur.com/ZsVPOc3.png)

---

#### Step 2 — Remove Kara's Existing Permissions

Remove Kara's current permissions so they can be configured again.

```powershell
icacls "C:\Users\Qwiklab\Documents\important_document" /remove "Kara"
```

![step2](https://i.imgur.com/RujBTiD.png)
![step2](https://i.imgur.com/5IXh0ya.png)

---

#### Step 3 — Grant Read Permission

Grant Kara read access:

```powershell
icacls "C:\Users\Qwiklab\Documents\important_document" /grant "Kara:(r)"
```

![step3](https://i.imgur.com/19ky92y.png)

---

#### Step 4 — Verify

Run:

```powershell
icacls "C:\Users\Qwiklab\Documents\important_document"
```

Kara should now have:

```text
Read
```

and should no longer have write access.

![step4](https://i.imgur.com/ZhzDa6T.png)

---

### Example 2 — Give a Second User Access

#### Scenario

There is a folder called:

```text
C:\Users\Qwiklab\Secret
```

Initially:

* Kara has Read permission.
* Phoebe does not have permission.

The goal is to:

* Give Phoebe Read permission.
* Give Kara Read and Write permissions.

---

#### Step 1 — View Current Permissions

```powershell
icacls "C:\Users\Qwiklab\Secret"
```

---

#### Step 2 — Grant Phoebe Read Access

```powershell
icacls "C:\Users\Qwiklab\Secret" /grant "Phoebe:(r)"
```

![step2-2](https://i.imgur.com/cKw1P6h.png)

---

#### Step 3 — Give Kara Write Access

Kara already has read access, so write access can be added:

```powershell
icacls "C:\Users\Qwiklab\Secret" /grant "Kara:(w)"
```

---

#### Step 4 — Verify

```powershell
icacls "C:\Users\Qwiklab\Secret"
```

The final permissions should provide:

```text
Kara   → Read + Write
Phoebe → Read
```

![step3-4](https://i.imgur.com/PVuA6ny.png)

---

### Example 3 — Modify Permissions for a Group

#### Scenario

The folder:

```text
C:\Users\Qwiklab\Music
```

has the **Everyone** group with both Read and Write permissions.

The goal is to change the Everyone group's permissions to **Read only**.

---

#### Step 1 — View Existing Permissions

```powershell
icacls "C:\Users\Qwiklab\Music"
```

![step1](https://i.imgur.com/YMv7q7g.png)

---

#### Step 2 — Remove Existing Everyone Permissions

```powershell
icacls "C:\Users\Qwiklab\Music" /remove "Everyone"
```

![step2](https://i.imgur.com/PQNH8KX.png)

---

#### Step 3 — Grant Read Permission

```powershell
icacls "C:\Users\Qwiklab\Music" /grant "Everyone:(r)"
```

---

#### Step 4 — Verify

```powershell
icacls "C:\Users\Qwiklab\Music"
```

The Everyone group should now have:

```text
Read
```

and no Write permission.

![step3-4](https://i.imgur.com/BFLcs4v.png)


---

### Example 4 — Give Authenticated Users Write Access

#### Scenario

The file:

```text
C:\Users\Qwiklab\Documents\not_so_important_document
```

needs to give the **Authenticated Users** group Write access.

---

#### Step 1 — View Current Permissions

```powershell
icacls "C:\Users\Qwiklab\Documents\not_so_important_document"
```

The `Authenticated Users` group is not currently listed.

![step1](https://i.imgur.com/Lr9qr96.png)

---

#### Step 2 — Grant Write Permission

```powershell
icacls "C:\Users\Qwiklab\Documents\not_so_important_document" /grant "Authenticated Users:(w)"
```

---

#### Step 3 — Verify

```powershell
icacls "C:\Users\Qwiklab\Documents\not_so_important_document"
```

The `Authenticated Users` group should now have:

```text
Write
```

![step2-3](https://i.imgur.com/wSwqmv4.png)


---

### Example 5 — Make a File Readable by Everyone

#### Scenario

The file:

```text
C:\Users\Qwiklab\Documents\public_document
```

needs to be readable by all users on the system.

Instead of manually adding every user, the **Everyone** group can be given Read permission.

---

#### Step 1 — View Current Permissions

```powershell
icacls "C:\Users\Qwiklab\Documents\public_document"
```

---

#### Step 2 — Grant Everyone Read Access

```powershell
icacls "C:\Users\Qwiklab\Documents\public_document" /grant "Everyone:(r)"
```

---

#### Step 3 — Verify

```powershell
icacls "C:\Users\Qwiklab\Documents\public_document"
```

The Everyone group should now have:

```text
Read
```

![step1-2-3](https://i.imgur.com/letHWe5.png)

---
---

### Permission Management Workflow

A useful workflow for Windows permission troubleshooting is:

```text
Identify the file/folder
        ↓
Check current permissions
        ↓
Identify the user/group
        ↓
Determine required access
        ↓
Modify permissions
        ↓
Verify permissions
        ↓
Test access
```

This approach helps avoid accidentally granting excessive access.

---
---

### PowerShell / ICACLS Commands Used

| Command                            | Purpose                     |
| ---------------------------------  | --------------------------- |
| icacls <path>.                     | View permissions            |
| icacls <path> /grant "<user>:(r)"  | Grant Read permission       |
| icacls <path> /grant "<user>:(w)"  | Grant Write permission      |
| icacls <path> /remove "<user>"     | Remove a user's permissions |
| icacls <path> /grant "Everyone:(r)"| Grant Everyone Read access  |

---
---

### Skills Demonstrated

#### Windows Administration

* Using PowerShell
* Working with administrative privileges
* Managing file permissions
* Managing folder permissions
* Working with Windows users
* Working with Windows groups

#### Access Control

* Viewing ACLs
* Granting permissions
* Removing permissions
* Modifying user permissions
* Modifying group permissions
* Verifying access permissions

#### Troubleshooting

* Identifying incorrect permissions
* Determining required access
* Applying permission changes
* Verifying configuration changes

---
---

### IT Support Relevance

File and folder permissions are common sources of Windows access problems.

For example, a user might report:

> "I can see the folder, but I can't modify the files."

An IT Support Specialist could investigate:

1. Which user account is being used?
2. What permissions does the user currently have?
3. Is the user part of an appropriate group?
4. Does the user have Read permission?
5. Does the user have Write permission?
6. Are there conflicting permissions?
7. Were the permissions changed successfully?

PowerShell and `ICACLS` can help an IT Support Specialist investigate and modify these permissions.

---
---

### Cybersecurity Relevance

Permissions are an important part of cybersecurity because they help control access to information and resources.

Incorrect permissions can potentially allow users to access or modify information they should not have access to.

Understanding permissions helps security professionals with:

* Access control
* Least privilege
* File security
* User management
* Group management
* Incident investigation
* Windows security administration

---
---

### Troubleshooting Scenario

#### Scenario

A user named Kara tells the IT Support team:

> "I can open the document, but I can't make changes to it."

#### Troubleshooting Approach

First, identify the file and check its permissions:

```powershell
icacls "C:\Path\To\File"
```

Look for Kara's permissions.

If Kara only has:

```text
Read
```

but needs to edit the file, Write permission may need to be granted according to the organization's access requirements.

For example:

```powershell
icacls "C:\Path\To\File" /grant "Kara:(w)"
```

Then verify:

```powershell
icacls "C:\Path\To\File"
```

The important step is to **verify the required access before making changes** and then confirm that the change was successful.

---
---

### Lab Results

During this lab, I practiced modifying permissions for both individual users and groups.

#### Permission Changes

| Resource                    | User/Group          | Final Access |
| --------------------------- | ------------------- | ------------ |
| `important_document`        | Kara                | Read         |
| `Secret`                    | Kara                | Read + Write |
| `Secret`                    | Phoebe              | Read         |
| `Music`                     | Everyone            | Read         |
| `not_so_important_document` | Authenticated Users | Write        |
| `public_document`           | Everyone            | Read         |

---
---

### What I Learned

Through this lab, I learned how to:

* Use PowerShell to manage Windows permissions
* Use `ICACLS` to view permissions
* Grant permissions to users
* Remove permissions from users
* Modify permissions for groups
* Understand Read and Write access
* Verify permission changes
* Understand why groups are useful for access management
* Apply the principle of least privilege

---

### Portfolio Skills

**Windows | PowerShell | ICACLS | File Permissions | Access Control | User Management | Group Management | Troubleshooting | Least Privilege | Cybersecurity**
