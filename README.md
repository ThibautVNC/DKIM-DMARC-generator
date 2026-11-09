<div align="center">

# DKIM/DMARC Helper

**Fix Microsoft 365 mail rejected by Outlook.com / Hotmail. From diagnosis to customer email in six steps.**

<br>

<a href="https://thibautvnc.github.io/DKIM-DMARC-generator/">
  <img src="https://img.shields.io/badge/Open%20the%20tool-%E2%86%92-1f5fbf?style=for-the-badge&logo=microsoftexchange&logoColor=white" alt="Open the tool" height="42">
</a>

<br><br>

![Microsoft 365](https://img.shields.io/badge/Microsoft%20365-Exchange%20Online-0078D4?style=flat-square)
![PowerShell](https://img.shields.io/badge/PowerShell-ready-5391FE?style=flat-square&logo=powershell&logoColor=white)
![Runs locally](https://img.shields.io/badge/Runs-in%20your%20browser-2ea44f?style=flat-square)

</div>

---

## When to use it

Emails from a Microsoft 365 tenant to `@hotmail.com`, `@outlook.com`, `@live.com` or `@msn.com` fail, and the message trace shows:

```
550 5.7.1 Message rejected: Message lacks SPF/DKIM/DMARC Auth Records
```

Outlook.com rejects mail from domains that aren't fully authenticated. In most cases SPF is fine, but **DKIM and DMARC are missing**.

## How it works

| Step | What you get |
| :---: | --- |
| **1 · Domain** | Automatic check of the public MX, SPF, DMARC and DKIM records, with warnings for mixed MX providers and SPF lookup limits |
| **2 · Confirm error** | PowerShell commands to connect to the right tenant and confirm the error in the message trace |
| **3 · DKIM values** | Command to generate the tenant's DKIM keys. Paste the output and the tool validates it against the domain |
| **4 · DNS records** | The exact records to add (DKIM CNAMEs, DMARC, and SPF if it's missing) with copy buttons |
| **5 · Email customer** | DNS host detected from the name servers, plus a ready-to-send email with the records |
| **6 · Finish** | Commands to enable DKIM and verify, a live DNS re-check, the confirmation email, the time entry and troubleshooting |

## Requirements

- Exchange Online PowerShell (`Install-Module ExchangeOnlineManagement`)
- Admin or delegated (GDAP) access to the customer's tenant

## Why can't the DKIM records be generated from the domain name?

The CNAME values contain the **tenant name**, which isn't always the same as the domain, plus a **partition** assigned by Microsoft:

```
selector1-customer-com._domainkey.customer.onmicrosoft.com            older tenants
selector1-customer-com._domainkey.customer.a-v1.dkim.mail.microsoft   newer tenants (a-v1, b-v1, r-v1, ...)
```

A wrong value doesn't give an error, DKIM simply won't work. That's why the tool asks for the output of `Get-DkimSigningConfig` and warns you when it doesn't match the domain, for example when you're connected to the wrong tenant.

## Privacy

Everything runs locally in your browser. The only external requests are public DNS lookups via Google and Cloudflare DNS-over-HTTPS. Nothing is stored or sent anywhere else.
