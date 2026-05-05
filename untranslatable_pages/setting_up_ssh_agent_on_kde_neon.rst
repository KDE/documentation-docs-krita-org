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

1) Make sure you remove all explicit calls to ``ssh-agent`` in your ``.bashrc`` and ``.bash_profile`` files.

2) Disable ssh support in the GPG Agent service:

    1) Comment out line `enable-ssh-support` in `~/.gnupg/gpg-agent.conf`
    
    2) Disable the ssh-related socket as well:

        .. code:: bash

            systemctl --user stop gpg-agent-ssh.socket
            systemctl --user disable gpg-agent-ssh.socket
            systemctl --user mask gpg-agent-ssh.socket

3) Create ssh-agent service. 

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

4) Reload the systemd daemon

    .. code:: bash

        systemctl --user daemon-reload

5) Start the service

    .. code:: bash

        systemctl --user start ssh-agent.service

6) Check if everything loaded correctly:

    .. code:: bash

        systemctl --user status ssh-agent.service

7) OpenSSH's `agent-launch` uses DBus service to push variables into the user's environment. You may need to reboot the entire system to make sure the environment variable is properly loaded. Check the content of `$SSH_AUTH_SOCK` in your shell and compare it with the values in the status report of the service to verify your changes.
