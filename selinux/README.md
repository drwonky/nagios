# nagios/nagiosql SELinux policies

My nagiosql is setup with /usr/local/nagios/etc/nagiosql as the directory where it writes config files.

I had to set these contexts to get nagios and nagiosql to play nice on Fedora Server 32 (RHEL 8 equiv)

`semanage fcontext -a -t httpd_sys_rw_content_t '/var/www/html/nagiosql/config/.*'
semanage fcontext -a -t httpd_sys_rw_content_t '/usr/local/nagios/etc/.*'
restorecon -F -Rv /usr/local/nagios/etc
restorecon -F -Rv /var/www/html/nagiosql/config`

To install the custom policies, which are a combination of work from sealert, then ausearch and manual editing of the .te files, plust the -fixes came from stackoverflow (with editing to fix erroneous file directives).

`semanage -i my-*.pp`

