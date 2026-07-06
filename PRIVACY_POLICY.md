# Privacy Policy for WakeWise Alarm

**Effective date:** 07-05-2026
**Last updated:** 07-05-2026

This Privacy Policy explains what information the **WakeWise Alarm** mobile
application ("WakeWise", "the app", "we", "us") collects, how it is used, and
who it is shared with. WakeWise is provided by **the WakeWise team**.

We designed WakeWise to work with as little personal data as possible. The app
has **no user accounts, no advertising, no analytics or crash-reporting SDKs,
and does not sell your data.**

---

## 1. Summary

| What | Why | Where it goes |
|------|-----|---------------|
| A **hashed device identifier** (SHA-256 of your Android ID) | To anchor your 7-day free trial and prevent trial abuse via reinstall | Our backend proxy (Cloudflare), stored up to 90 days |
| The **addresses / locations** you enter for a commute (home, work, stops) | To calculate real-time, traffic-aware travel time so your alarm wakes you at the right moment | Sent to Google Maps Platform (via our proxy) to compute the route |
| **Address search text** you type when picking a place | To show address autocomplete suggestions | Sent to Google Places directly from the app |
| **Your IP address** | Rate limiting / abuse protection; standard networking | Seen by our proxy (Cloudflare) and by Google when the app contacts it |
| **Purchase / subscription status** | To unlock the paid subscription and verify it is active | Handled by Google Play Billing; a purchase token is verified with Google |

Everything else — your alarms, schedules, saved addresses, imported ringtones,
chosen background image, and usage statistics — **stays on your device.**

---

## 2. Information we collect and process

### 2.1 Hashed device identifier (free-trial anti-abuse)

WakeWise offers a 7-day free trial. To stop the trial from being reset by
uninstalling and reinstalling the app, we anchor the trial start date on our
server.

To do this, the app reads the Android system value `Settings.Secure.ANDROID_ID`,
computes a one-way **SHA-256 hash** of it, and sends only that hash to our
backend proxy. **The raw Android ID never leaves your device.** Our proxy
records the first time it sees a given hash and returns that timestamp so the
trial length is consistent.

- Android ID is already scoped per app-signer and device user; it does not
  identify you across other apps or reveal your identity.
- The hash is stored in our key-value store for up to **90 days**, after which
  it is automatically deleted.

### 2.2 Commute locations and routes

To compute a traffic-aware wake time, WakeWise needs the **origin, destination,
and any intermediate stops** of your commute. You enter these yourself (by
typing an address or picking one from autocomplete). WakeWise does **not** access
your device's GPS/precise location — the app requests no location permission.

When it is time to estimate your commute, the app sends these addresses (or their
coordinates) to our backend proxy, which forwards them to the **Google Maps
Directions API** to calculate driving time in current traffic. Our proxy does not
retain your addresses beyond what is needed to complete the request; Google
processes them under its own privacy policy (see Section 4).

Your alarms and saved addresses are also stored **locally on your device** in the
app's database.

### 2.3 Address autocomplete

When you search for an address, the text you type is sent to the **Google Places
SDK** to return matching suggestions and place details. This request goes from
your device to Google directly and is subject to Google's privacy policy.

### 2.4 Network information (IP address)

Like any app that makes network requests, WakeWise transmits your device's IP
address to the servers it contacts. Our backend proxy uses the IP address for
**per-IP rate limiting** to protect the service from abuse. We do not use it to
build a profile of you, and we do not store it for analytics.

### 2.5 Subscriptions and payments

The paid subscription is sold and processed entirely through **Google Play
Billing**. We never see or store your payment card or billing details — Google
handles all of that.

When you subscribe, Google Play provides the app a **purchase token**. The app
stores this token on your device and forwards it to our backend proxy, which
verifies with the **Google Play Developer API** that your subscription is active.
The proxy may cache the result (keyed by a hash of the token) for a short time to
avoid repeated verification calls.

### 2.6 Information stored only on your device

The following never leaves your device (except through Android's own optional
backup — see Section 6) and is not sent to us:

- Your alarms, schedules, arrival times, and settings
- Your saved address book ("Home", "Work", etc.)
- Alarm history and statistics (e.g. minutes of sleep saved)
- Ringtones you import and any background image you choose
- App preferences (dark mode, onboarding state, trial/subscription flags)

If you uninstall the app, this on-device data is removed by Android.

---

## 3. What we do **not** collect

- No name, email address, phone number, or user account.
- No precise or background GPS location (the app requests no location permission).
- No contacts, calendar, photos library, or microphone access.
- No advertising identifier, and **no advertising**.
- No third-party analytics or crash-reporting SDKs.

---

## 4. Third-party services

WakeWise relies on the following third parties to function. Each processes data
under its own privacy policy:

- **Google Maps Platform** (Directions API and Places SDK) — computes commute
  time and provides address autocomplete.
  https://policies.google.com/privacy
- **Google Play Billing / Google Play Developer API** — processes subscription
  payments and verifies entitlement.
  https://policies.google.com/privacy
- **Cloudflare** — hosts our backend proxy that fronts the Google Directions API
  and anchors the free trial. https://www.cloudflare.com/privacypolicy/

We do **not** sell your personal information, and we do not share it with third
parties except as needed to provide the features described above.

---

## 5. How long we keep data

- **Hashed device identifier:** up to 90 days on our proxy, then automatically
  deleted.
- **Commute addresses:** processed transiently to fulfil a routing request; our
  proxy does not store them after the request completes. Google retains request
  data under its own policy.
- **Cached subscription verification:** a hashed purchase token may be cached
  briefly (about one hour).
- **On-device data:** kept until you delete it in the app or uninstall the app.

---

## 6. Android backup

If you have Android's system backup or device-transfer feature enabled (a
Google account setting you control), Android may back up the app's on-device
data — including your alarms, saved addresses, and settings — to your Google
account so it can be restored on a new device. This backup is managed by Google
under your Google account settings, not by us. You can disable it in your
device's backup settings.

---

## 7. Security

Requests between the app and our backend proxy are sent over HTTPS and require a
bearer token. We send only a one-way hash of your device identifier, never the
raw value. No method of transmission or storage is 100% secure, but we limit
what we collect specifically to reduce risk.

---

## 8. Children's privacy

WakeWise is not directed to children under 13 (or the equivalent minimum age in
your jurisdiction), and we do not knowingly collect personal information from
children. If you believe a child has provided us information, contact us and we
will delete it.

---

## 9. Your rights and choices

Depending on where you live (for example, under the EU/UK GDPR or the California
CCPA/CPRA), you may have the right to access, correct, or delete your personal
information, or to object to certain processing.

Because WakeWise stores most data on your device and holds only a hashed,
non-identifying device value on the server, you can exercise most of these rights
directly:

- **Delete on-device data:** clear the app's storage or uninstall the app.
- **Delete the server trial anchor:** it expires automatically within 90 days;
  contact us if you want it removed sooner.
- **Manage your subscription:** through the Google Play Store subscriptions
  screen.

To make any other request, contact us at the address below.

---

## 10. Changes to this policy

We may update this Privacy Policy from time to time. When we do, we will revise
the "Last updated" date above and, where appropriate, provide a more prominent
notice. Continued use of the app after changes take effect constitutes acceptance
of the updated policy.

---

## 11. Contact

If you have questions about this Privacy Policy or your data, contact:

**The WakeWise team**
Email: **smartcommutealarm@gmail.com**

This policy is governed by the laws of the **State of Florida, United States**.
