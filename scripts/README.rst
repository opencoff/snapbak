Useful Scripts
==============
This directory has some scripts and launchd config to help me on OS X.

Briefly:

``do-backup``
    Shell script to take all the essential stuff on OS X (/etc, macports
    stuff, my dotfiles etc.) and stash it in a local directory. 

    The script uses ``snapbak`` to take the latest stashed directory and
    push it into the tarsnap backup cloud. If there is no network connectivity
    (e.g., wifi is not up yet), the script waits for a 5 seconds and
    retries. It gives up after 5 attempts. This one feature helped me immensly
    to ensure that when I wakeup my macbook in the morning, the script waits a
    reasonable time for WiFi to be established before starting the backup..

    The local backup stash is in ``$HOME/backup/osx/HOSTNAME/``
    Daily backups are in ``$BACKUP/daily.0``, monthly backups are in
    ``$BACKUP/monthly.0``.

    The script keeps last 10 daily backups and last 14 monthly backups.
    All files are compressed. My last 10 months of backup and last 10
    days of backup come to a total of 43MB.

    This script takes a single argument indicating the backup type. It
    writes its progress to */tmp/backup.log*.

    **NB #1** This script is NOT usable out-of-the-box. You should edit the top
    part of the script to setup the following:

    - location of backup directory
    - location of tarsnap key

    **NB #2** Many files in ``/etc`` are not accessible unless you are root. So,
    this script re-execs itself with 'sudo' to gain elevated privileges.

``net.herle.dailybak.plist``
    Launchd control file for doing daily backups. It is configured to start a
    backup every day at 8am. ``man launchd.plist`` is your friend. 

    **NB** This control file is configured to store things in *my* home
    directory. Edit it as needed to suit your environment.

``net.herle.monthlybak.plist``
    Launchd control file for doing monthly backups. It is configured to start a
    backup at 7am on the 1st day of every month.

    **NB** This control file is configured to store things in *my* home
    directory. Edit it as needed to suit your environment.

Launchd Integration
-------------------
Edit and copy the two ``.plist`` files into ``~/Library/LaunchAgents``.
Logout and log back in.

You may find it easier to just invoke ``snapbak`` from the launchd control
files above.

.. vim:ft=rst:notextmode:expandtab:tw=74:sw=4:ts=4:
