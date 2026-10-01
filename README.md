# Spot the Scam

A phishing awareness game for Cybersecurity Awareness Month. Everything is in one file, `spot-the-scam.html`: no external scripts, fonts, images or tracking. It works offline and in any modern browser.

## How it plays

The page opens with a short loading animation (click to skip) and a title menu with Start, Continue (when a level is in progress) and How to play. Each level starts with an intro animation.

Game touches: point pop-ups, a streak counter for correct calls in a row, a shake on risky choices, confetti for 2+ stars, and small synthesized sound effects. Sound starts at 25% volume, with a mute button and volume slider on the menu and in the top bar. The setting is remembered.

Players pick a level: **Easy**, **Medium** or **Hard**. Each play is five emails in a realistic inbox. The **Call Ed** button shows Ed's alpaca (with a Linux penguin on its back) asking "Did you email Helpdesk?"

1. **Check**: click the sender's name to show the full address, hover or click links to see where they really go, and click attachments to see the file type. Nothing opens.
2. **Decide**: Trust it, Verify another way, or Report to Helpdesk.
3. **Learn**: the clues are highlighted and numbered on the email, with an explanation.
4. **Score**: best choice 100 points, a safe but not ideal choice 50, a risky choice 0. Out of 500 per level: 450+ is 3 stars, 300+ is 2 stars, anything else is 1 star.

Progress is saved after every answer in a cookie (with browser storage as a backup), so players can close the page and come back to finish a level. Best scores and stars are kept for a year. "Clear my scores" on the level screen wipes them. Nothing is sent anywhere.

Built for laptop and desktop screens for now.

Each level has a pool of emails, and every play draws five at random: one or two real ones and the rest suspicious, in random order. Many of the scams have spelling or grammar mistakes, especially on Easy. A few real emails have a small typo too, to show that a typo alone doesn't make an email a scam.

| Level | Email | Real or scam | Best choice |
|---|---|---|---|
| Easy | "selected to recieve a $500 gift card" | Scam | Report |
| Easy | "Your mailbox is 99% FULL" from "IT Departmnet" | Scam | Report |
| Easy | Fake ADP "direct deposit SUSPENDED" | Scam | Report |
| Easy | Fake IRS refund, "you are eligable" | Scam | Report |
| Easy | Fake Teams "(3) unread mesages" | Scam | Report |
| Easy | Fake StreamFlix "acount is on hold" | Scam | Report |
| Easy | "Congradulations" bonus letter, .pdf.exe attachment | Scam | Report |
| Easy | ADP "Your pay statement is ready" | Real | Trust |
| Easy | Helpdesk Awareness Month announcement | Real | Trust |
| Easy | Potluck reminder from a coworker (has a small typo) | Real | Trust |
| Easy | Facilities parking lot repaving | Real | Trust |
| Medium | Microsoft 365 password expires in 2 hours | Scam | Report |
| Medium | Pat Morgan "Quick favor" gift cards | Scam | Report |
| Medium | "Q4 Salary Adjustments.xlsx" shared from docshare-files.net | Scam | Report |
| Medium | Voicemail with an .html attachment | Scam | Report |
| Medium | "Ticket closed" from wfse-support.org | Scam | Report |
| Medium | ShopRight order with a callback phone number | Scam | Report |
| Medium | Fake ADP "direct deposit change request" | Scam | Report |
| Medium | ILOVEYOU with LOVE-LETTER-FOR-YOU.TXT.vbs | Scam | Report |
| Medium | Jordan Lee shared "October volunteer schedule" | Real | Trust |
| Medium | HR open enrollment | Real | Trust |
| Medium | Helpdesk scheduled maintenance | Real | Trust |
| Medium | Helpdesk "password expires in 7 days" | Real | Trust |
| Hard | Brightline Supply bank change (real vendor address) | Possibly real, high risk | Verify |
| Hard | VPN re-registration from wfse.co | Scam | Report |
| Hard | Sam Whitaker reply with an .htm "report" | Scam | Report |
| Hard | "Please sign" policy from wfse-hr.org | Scam | Report |
| Hard | Past-due invoice from brightline-suppply.com | Scam | Report |
| Hard | MFA re-enrollment by QR code | Scam | Report |
| Hard | W-2s for all staff, reply-to an outside address | Scam | Report |
| Hard | Org chart "shared" to a fake SharePoint link | Scam | Report |
| Hard | ADP W-2 choice with a deadline | Real | Trust |
| Hard | Brightline Supply "order has shipped" | Real | Trust |
| Hard | HR survey on Microsoft Forms | Real | Trust |

All names, vendors and scam domains are fictional. The real emails assume `wfse.org`, `intranet.wfse.org` and `wfse.sharepoint.com`, and that payroll emails come from ADP at `noreply@adp.com` (MyADP at my.adp.com). Adjust these if your real addresses differ.

## Editing the emails

Open the file in a text editor and find `var EMAILS = {`. Each email has a sender, subject, body, links, the best and acceptable choices, and a list of clues. In the body, `[[key|text]]` makes a link (add `|cta` for a button) and `{{key|text}}` marks a phrase that gets highlighted as a clue. Each clue's `k` matches one of those keys, `from` for the sender, or an attachment's key. Which emails belong to which level, and how many real ones each play includes, is set in `var LEVELS`.

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

Scores stay in each player's own browser. Nobody else can see them, and clearing browser data or switching browsers starts fresh. In Safari, embedded pages often can't keep cookies, so progress may not save there. If you want completion tracking, a simple option is to link a short Microsoft Form from the results screen.
