# iRedMail-exclusions-plugin
This plugin comes with exclusion rules to fix false positives when using iRedMail with the CoreRuleSet, currently only Roundcube webmail and iRedAdmin open source is supported.

## Requirements
CRS Version 4.0 or newer

## How to Install
To install the plugin add includes to the path for ``iRedMail-exclusions-config.conf`` and ``iRedMail-exclusions-before.conf`` after ``crs-setup.conf`` but before loading any CRS rules. See below for an example on how to install.
```
Include /path/to/coreruleset/modsecurity.conf
Include /path/to/coreruleset/crs-setup-mail.conf

Include /path/to/coreruleset/plugins/iRedMail-exclusions-config.conf
Include /path/to/coreruleset/plugins/iRedMail-exclusions-before.conf

Include /path/to/coreruleset/rules/*.conf
```
This plugin will automatically be enabled by default once you install it.

## Disabling the plugin
The plugin can be disabled by uncommenting rule ``9517000`` inside ``/plugins/iRedMail-exclusions-config.conf``

## Reporting false positives
If you find a false positive that this plugin does not cover then please open a new issue with the following details to make troubleshooting easier:
1. CRS Version
2. ModSecurity/Coraza Version
3. modsec audit logs
4. what caused the false positive
