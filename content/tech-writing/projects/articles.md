---
title: Technical Articles
type: docs
prev: tech-writing/projects/docs_as_code
next: tech-writing/process
weight: 3
---

## A Practical Guide to the Linux Filesystem

<a title="Dhanusha Dhananjaya, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Linux_file_system_foto_no_exif_(1).jpg"><img width="512" alt="Linux file system foto no exif (1)" src="https://upload.wikimedia.org/wikipedia/commons/4/4b/Linux_file_system_foto_no_exif_%281%29.jpg?20200924215412"></a>

A practical, investigative guide to how the Linux filesystem behaves in everyday use. Instead of memorizing rules, this article focuses on observable patterns to help you understand what’s safe to change, what might break, and how to reason about filesystem problems on real systems.

{{% details title="Audience" closed="true" %}}

This article is written for:

* Linux users who are past the very first steps and want to understand *why* things behave the way they do
* Homelab users and self-hosters managing their own systems
* Developers or technical learners who are comfortable using Linux but feel uncertain when troubleshooting filesystem issues

It assumes basic familiarity with Linux concepts (paths, users, commands), but does not require prior knowledge of filesystems as a theory topic.

{{% /details %}}

{{% details title="Approach" closed="true" %}}

The article is structured as an investigation rather than a reference manual.

* Focuses on observable behavior instead of exhaustive rules
* Uses common Debian-based systems (Ubuntu, Debian, Linux Mint) as a practical baseline
* Builds understanding through patterns: responsibility, ownership, and file purpose
* Emphasizes prediction (“what will break if I touch this?”) over memorization

Examples and explanations are grounded in real system behavior, not abstract definitions.

{{% /details %}}

{{% details title="Challenges" closed="true" %}}

Key challenges addressed in this article include:

* Explaining filesystem structure without oversimplifying or overwhelming
* Avoiding distro-specific edge cases while remaining concrete and testable
* Teaching permissions and responsibility as *signals*, not obstacles
* Balancing beginner accessibility with usefulness for real troubleshooting

The article deliberately avoids completeness in favor of clarity and practical reasoning.

{{% /details %}}

Here's a link to the full article: [A Practical Guide to the Linux Filesystem](/blog/practical_linux_filesystem/)


## How to Read and Understand a Linux Command

Image

Description

{{% details title="Audience" closed="true" %}}

{{% /details %}}

{{% details title="Approach" closed="true" %}}

{{% /details %}}

{{% details title="Challenges" closed="true" %}}

{{% /details %}}

Here's a link to the full article: [How to Read and Understand a Linux Command](/blog/linux_commands)
