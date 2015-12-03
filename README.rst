Brief Description
=================
``snapbak`` is a very simple tarsnap frontend. Main features:

- No config file needed; completely driven by command line
- Do hourly, daily, weekly, monthly backup with N sets per type
- Deletes older archives (older than N sets)

Usage
=====
::
    snapbak Keyfile Archive hourly|daily|weekly|monthly [Max-Sets] Dir [Dir ...]

Positional arguments::

    Keyfile             Tarsnap keyfile
    Archive             The tarsnap archive prefix
    type                Backup type; one of 'hourly', 'daily', 'weekly' or 'monthly'
    Dir                 One or more directories to backup

Optional arguments::

    -h, --help          show this help message and exit
    -V,                 show version information and quit
    -n, --dry-run       Do a dry-run, don't actually commit things [False]
    -v, --verbose       Show verbose progress messages [False]
    -c D, --cachedir D  Use 'D' as the tarsnap cache dir []


Examples
========
Backup dirA, dirB identified by 'work' and keep last 7 days worth of
daily backups::

  snapbak /path/to/Keyfile.key work daily 7 dirA dirB

Backup directories *10*, *20* identified by ``photos`` and keep
last 10 weeks worth of weekly backups::

  snapbak /path/to/Keyfile.key photos weekly 10 10 20

In the above example, the first ``10`` is the number of backup sets
and the second *10* is the directory name.

