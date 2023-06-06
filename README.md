# iRedMail-exclusions-plugin
This plugin contains exclusion rules to fix false positives when using [iRedMail](https://iredmail.org/) and [CoreRuleSet](https://github.com/coreruleset/coreruleset/). This plugin support Roundcube Webmail, SOGo Groupware, and iRedAdmin admin panel (Open Source Edition).

**Note:** this plugin is designed to be used for an iRedMail email server, if you are using a different email server (eg. Mailcow, Zimbra, Mailu) or built your own from scratch then this plugin may not work correctly.

## Requirements
- CRS Version 4.0 or newer
- ModSecurity compatable Web Application Firewall

## How to Install
To install the plugin add includes to the path for ``iRedMail-exclusions-config.conf`` and ``iRedMail-exclusions-before.conf`` after ``crs-setup.conf`` but before loading any CRS rules. See below for an example on how to install.
```
Include /path/to/coreruleset/modsecurity.conf
Include /path/to/coreruleset/crs-setup.conf

Include /path/to/coreruleset/plugins/iRedMail-exclusions-config.conf
Include /path/to/coreruleset/plugins/iRedMail-exclusions-before.conf

Include /path/to/coreruleset/rules/*.conf
```
By default, this plugin assumes that your iRedMail is configured to use Roundcube Webmail with iRedAdmin. If your iRedMail is configured differently, then you must inform this plugin how your iRedMail server is configured.

Edit rule ``9518001`` in ``iRedMail-exclusions-config.conf`` file to inform the plugin of how your iRedMail is setup.
```
# Value of 0 = RoundCube Webmail + iRedAdmin open source (Default)
# Value of 1 = SOGo Webmail + iRedAdmin open source 
# Value of 2 = Roundcube Webmail standalone
# Value of 3 = SOGo Webmail standalone
# Value of 4 = iRedAdmin standalone

SecAction \
  "id:9518001,\
   phase:1,\
   pass,\
   nolog,\
   ver:'iRedMail-exclusions-plugin/1.0.0',\
   setvar:'tx.iRedMail-exclusions-plugin-type=0'"
```

## Disabling the plugin
The plugin can be disabled by uncommenting rule ``9518000`` inside ``/plugins/iRedMail-exclusions-config.conf`` or by removing the includes for this plugin.

## Reporting false positives
If you find a false positive that this plugin does not cover then please open a new issue with the following details to make troubleshooting easier:
1. CRS Version
2. ModSecurity/Coraza Version
3. modsec audit logs
4. what caused the false positive

## Disclaimer
This plugin does not support iRedAdmin Pro, although false positive reports are more than welcome for iRedAdmin Pro.
