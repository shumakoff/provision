## Autoprovision for SNR VoIP Phones
### with a little help from Asterisk

This script helps to generate configuration files for SNR VoIP Phones. 

Central provisioning is good and all, but sometimes you need to have some specific settings for certain phones. This script allows you to have such custom settings in config file.
Script allows you to customize settings for SIP accounts that bind to a phone via "description" field in sip.conf. 

Parameters go in sip.conf. Line with parameters must start with ";;; ". 
You can check for all available config options in templates/```<model>```.template.
You must specify MAC-address for all managed SIP-accounts in the "description" field along with the template that is used by phone binded to this SIP-account, for example ";;; Template=SNR-VP-7030"), without file name extension.

## Examples

Example of minimal working configuration:
```
[512](office)
;;; Template=SNR-VP-7030
    description=4c3b7400a9c2
    secret=secret
    callerid="512"
```

Example of two SIP-accounts, each of which with a custom ringtone:
```
[587](office)
;;; Template=SNR-VP-7030
;;; Ring_Type=8
    description=4c3b7400ecae
    secret=secret
    callerid="587"

[618](office)
;;; Template=SNR-VP-7030
;;; Ring_Type=9
    description=4c3b7400ecac
    secret=secret
    callerid="618"
```

After filling all of the required fields in sip.conf you can generate config file by running ```provision --sip <your_sip> --verbose```.
Generated config file will be placed in ```output_dir``` from ```provision.conf```. Please check ```provision.conf``` for more options before running the script.
