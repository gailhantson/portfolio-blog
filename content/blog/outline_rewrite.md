---
title: A Practical Outline Rewrite
date: 2026-01-01
authors:
  - name: gailhantson
    link: https://github.com/gailhantson
    image: https://avatars.githubusercontent.com/u/146262022?v=4
summary: This artifact compares an initial outline with a revised outline and explains how changes were made to better align the structure with the goals of the article.


---

## Introduction

This document shows how an outline changed over time. It compares an early outline with a revised one. The goal is to explain how the structure was improved to better match the purpose of the article.

## An Impractical Outline

---

This outline is an early draft. It is accurate but not very useful. It focuses on definitions and lists instead of how people actually use a Linux system.

The outline tries to cover many topics. It explains what things are, but not how they behave. This makes it harder for a reader to apply the information.

### Introduction to File Systems

- Definition of a filesystem
- Brief history of filesystems
- Why filesystems matter

### Types of Filesystems

- FAT
- NTFS
- ext4
- ZFS
- Btrfs
- XFS
- Other Linux-supported filesystems

### Linux Filesystem Overview

- What is "the Linux filesystem"
- Filesystem hierarchy standard (FHS)
- Everything is a file

### Linux Directory Structure

- ```/```
- ```/bin```
- ```/sbin```
- ```/usr```
- ```/etc```
- ```/var```
- ```/home```
- ```/tmp```
- ```/media```
- ```/mnt```

### Permissions and Ownership

- Users and groups
- Read, write, execute
- ```chmod```, ```chown```

### Common Filesystem Commands

- ```ls```
- ```cd```
- ```pwd```
- ```mount```
- ```df```
- ```du```

### Differences Between Linux and Windows Filesystems

- Drive letters vs root directory
- NTFS vs ext4

### References and Further Reading

- Wikipedia
- Arch Wiki
- TLDP
- Blog posts and videos

## A Practical Outline

---

This outline is focused on how the filesystem is used in real situations. It limits scope to common Linux systems and shared behavior.

The sections are organized around questions a user might ask. The outline emphasizes where files live, who owns them, and what happens when something goes wrong.

### Learning the Filesystem Without Guessing

- Why this is an investigation, not a reference
- What "practical" means in this guide
- What confidence looks like at the end

### What "Linux Filesystem" Means (and Doesn't)

- Linux supports many filesystems
- Why we are *not* cataloging them
- Focusing on Debian / Ubuntu / Mint behavior
- ext4 as the shared baseline

### One Big Tree

- Everything lives under ```/```
- No drive letters
- How disks and USB drives are mounted into the tree
- Why this changes how you think about "where things are"

### Your Stuff, the System's Stuff, and Shared Territory

- Files are not equal
- Responsibility as the organizing principle
- Why this mental model prevents mistakes

### The Places You Need to Recognize

- ```/home```
- ```/etc```
- ```/ur/bin``` and ```/bin```
- ```/var```
- ```/tmp```
- ```/media``` and ```/mnt```
- What each is *for* in practice
- What usually breaks if you touch them

### How Programs Use the Filesystem

- Installing a program scatters files on purpose
- Binaries vs configs vs state vs logs
- Tracing one program as an example

### Why "Permission Denied" Is a Feature

- Ownership and safety rails
- Why most things are locked down
- How permissions reflect responsibility

### When Things Go Wrong (and What the Filesystem Is Telling You)

- Editing the wrong file
- Deleting a config and watching a reset
- Running out of space in /var
- Losing a mounted drive
- Reading failures as signals, not mysteries

### Why This Matters in a Homelab

- Knowing what to back up
- Knowing what's disposable
- Rebuilding systems with confidence
- Making cleaner architecture decisions

### What You Can Now Predict

- Who owns a path
- Whether it's safe to touch
- What breaks if it disappears
- Why Linux is behaving the way it is

### References Used in This Investigation

- Articles, wikis, videos
- How to keep learning beyond this guide

## What changed?

The outline was rewritten to reduce scope and remove unnecessary detail. Topics that required deep background knowledge were removed or de-emphasized.

The revised outline changes the order of sections. It introduces behavior first and definitions later. It also shifts focus from listing features to explaining outcomes and consequences.

## Read the full article

Read the full article - [A Practical Guide to the Linux Filesystem](/blog/practical_linux_filesystem) - to see how the structure supports practical understanding.