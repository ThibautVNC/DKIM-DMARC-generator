# DKIM/DMARC Helper – Outlook/Hotmail rejections

A step-by-step helper for mail that Outlook.com/Hotmail rejects with:

```
550 5.7.1 Message rejected: Message lacks SPF/DKIM/DMARC Auth Records
```

## 👉 [Open the tool](https://<github-user>.github.io/<repo>/)

## Steps

| Step | What happens |
| --- | --- |
| 1. Domain | Enter the domain. Its public MX, SPF, DMARC and DKIM records are checked automatically. |
| 2. Confirm error | PowerShell commands to connect to the right tenant and confirm the error in the message trace. |
| 3. DKIM values | Command to create the DKIM config and get its values. Paste the output into the tool. |
| 4. DNS records | The records to add (DKIM CNAMEs, DMARC, and SPF if it's missing). |
| 5. Email customer | The DNS host is detected from the name servers, with a WHOIS/DNS Belgium link. Ready-to-send email with the records. |
| 6. Finish | Commands to enable DKIM and verify, a public DNS re-check, the confirmation email, the time entry and troubleshooting. |

## Why paste the DKIM output?

The DKIM values can't be derived from the domain name. They contain the tenant name, which isn't always the same as the domain, plus a partition assigned by Microsoft:

```
selector1-customer-com._domainkey.customer.onmicrosoft.com            (older tenants)
selector1-customer-com._domainkey.customer.a-v1.dkim.mail.microsoft   (newer tenants: a-v1 / b-v1 / r-v1 / ...)
```

A wrong value doesn't give an error, DKIM simply won't work. The tool warns you when the pasted values don't match the domain, for example when you're connected to the wrong tenant.

## Enable GitHub Pages

Repo → **Settings → Pages → Source: Deploy from a branch → `main` / root**. After a minute the tool is available at `https://<github-user>.github.io/<repo>/`.

Everything runs locally in the browser. Public DNS lookups use Google/Cloudflare DNS-over-HTTPS. No data is stored or sent anywhere else.
