.. meta::
    :description:
        A manual on setting up ssh-agent to access git repositories

.. metadata-placeholder

    :authors:
        - Dmitry Kazakov <dimula73@gmail.com>
    :license: GNU free documentation license 1.3 or later.

.. _setting_up_ssh_agent_on_kde_neon:

===========================================================
Setting up ssh-agent to access Krita repository on KDE Neon
===========================================================

#) Make sure you remove all explicit calls to ``ssh-agent`` in your ``.bashrc`` and ``.bash_profile`` files.

#) Disable ssh support in the GPG Agent service:

    1) Comment out line `enable-ssh-support` in `~/.gnupg/gpg-agent.conf`
    
    2) Disable the ssh-related socket as well:

        .. code:: bash

            systemctl --user stop gpg-agent-ssh.socket
            systemctl --user disable gpg-agent-ssh.socket
            systemctl --user mask gpg-agent-ssh.socket

#) Remove explicit set up of `SSH_AUTH_SOCK` in `/etc/profile.d/org.kde.neon.ksshaskpass_auth_sock.sh`. Comment-out the contents of the file so that it looked like that:

    .. code:: bash

        # SPDX-License-Identifier: GPL-3.0-only OR LicenseRef-KDE-Accepted-GPL
        # SPDX-FileCopyrightText: 2026 Carlos De Maine <carlosd.kde@gmail.com>

        #  NOTE: Disabled! Will be set by ssh-agent.service!

        # in a wayland seesion the SSH_AUTH_SOCK needs to be set as below
        # in a X11 session this is set automatically and thus does not need to be done here

        # if [ "$XDG_SESSION_TYPE" = "wayland" ]; then
        #   export SSH_AUTH_SOCK="$XDG_RUNTIME_DIR/ssh-agent.socket"
        # fi


#) Create ssh-agent service.

    .. code:: bash

        systemctl --user edit --full ssh-agent.service

    This command will show you an OS-specific template of the service file. You can modify it or just use the following example:

    .. code::

        [Unit]
        Description=OpenSSH Agent
        Documentation=man:ssh-agent(1)
        Before=graphical-session-pre.target
        Wants=dbus.socket
        After=dbus.socket

        [Service]
        ExecStart=/usr/lib/openssh/agent-launch start -- -t 60m
        ExecStopPost=/usr/lib/openssh/agent-launch stop

    If you want to modify the timeout for your SSH keys, change the ``-t 60m`` flag.

#) Reload the systemd daemon

    .. code:: bash

        systemctl --user daemon-reload

#) Start the service

    .. code:: bash

        systemctl --user start ssh-agent.service

#) Check if everything loaded correctly:

    .. code:: bash

        systemctl --user status ssh-agent.service

#) OpenSSH's `agent-launch` uses DBus service to push variables into the user's environment. You may need to reboot the entire system to make sure the environment variable is properly loaded. Check the content of `$SSH_AUTH_SOCK` in your shell and compare it with the values in the status report of the service to verify your changes.
