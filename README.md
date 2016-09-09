dotqmail
=========

The role will set up the dotqmail files in ansible users home for netqmail server as it is used for example on uberspace.de.
*Make sure you have made a backup of your dotqmail files before running this role since it will overwrite or delete them without any further request!!!*

Requirements
------------

See variables section what could be configured. The default configuration only provides basic functionality and does not covers any needs a normal user would have.

Role Variables
--------------

* dotqmail_rootfile  This list of lines is used as content of the root dotqmail file ".qmail" which is treatened separately since it has no extention (and therefore no valid key). Per default it will redirect mails to ./Maildir/ which can be simply overwritten e.g. in inventory files.

* dotqmail_config_files  Can be configured as a dict of lists were the keys are the dotqmail file extentions you like to have and the list entries (which should be strings) are the redirection lines to add to that file
  Example:
    dotqmail_config_files:
      "info" : ["./Maildir/"]
      "mail" : ["./Maildir/", "mail@example.com"]

  The example above will create two dotqmail files ".qmail-info" and ".qmail-mail". The both will redirect the Mails to users Maildir while the latter one will also redirect the mail to address mail@example.com. See (https://wiki.uberspace.de/mail:dotqmail) for more information about dotqmail files and redirection lines syntax.

* dotqmail_default_files  Has roughly the same function as dotqmail_config_files with the *important* difference that it will be combined with the one above to generate the actual working dict and items here will be overwritten by items of dotqmail_config_files if they use the same extention/dict-key. This is present to enforce basic conformity with RFC 2142.

* dotqmail_file  This is the actual dict we work on and normally *should not be changed directly*. It is the combination of dotqmail_config_files over dotqmail_default_files.

* dotqmail_prefix  This is the prefix used to detect the dotqmail filename. By default this is ".qmail-" and normally *should not be changed*.

Dependencies
------------

There are currently no additional depencies.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: dotqmail

License
-------

GPLv3

Author Information
------------------

Copyright 2016 Jonathan Golder jonathan@golderweb.de https://golderweb.de/
