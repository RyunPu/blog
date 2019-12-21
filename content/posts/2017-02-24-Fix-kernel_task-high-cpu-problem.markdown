---
layout: post
title:  "Fix kernel_task high cpu problem"
date:   2017-02-24
categories: ['mac']
tags: ['mac']
---

0. Reboot into recovery mode (Command + R on boot prior to startup chime), select Utilities/Terminal, `csrutil disable` \<Enter\> (repeat process, use `csrutil enable` after removing the file), reboot.

1. Go to About this mac under the apple in the upper left and click on More info

2. Click on system report

3. make a note of what it says after Model Identifier (MacBookPro8,2 is mine).

4. From the Root drive (not home folder): – System  Library – Extensions – IOPlatformPluginFamily.kext (alt-click/View Contents) – Plugins – ACPI_SMC_PlatformPlugin.kext – View Contents – Resources -– find the name from step 3 and move it to a folder that you can find again if needed.

5. Restart and you’re done (other than enabling SIP).
