ansible-duplicity
=================

Install Duplicity 0.7.x and configure it to make automatic backups to
Amazons S3.

Requirements
------------

No special requirements.

Role Variables
--------------

+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
|                Name                |   Type   |                Description                | Mandatory |              Default               |
+====================================+==========+===========================================+===========+====================================+
| ``duplicity_aws_key_id``           |  string  | AWS key id - exported to                  |    yes    |                                    |
|                                    |          | ``AWS_ACCESS_KEY_ID`` environmental       |           |                                    |
|                                    |          | variable and used for S3 authentication   |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``vaulted_duplicity_aws_key``      |  string  | AWS key - exported to                     |    yes    |                                    |
|                                    |          | ``AWS_SECRET_ACCESS_KEY`` environmental   |           |                                    |
|                                    |          | variable and used for S3 authentication   |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``vaulted_duplicity_passphrase``   |  string  | passphrase used to encrypt backup         |    yes    |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_backup_sources``       |  string  | list of paths to backup                   |    yes    |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_backup_dest``          |  string  | destination of the backup. At the moment, |    yes    |                                    |
|                                    |          | only AWS S3 is supported.                 |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_log_file``             |  string  | location of the log file                  |     no    | ~/duplicity.log                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_full_if_older_than``   |  string  | create full backup if last last backup is |     no    | 30D                                |
|                                    |          | older                                     |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_report_email``         |  string  | send report via email if set              |     no    |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_report_email_subject`` |  string  | subject of report email                   |     no    | Backup report                      |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_create_cronjob``       | boolean  | create cronjob for backup                 |     no    | true                               |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_cron_weekday``         |  string  | ``weekday`` setting for cronjob           |     no    | *                                  |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_cron_day``             |  string  | ``day`` setting for cronjob               |     no    | *                                  |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_cron_hour``            |  string  | ``hour`` setting for cronjob              |     no    | 1                                  |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``duplicity_cron_minute``          |  string  | ``minute`` setting for cronjob            |     no    | 10                                 |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+

Dependencies
------------

No dependencies.

Example Playbook
----------------

To use the role in your playbook, add something like the following to
the desired play:

.. code-block:: yaml

    - hosts: servers
      roles:
         - { role: domenblenkus.duplicity }

License
-------

Licensed under the GPLv3 License. See the COPYING file for details.

Author Information
------------------

Domen Blenkuš
