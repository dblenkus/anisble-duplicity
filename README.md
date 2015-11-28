ansible-duplicity
=================

Install Duplicity 0.7.x and configure it to make automatic backups to
Amazons S3.

Requirements
------------

No special requirements.

Role Variables
--------------

List of variables that has to be set before running role:
  - `duplicity_aws_key_id`: AWS key id - exported to
    `AWS_ACCESS_KEY_ID` environmental variable and used for S3
    authentication
  - `vaulted_duplicity_aws_key`: AWS key - exported to
    `AWS_SECRET_ACCESS_KEY` environmental variable and used for S3
    authentication
  - `vaulted_duplicity_passphrase`: passphrase used to encrypt backup
  - `duplicity_backup_sources`: list of paths to backup
  - `duplicity_backup_dest`: destination of the backup. At the moment,
    only AWS S3 is supported.

List of extra variables:
  - `duplicity_log_file`: location of the log file (default:
    ~/duplicity.log)
  - `duplicity_full_if_older_than`: create full backup if last last
    backup is older (default: 30D)
  - `duplicity_report_email`: send reports via email if set
  - `duplicity_report_email_subject`: subject of reports email
    (default: Backup report)
  - `duplicity_create_cronjob`: create cronjob for backup
  - `duplicity_cron_weekday`: `weekday` setting for cronjob (default: *)
  - `duplicity_cron_day`: `day` setting for cronjob (default: *)
  - `duplicity_cron_hour`: `hour` setting for cronjob (default: 1)
  - `duplicity_cron_minute`: `minute` setting for cronjob (default: 10)

Dependencies
------------

No dependencies.

Example Playbook
----------------

To use the role in your playbook, add something like the following to
the desired play:

    - hosts: servers
      roles:
         - { role: domenblenkus.duplicity }

License
-------

Licensed under the GPLv3 License. See the COPYING file for details.

Author Information
------------------

Domen Blenkuš
