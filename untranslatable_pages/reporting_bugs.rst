.. meta::
    :description:
        Guide to Reporting Bugs.

.. metadata-placeholder

    :authors: - Boudewijn Rempt <boud@valdyas.org>
    :license: GNU free documentation license 1.3 or later.

.. _bugs_reporting:

==============
Reporting Bugs
==============

Krita is, together with many other projects, part of the KDE community. Therefore, bugs for Krita are tracked in KDE's bug tracker: `KDE's bug tracker <https://bugs.kde.org>`_. The bug tracker is a tool for Krita's developers to help them manage bugs in the software, prioritize them and plan fixes. It is not a place to get user support!

The bug tracker contains two kinds of reports: bugs and wishes. Bugs are errors in Krita's code that interrupt using Krita. Wishes are feature requests: the reporter thinks some functionality is missing or would be cool to have.

Do not just create a feature request in the bug tracker: follow `Feature Requests <https://krita.org/en/item/ways-to-help-krita-work-on-feature-requests/>`_ to learn how to create a good feature request.

This guide will help you create a good bug report. If you take the time to create a good bug report, you have a much better chance of getting a developer to work on the issue. If there is not enough information to work with, or if the bug report is unreadable, a developer will not be able to understand and fix the issue.


.. contents::

Only Report Bugs
----------------

A bug is a problem in Krita's code.

- If you have problems with your drawing tablet, for instance no support for pressure, then that is unlikely to be a problem in Krita's code: it is almost certain to be a problem with your setup or the driver for your tablet.
- If you've lost the toolbox, that's not a bug.
- If you have deleted your work, that is not a bug.
- If Krita works differently from another application, that's not a bug.
- If Krita works differently than you expected, that's not a bug.
- If Krita is slower than you expected, that's not a bug.


- If Krita crashes, that's a bug.
- If a file you save comes out garbled, that's a bug.
- If Krita stops working, that's a bug.
- If Krita stops displaying correctly, that's a bug.


Check the FAQ
-------------

If you've got a problem with Krita, first check the `FAQ <https://docs.krita.org/en/KritaFAQ.html>`_. See whether your problem is mentioned there. If it is, apply the solution. If that doesn't work for you, do not report a bug. Ask for help on `Krita's Forum <https://forums.kde.org>`_.

Ask on Krita's Forum or IRC Chat Channel
-------------------------------------------------------

If uncertain, ask on `Krita's IRC chat channel <https://krita.org/en/irc/>`_ or the `Krita Forum <https://forum.kde.org/krita>`_.

Krita's chat channel is maintained on webchat.freenode.net. Developers and users hang out to discuss Krita's development and help people who have questions.

.. important::
    Most Krita developers live in Europe, and the channel is very quiet when it's night in Europe. You also have to be patient: it may take some time for people to notice your question even if they are awake.


.. admonition:: Also ...

   Krita does not have a paid support staff. You will chat with volunteers, users and developers. It is not a help desk.


But you can still ask your question, and the people in the channel are a friendly and helpful lot.


Use the Latest Version of Krita
-------------------------------

Check Krita's website to see whether you are using the latest version of Krita. There are two "latest" versions:

- Latest stable: check the `Download page <https://krita.org/download/>`_. Always try to reproduce your bug with this version.
- Stable and Unstable Nightly builds. The stable nightly build is built from the last release plus all bug fixes done since the last release. This is called **Krita Plus*** The unstable nightly build contains new features and is straight from the development branch of Krita. This is called **Krita Next**. You can download these builds from the `Download page <https://krita.org/download/>`_.


Check The Bug Tracker for Duplicates
------------------------------------

This can be tricky: many bug reports are very unclear, have misleading subjects or are assigned to the wrong component. The Krita team tries to triage incoming bugs, fixing the subject, the component and asking for more information in case the bug is not clear.

But please do try to check whether a problem has already been reported. If it is, please add your report as a comment to that bug ticket.


Be Complete and Be Completely Clear
-----------------------------------

Give all information. That means that you should give information about your operating system, hardware, the version of Krita you're using and, of course about the problem.

- Operating system: fill in the requisite field in the bug tracker's form
- Version: fill in the requisite field in the bug tracker's form
- Hardware information: copy the information from the :menuselection:`Help --> Show System Information for Bug Reports` or Bug Reports window into your report. Note how many displays you have.
- If you are using a drawing tablet, tell us the brand and type.
- Tell us what kind of image you were working on: the size, the resolution, the color model and channel depth.
- If you are reporting a crash, attach a crash log. Follow `this link <https://docs.krita.org/en/reference_manual/dr_minw_debugger.html#dr-minw>`_ to learn how to get a crash log on Windows. On Linux, follow your distribution's instructions to install debug symbols if you have installed Krita from a distribution package. It is not possible to create a useful crash log with Linux appimages.
- Attach the contents of the :menuselection:`Help --> Show System Information for Bug Reports` dialog to the bug report.


The problem needs to be clearly stated:
- what happened,
- what had you expected to happen instead,
- how the problem can be reproduced.

Give a concise and short description, then enumerate the steps needed to reproduce the problem. If you cannot reproduce the problem, and it isn't a crash, think twice before making the report: the developers likely cannot reproduce it either.

If at all possible, attach your original Krita file (the one that ends in ``.kra``) to the bug report, or if it's too big, add a link for download. If you do that, make sure the file will be there for **years** to come: do not remove it.

If you think it would be useful, you can also attach or link to a video. Note that the Krita developers and bug triagers are extremely busy, and that it takes less time to read a good description and a set of steps to reproduce than it takes to watch a video for clues for what is going on.

When making a video or a screenshot, include the whole Krita window, including the titlebar and the statusbar.




You're Not Done After You Have Filed the Report
-----------------------------------------------

After you have filed your bug, mail will be sent out to all Krita developers and bug triagers. You do not have to go to the chat channel and tell us you created a bug.

When a developer decides to investigate your report, they will start adding comments to the bug. There might be additional questions: please answer them as soon as possible.

When the developer has come to a conclusion, they will **resolve** the bug. That is done by changing the resolution status in the bug tracker. These statuses are phrased in developer speak, that is to say, they might sound quite rude to you. There's nothing that we can do about that, so do not take it personally. The bug reporter should *never* change the status after a developer changed it.

These are the most used statuses:

- Unconfirmed: your bug has not been investigated yet, or nobody can reproduce your bug.
- Confirmed: your bug is a bug, but there is no solution yet.
- Assigned: your bug is a bug, someone is going to work on it. There probably will be a corresponding task on the https://phabricator.kde.org/project/view/8/ developer workboard.
- Resolved/Fixed: your bug was a genuine problem in Krita's code. The developer has fixed the issue and the solution will be in the next release.
- Duplicate: your bug has been reported before.
- Needinfo/WaitingForInfo. You need to provide more information. If you do not reply within a reasonable amount of time the bug will be closed.
- Resolved/Invalid: your report was not about a bug.
- Resolved/Upstream: the issue you observed is because of a bug in a library Krita uses, or a hardware driver, or your operating system. We cannot do anything about it.
- Resolved/Downstream: Only on Linux. The issue you observed happens because your Linux distribution packages Krita in a way that causes problems.

See also our chapter on `Bug Triaging <https://docs.krita.org/en/untranslatable_pages/triaging_bugs.html>`_
