Brief Description
=================
``snapbak`` is a very simple tarsnap frontend. Main features:

- No config file needed; completely driven by command line
- Do hourly, daily, weekly, monthly backup with N sets per type
- Deletes older archives (older than N sets)


Usage::

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

The archive name in the tarsnap cloud is derived as ``Archive-Type-Tstamp``; where:

- ``Archive`` is the archive name prefix from the command line
- ``Type`` is the backup type (daily, weekly etc.)
- ``Tstamp`` is the current date, time in the format YYYY-MMM-DD-hh-mm; where:
   YYYY: four digit year, MMM: short month name, DD: two digit date,
   hh: two digit hour in 24 hour format, mm: two digit minute.


Examples
========
#. Backup dirA, dirB identified by 'work' and keep last 7 days worth of
   daily backups::

  snapbak /path/to/Keyfile.key work daily 7 dirA dirB

#. Backup directories *10*, *20* identified by ``photos`` and keep
   last 10 weeks worth of weekly backups::

  snapbak /path/to/Keyfile.key photos weekly 10 10 20

In the above example, the first ``10`` is the number of backup sets
and the second *10* is the directory name.


FAQ
===
#. How do I know which archives are stored in the cloud?

   ``tarsnap --keyfile /path/to/Keyfile.key --list-archives``

#. Why do you need to do hourly backups?

   I don't know. But if you do - ``snapbak`` supports it.


#. How many daily, weekly and monthly sets do I need to keep?

   It depends on your needs. I use the following:

   - 10 daily backups
   - 6 weekly backups
   - 14 monthly backups

   And no, I don't use hourly backups.



