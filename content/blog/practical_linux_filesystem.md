---
title: A Practical Guide to the Linux Filesystem
date: 2026-01-01
authors:
  - name: gailhantson
    link: https://github.com/gailhantson
    image: https://avatars.githubusercontent.com/u/146262022?v=4
summary: Summary here.

---

<a title="Dhanusha Dhananjaya, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Linux_file_system_foto_no_exif_(1).jpg"><img width="512" alt="Linux file system foto no exif (1)" src="https://upload.wikimedia.org/wikipedia/commons/4/4b/Linux_file_system_foto_no_exif_%281%29.jpg?20200924215412"></a>

## Learning the Filesystem Without Guessing

This guide is practical because I want to understand how the Linux filesystem works in everyday use. The goal is to understand it well enough to stop guessing when something goes wrong.

I am writing this article as an investigation. It follows my process of learning how the filesystem behaves as I use it, rather than trying to explain every detail or rule.

This approach is especially useful in a homelab, where small mistakes can break services or erase data. Understanding where things live and who owns them makes systems easier to rebuild and maintain.

Sources I used while learning are linked throughout the guide. The focus is on what I can observe and test on a running Linux system.

To begin, it helps to be clear about what I mean by the term “Linux filesystem.”

## What "Linux Filesystem" Means (and Doesn't)

The term “Linux filesystem” can be confusing because Linux supports many different filesystems. There is no single filesystem used by all Linux systems. In practice, most desktop and server systems behave in similar ways.

This guide does not try to list or compare every filesystem Linux can use. Instead, it focuses on common behavior seen on Debian, Ubuntu, and Linux Mint. These are popular beginner distributions, and they usually use the ext4 filesystem. Because of this, they organize files in similar and predictable ways.

For clarity, this guide assumes the following:

- Linux supports many filesystem types
- There is no single “Linux filesystem”
- Debian, Ubuntu, and Linux Mint are common beginner systems
- These systems usually use ext4
- ext4 provides a shared baseline for learning

## One Big Tree

Linux uses a single directory tree that starts at /. All files and folders exist somewhere under this root.

This is different from Windows, where each drive has its own letter, such as C: or D:. In Linux, storage devices do not get their own letters. They are connected into the existing tree.

When a USB drive or disk is added, it appears as a directory inside the tree. This model affects how paths work and how files are located.

<a title="GNOME-Team, GPL &lt;http://www.gnu.org/licenses/gpl.html&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Filesystem_Hierarchy_Standard.png"><img width="512" alt="Filesystem Hierarchy Standard" src="https://upload.wikimedia.org/wikipedia/commons/0/08/Filesystem_Hierarchy_Standard.png?20111024112321"></a>

This model changes how you think about file locations:

- Files are identified by their path, not by a drive
- Storage devices are part of the same structure
- A folder can represent a disk, a USB drive, or the system itself
- Knowing the path tells you where something belongs

## Your Stuff, the System's Stuff, and Shared Territory

Because all files live in the same tree, Linux needs a way to separate responsibility. Some files are meant to be changed by the user. Some are controlled by the system. Others are shared by programs. Understanding this separation helps prevent mistakes.

Not all files are equal. Files exist for different reasons, and they are treated differently by the system. 

- Some files hold personal data. 
- Some files make the system work. 
- Some files store settings or state for programs.

Responsibility is the main way these files are organized:

- User files are placed where the user has control
- System files are placed where changes are restricted. 
- Shared files are placed where many programs can safely access them.

This mental model helps explain many common problems. It explains why some files can be edited freely and others cannot. It explains why certain actions require extra permission. It also explains why changing the wrong file can affect the entire system.

By learning which parts of the filesystem belong to which role, it becomes easier to know what is safe to touch and what should be left alone.

## The Places You Need to Recognize

Linux systems contain many directories, but most users only interact with a small number of them. This section focuses on the locations that are most commonly encountered during normal use and troubleshooting.

These are not all of the directories in a Linux system. They are the ones that matter most in practice, especially when trying to understand where files live and what might break.

| Location           | Used for in practice                 | What usually breaks if you touch it  |
| ------------------ | ------------------------------------ | ------------------------------------ |
| `/home`            | Personal files and user settings     | Mostly affects one user              |
| `/etc`             | System-wide configuration files      | Services may fail to start           |
| `/usr/bin`, `/bin` | Programs and system commands         | Commands may stop working            |
| `/var`             | Logs, caches, and changing data      | Services may fill disks or crash     |
| `/tmp`             | Temporary files                      | Usually safe; files may be recreated |
| `/media`, `/mnt`   | Mounted drives and removable storage | Data may disappear if unmounted      |

