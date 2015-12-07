Brief Description
=================
``snapbak`` is a very simple tarsnap_ frontend. Main features:

- No config file needed; completely driven by command line
- Do hourly, daily, weekly, monthly backup with N sets per type
- Deletes older archives (older than N sets)

.. _tarsnap: http://tarsnap.com/

Requirements
------------
* Python 2.7.x (on any supported platform)
* Tested on:
    - Debian Linux amd64 (testing, unstable)
    - OpenBSD 5.7, 5.8 - amd64, i386
    - OS X Mavericks, OS X Yosemite

Installation
------------
Copy the ``snapbak`` script to your preferred location in ``$PATH``. I put
this in ``$HOME/bin``.

Usage
-----
Brief usage::

    snapbak Keyfile Archive hourly|daily|weekly|monthly [Max-Sets] Dir [Dir ...]

Positional arguments::

    Keyfile     Tarsnap keyfile
    Archive     The tarsnap archive prefix
    type        Backup type; one of 'hourly', 'daily', 'weekly' or 'monthly'
    Dir         One or more directories to backup
    Max-Sets    An integer argument denoting the maximum number of previous
                backups to retain.

If ``Max-Sets`` is not provided, the program uses the following
defaults:

- Hourly:  24 
- Daily:   10
- Weekly:   6
- Monthly: 14

If you have a directory name that can be interpreted as an
integer and thus confused for "Max-Sets", you can disambiguate by
providing a valid "Max-Sets" value or "-" if you want to use the
program supplied defaults.

Optional arguments::

    -h, --help          show this help message and exit
    -n, --dry-run       Do a dry-run, don't actually commit things [False]
    -v, --verbose       Show verbose progress messages [False]
    -c D, --cachedir D  Use 'D' as the tarsnap cache dir []
    -V                  Show version information and quit

The archive name in the tarsnap cloud is derived as ``Archive-Type-Tstamp``; where:

- ``Archive`` is the archive name prefix from the command line
- ``Type`` is the backup type (daily, weekly etc.)
- ``Tstamp`` is the current date, time in the format YYYY-MMM-DD-hh-mm; where:
  YYYY: four digit year, MMM: short month name, DD: two digit date,
  hh: two digit hour in 24 hour format, mm: two digit minute.


Examples
========
- Backup dirA, dirB identified by 'work' and keep last 7 days worth of
  daily backups::

      snapbak /path/to/Keyfile.key work daily 7 dirA dirB

- Backup directories *10*, *20* identified by ``photos`` and keep
  last 10 weeks worth of weekly backups::

      snapbak /path/to/Keyfile.key photos weekly 10 10 20

  In the above example, the first ``10`` is the number of backup sets
  and the second *10* is the directory name.

- Do a monthly backup of directories *10*, *20* identified by the prefix ``foo``
  and use the program defaults for number of retained backups::

      snapbak /path/to/Keyfile.key foo monthly - 10 20


FAQ
===
- How do I know which archives are stored in the cloud?
    ``tarsnap --keyfile /path/to/Keyfile.key --list-archives``

- Why do you need to do hourly backups?
    I don't know. But if you do, ``snapbak`` supports it.


- How many daily, weekly and monthly sets do I need to keep?
    It depends on your needs. I use the following:

    - 10 daily backups
    - 6 weekly backups
    - 14 monthly backups

    And no, I don't use hourly backups.


.. vim:ft=rst:notextmode:expandtab:tw=74:sw=4:ts=4:
