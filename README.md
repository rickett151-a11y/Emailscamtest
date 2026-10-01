# Spot the Scam

A five-email phishing awareness game for Cybersecurity Awareness Month. Everything is in one file, `spot-the-scam.html`: no external scripts, fonts, images or tracking. It works offline and in any modern browser.

## How it plays

1. **Inspect**: tap the sender's name, links and attachments. The Inspector shows the real address, link destination and file type. Nothing opens.
2. **Choose**: Trust it, Verify another way, or Report to Helpdesk.
3. **Learn**: the clues are highlighted and numbered on the email, with an explanation.
4. **Finish**: a score out of 500 after five emails, with the Helpdesk@wfse.org reminder.

Scoring: best choice 100 points, a safe but not ideal choice 50, a risky choice 0.

Each round draws 2 legitimate emails and 3 suspicious ones from a pool of 8, in random order, so replays differ:

| Email | Type | Best choice |
|---|---|---|
| Microsoft 365 password expiry | Credential phishing | Report |
| Dana Ortiz shared "Q4 Salary Adjustments.xlsx" | Fake shared document | Report |
| Pat Morgan, "Quick favor" | Gift card scam | Report |
| Brightline Supply bank change | Payment change request | Verify |
| Parcel redelivery fee | Delivery fee scam | Report |
| Helpdesk Awareness Month announcement | Legitimate | Trust |
| Expense report approved | Legitimate | Trust |
| Jordan Lee shared "October volunteer schedule" | Legitimate | Trust |

All names, vendors and scam domains are fictional. The legitimate emails assume `wfse.org`, `intranet.wfse.org` and `wfse.sharepoint.com`. Adjust these if your real addresses differ.

## Editing the emails

Open the file in a text editor and find `var EMAILS = [`. Each email has a sender, subject, body, links, the best and acceptable choices, and a list of clues. In the body, `[[key|text]]` makes a link (add `|cta` for a button) and `{{key|text}}` marks a phrase that gets highlighted as a clue. Each clue's `k` matches one of those keys, or `from` for the sender.

## Putting it on SharePoint

SharePoint Online won't run an uploaded `.html` file as a page. On most tenants it downloads instead, because custom scripts are blocked. So the practical routes are:

**1. Host the file elsewhere and embed it (recommended).** Put `spot-the-scam.html` on any small static web host your organization controls, such as Azure Static Web Apps (free tier), an existing internal web server, or an approved site host. Then on the SharePoint page, add the **Embed** web part and paste:

```html
<iframe src="https://YOUR-HOST/spot-the-scam.html" width="100%" height="1000" style="border:0" title="Spot the Scam"></iframe>
```

The host's domain must be allowed in the site's **HTML Field Security** list (Site settings > HTML Field Security). A site owner can add it. If it isn't allowed, the Embed web part will say the site can't be embedded.

**2. SPFx web part.** If you'd rather have it installed inside SharePoint with no outside host, the same HTML and JavaScript can be packaged as an SPFx web part. That needs a SharePoint admin to deploy it to the app catalog. This is more setup, but it is the most "native" option.

**3. Upload as .aspx (not recommended).** Some tenants let you rename the file to `.aspx` and open it from Site Assets, but only when custom script is enabled on that site. Microsoft now discourages this, and the setting can be switched back off automatically.

## What it doesn't do

Scores aren't saved or sent anywhere. Each person sees only their own result. If you want completion tracking, a simple option is to link a short Microsoft Form from the results screen.