Recognizing these locations provides a basic map of the filesystem. It does not explain everything, but it covers the places most likely to be touched, edited, or involved when something goes wrong.

With this map in place, it becomes easier to understand how programs use the filesystem and why their files are spread across different locations.

## How Programs Use the Filesystem

Programs use the filesystem in many different ways. The exact details depend on the program, the distribution, and how the system is set up.

The steps below are a simplification. They are not meant to describe every case or exact process. They show a common pattern that helps explain why program files are spread across the filesystem.

1. A program’s main executable is placed in a system directory such as ```/usr/bin```.

2. Default configuration files are placed in a shared location, often under ```/etc```.

3. User-specific settings are stored in the user’s home directory.

4. Logs and changing data are written to ```/var```.

5. Temporary files are created in ```/tmp``` as needed.

This pattern helps separate responsibility. It allows the system to protect important files while still letting users change their own settings.

{{< callout type="info">}}

**Info: Example — Following One Program’s Files**

Pick a program you already use, such as ssh, nano, or curl. You are not trying to understand everything it does. The goal is only to notice where its files appear.

1. Look for the program’s executable in ```/usr/bin```.
2. Then check ```/etc``` for any configuration files related to it.
3. If you run the program as a user, look in your home directory for user-specific settings.
4. Finally, check ```/var``` for logs or other changing data.

You may not find files in every location. That is expected. The purpose of this activity is to see that one program can be spread across multiple parts of the filesystem, each with a different role.

{{< /callout >}}

## Why "Permission Denied" Is a Feature

Linux uses permissions to control who can change which files. This is not meant to block users. It is meant to protect the system.

Each file has an owner and a set of rules. These rules decide who can read, write, or run the file. Most system files are owned by the system, not by individual users.

Because of this, many files are locked down by default. This prevents accidental changes that could break the system. It also protects shared files from being changed by the wrong program or user.

Permissions reflect responsibility. User-owned files can be changed freely. System-owned files require extra permission. When the system says “permission denied,” it is signaling that the file is protected for a reason.

Understanding this makes permission errors easier to read. Instead of being confusing, they become a sign that the system is working as designed.

## When Things Go Wrong (and What the Filesystem Is Telling You)

Problems are often the fastest way to learn how the filesystem works. When something breaks, the location of the failure usually points to the cause.

### Editing the Wrong File

Editing a system file can change how the whole system behaves. If a service stops working after a file change, the location of that file often explains why. Files under system directories affect more than one user.

### Deleting a Config and Watching a Reset

Many programs recreate configuration files if they are missing. When a config file is deleted and the program resets, it shows that the file stored settings, not program logic. This behavior helps separate settings from code.

### Running Out of Space in `/var`

The `/var` directory stores data that changes over time, such as logs. If `/var` fills up, programs may fail even if other parts of the disk have space. This points to how storage is divided by purpose.

### Losing a Mounted Drive

When a mounted drive disappears, the files stored on it also disappear from the tree. The paths still exist, but the data is no longer attached. This shows how storage devices are connected into the filesystem.

### Reading Failures as Signals, Not Mysteries

Errors often describe the filesystem’s rules. Permission errors, missing files, and full disks all point to specific locations and responsibilities. Reading these failures as signals makes problems easier to understand and fix.

## Why This Matters in a Homelab

I use Linux in a homelab, where systems are changed and rebuilt often. In this setting, understanding the filesystem reduces risk.

When file locations are clear, it is easier to know what to back up. Personal data and configuration files usually matter most, while many system files can be replaced.

The filesystem also shows what is safe to remove. Logs, caches, and temporary files are often disposable. Knowing this prevents unnecessary caution.

This knowledge makes rebuilding systems easier. I can restore only what matters and allow the rest to be recreated.

Clear filesystem boundaries also support cleaner system design. Services can be separated and storage can be planned with fewer assumptions.

## What You Can Now Predict

After writing and testing this guide, I can look at a file path and make better guesses. I can tell who is responsible for it, whether it is safe to touch, and what might break if it is removed.

Linux still has complexity, but it no longer feels random. The filesystem provides clues, and those clues explain much of what the system is doing.

## References Used in This Investigation

- Articles, wikis, videos
- How to keep learning beyond this guide