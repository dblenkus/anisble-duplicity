ansible-backup
==============

Install Duplicity 0.7.x and configure it to make automatic backups  of
selected files and databases to Amazons S3.

Requirements
------------

The appropriate versions of `mondodump` and `pg_dump` need to be
installed onthe machine, where the backup script is run.
The `tar` and `gzip` tools must be installed on the machine, where the
backup script is run.

Role Variables
--------------

+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
|                Name                |   Type   |                Description                | Mandatory |              Default               |
+====================================+==========+===========================================+===========+====================================+
| ``backup_aws_key_id``              |  string  | AWS key id - exported to                  |    yes    |                                    |
|                                    |          | ``AWS_ACCESS_KEY_ID`` environmental       |           |                                    |
|                                    |          | variable and used for S3 authentication   |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``vaulted_backup_aws_key``         |  string  | AWS key - exported to                     |    yes    |                                    |
|                                    |          | ``AWS_SECRET_ACCESS_KEY`` environmental   |           |                                    |
|                                    |          | variable and used for S3 authentication   |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``vaulted_backup_passphrase``      |  string  | passphrase used to encrypt backup         |    yes    |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_backup_sources``          |  string  | list of paths to backup                   |    yes    |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_backup_dest``             |  string  | destination of the backup. At the moment, |    yes    |                                    |
|                                    |          | only AWS S3 is supported.                 |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_log_file``                |  string  | location of the log file                  |     no    | ~/duplicity.log                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_full_if_older_than``      |  string  | create full backup if last last backup is |     no    | 30D                                |
|                                    |          | older                                     |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_report_email``            |  string  | send report via email if set              |     no    |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_report_email_subject``    |  string  | subject of report email                   |     no    | Backup report                      |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_create_cronjob``          | boolean  | create cronjob for backup                 |     no    | true                               |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_user``                    |  string  | name of the backup user to create         |     no    | backup                             |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_user_shell``              |  boolean | indicate if ``backup``user will have      |     no    | false                              |
|                                    |          | shell or not.                             |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_backups_dir``             |  string  | Directory where to store backups. If it   |     no    | backups                            |
|                                    |          | is not an absolute path, it will be       |           |                                    |
|                                    |          | treated as relative to `backup_user`'s    |           |                                    |
|                                    |          | home directory                            |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_frequency``               |  string  | frequency of running the backup script as |     no    | daily                              |
|                                    |          | NOTE: It should be one of the valid       |           |                                    |
|                                    |          | values of ``special_time`` paramater of   |           |                                    |
|                                    |          | the `cron module`__                       |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_keep_number``             |  integer | minimal number of backups to keep         |     no    | 10                                 |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_keep_days``               |  integer | minimal number of days for which to keep  |     no    | 90                                 |
|                                    |          | the backups                               |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+

.. __: http://docs.ansible.com/cron_module.html


PostgreSQL configuration
~~~~~~~~~~~~~~~~~~~~~~~~

+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
|                Name                |   Type   |                Description                | Mandatory |              Default               |
+====================================+==========+===========================================+===========+====================================+
| ``backup_postgresql_host``         |  string  | PostgreSQL server's host name             |     yes   |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_postgresql_port``         |  integer | Port on which PostgreSQL server is        |     yes   |                                    |
|                                    |          | listening                                 |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_postgresql_user``         |  string  | Name of the user to use to connect to the |     yes   |                                    |
|                                    |          | PostgreSQL server                         |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_postgresql_password``     |  string  | Password to authenticate                  |     yes   |                                    |
|                                    |          | ``backup_postgresql_user`` to the         |           |                                    |
|                                    |          | PostgreSQL server                         |           |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
| ``backup_postgresql_database``     |  string  | Name of the PostgreSQL database to backup |     yes   |                                    |
+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+


SSH configuration
~~~~~~~~~~~~~~~~~

+------------------------------------+----------+-------------------------------------------+-----------+------------------------------------+
|                Name                |   Type   |                Description                | Mandatory |              Default               |
+====================================+==========+===========================================+===========+====================================+
| ``backup_authorized_key``          |  string  | public SSH key added to ``backup_user``'s |     yes   |                                    |
|                                    |          | ``~/.ssh/authorized_keys`` file           |           |                                    |
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
         - { role: domenblenkus.backup }

License
-------

Licensed under the GPLv3 License. See the COPYING file for details.

Author Information
------------------

Domen Blenkuš
Tadej Janež
