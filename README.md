# Pocket Cards

An offline wallet for loyalty cards, IDs, bank cards and anything else with a number.
Developed by Henry Poudel · hennrywebworm@gmail.com

## Features

- **Eight languages.** English, Burmese, Thai, Hindi, Nepali, Chinese, Japanese and Vietnamese (*Settings → Language*). The whole interface is translated; store and bank names stay as they are.
- **Your look.** Light, dark or automatic, plus 8 colour skins, or match your wallpaper on Android 12+.
- **Everything in one grid, sorted into groups.** Loyalty cards, Personal documents, Bank & payment cards, Transport, Coupons, Payment QR codes, Receipts, Investment accounts, Health and Others. You can rename, add, reorder and delete groups, and **one card can be in several groups**.
- **Rearrange by hand.** Press and hold a card, then drag it. Dropping it among another group's cards moves it there.
- **A type for every need**
  - *Cards* (loyalty, membership, transport such as Rabbit, Mangmoom and MRT, bank and payment cards)
  - *Documents* (passport, visa, Thai ID, pink card, work permit, driving licence, tax ID, social security, NRC, CI, **birth certificate**, marriage certificate, house registration, household list, degree, military document, police clearance, land title, vaccination record…)
  - *Coupons* (Lazada, Shopee, Robinson, Lotus's, Grab and more), with discount, valid-until date and "mark as used"
  - *Payment QR codes* (PromptPay, K PLUS, SCB, TrueMoney, KBZPay, AYA Pay, WavePay, CB Pay…). Scan your own receiving QR, or read it from a screenshot. It is copied exactly.
  - *Receipts*, invoices and warranties, with date, amount and warranty end date
  - *Securities accounts* (InnovestX, Bualuang, KS, KGI, Yuanta, IBKR, CB Securities…), with Cash, Cash Balance, Derivatives and Offshore sections (or your own), each holding up to 20 account numbers
- **Up to 50 photos per card**, stored as the original full-quality files. Swipe through them and double-tap to zoom.
- **Export any card as a PDF**: the code and details on page 1, then one photo per page. Share it or save it.
- **Show as barcode, QR code or number only** for anything you type in.
- **Private numbers.** "Hide number until tapped". Never store a card's CVV or PIN.
- **Sharing**, scan from photo, Google Drive and file backup, boarding passes (`.pkpass`), widget and app lock, as before.
- **About**: version, developer, email and WhatsApp (opens a chat, or the Play Store if WhatsApp isn't installed).

### NFC and transit cards
Pocket Cards can't act as your Rabbit or MRT card through the phone's NFC. Those cards hold their fare balance in a secured chip, and Android phones can't imitate that chip. Copying one would also break the transit operator's rules. What does work:
- **MRT Blue & Purple lines:** since 1 June 2026 the gates accept contactless Visa, Mastercard and UnionPay cards, and the old MRT / MRT Plus cards no longer work. Add your bank card to Google Wallet and tap your phone at the gate.
- **BTS:** keep using your Rabbit card. Store its number in Pocket Cards so you have it if it is lost.

## Updating your phone

Version 1.1 and later are signed with a permanent key (`app/pocketcards.keystore`), so 1.2 installs over 1.1 and keeps all your cards. Cards from earlier versions are upgraded automatically: front and back photos become the first two photos.

If you are coming from 1.0, uninstall it once first, after exporting a backup file.

**Keep the GitHub repository private.** The signing key's password is in `app/build.gradle.kts`.

## Google Drive setup (one time, about 5 minutes)

"Back up to Google Drive" needs Google to recognise the app. Until this is done, the button shows "Google Drive isn't set up for this app yet". "Save backup file" works without any setup.

1. Open <https://console.cloud.google.com/> and sign in with your Google account. Create a project, for example **Pocket Cards**.
2. Go to **APIs & Services → Library**, search for **Google Drive API** and click **Enable**.
3. Go to **Google Auth Platform** (or **OAuth consent screen**) and set it up:
   - App name **Pocket Cards**, user support email `hennrywebworm@gmail.com`, audience **External**.
   - Under **Audience → Test users**, add every Google account that will use Drive backup, including your own. Or click **Publish app**: the Drive permission the app uses (`drive.file`) needs no review from Google.
4. Go to **Clients** (or **Credentials → Create credentials → OAuth client ID**), choose **Android** and enter:
   - Package name: `com.pocketcards.app`
   - SHA-1 certificate fingerprint: `8A:8C:2A:D2:0A:19:20:5A:54:32:59:81:39:15:85:06:D2:EE:48:3F`
5. Save. Wait a few minutes, then try **Settings → Back up to Google Drive** in the app.

The app can only see the single file it creates (`PocketCards-backup.zip`), never anything else in your Drive.

## Build it

### GitHub (no computer setup)
The workflow in `.github/workflows/build.yml` builds the APK on every push. Open **Actions**, click the latest green run, and download **pocket-cards-apk** under **Artifacts**.

### Android Studio
Use *File → Open* on this folder, then press **Run ▶**.

## Where things are

| Path | What |
|---|---|
| `data/Models.kt` | Cards, groups, passes, settings |
| `data/Stores.kt` | Starter list of stores, documents, banks, transport, coupons, payment QRs, brokers and hospitals; edit freely |
| `data/PdfExporter.kt` | PDF export |
| `res/values-*/strings.xml` | Translations (my, th, hi, ne, zh, ja, vi) |
| `ui/theme/Theme.kt` | Light/dark mode and colour skins |
| `data/WalletRepository.kt` | Saving, groups, ordering |
| `data/DriveBackup.kt` | Google Drive backup and restore |
| `data/Backup.kt` | Backup .zip files |
| `data/CardShare.kt` | Sharing pictures, text and transfer codes |
| `scan/` | Camera scanner and reading codes from photos |
| `ui/` | All screens |
| `widget/CardsWidget.kt` | Home-screen widget |
| `res/mipmap-*/ic_launcher_foreground.png` | App icon |
| `res/drawable-nodpi/logo_art.png` | Logo used on the splash and About screens |
