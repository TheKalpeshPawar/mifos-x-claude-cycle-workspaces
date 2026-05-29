# Privacy Policy — Mifos-X Open Banking

**App Name:** Mifos-X Open Banking  
**Package:** org.mifos  
**Developer:** Mifos Initiative / openMF contributors  
**Contact:** privacy@mifos.org  
**Effective Date:** 2026-05-30  
**Version:** 1.0.0  

---

## 1. Introduction

Mifos-X Open Banking ("the App", "we", "us", "our") is a Kotlin Multiplatform banking application available on Android, iOS, desktop, and web. It connects retail banking customers ("Consumers") and banking field officers ("Field Officers") to financial services powered by the Open Bank Project (OBP) REST API v7.0.0.

We are committed to protecting your personal data and financial privacy. This Privacy Policy explains what data we collect, how we use it, who we share it with, and what rights you have.

This policy applies to all platforms on which the App is available: Android, iOS (iPhone and iPad), desktop (macOS, Windows, Linux), and web browser.

---

## 2. Controller Identity

The data controller responsible for your personal data is the deploying financial institution or banking organization that hosts the Open Bank Project instance to which this App connects. The App itself is open-source software; data is processed by and on behalf of the connected banking institution.

For the reference deployment at `api.openbankproject.com`:
- **Controller:** Open Bank Project Community Interest Company
- **Contact:** contact@openbankproject.com

If you are using a white-label deployment operated by another financial institution, that institution is the data controller. Consult their privacy notice.

---

## 3. Data We Collect and Why

### 3.1 Financial and Account Information

When you authenticate and use the App, we access the following financial data via the OBP API on your behalf:

| Data Type | Source | Purpose |
|---|---|---|
| Bank account numbers (masked) | OBP API — `/obp/v7.0.0/my/accounts` | Display account list and balances |
| Account balances | OBP API — `/obp/v7.0.0/accounts/{id}/balances` | Home dashboard, account detail screens |
| Transaction history | OBP API — `/obp/v7.0.0/accounts/{id}/transactions` | Transaction list, spending analysis |
| Beneficiary details (name, IBAN/account) | OBP API — `/obp/v7.0.0/my/transaction-request-types/{type}/beneficiaries` | Send money flows |
| Payment card information (masked PAN, expiry, status) | OBP API — `/obp/v7.0.0/my/cards` | Card management screens |
| Standing order details | OBP API — `/obp/v7.0.0/accounts/{id}/standing-orders` | Standing order management |
| Foreign exchange rates | OBP API — `/obp/v7.0.0/fx/available-currency-iso-codes` | FX rates screen |

**Retention:** Financial data accessed via the API is displayed in-session and may be cached locally in an encrypted Room KMP database on your device for offline viewing. The App does not transmit your financial data to any server other than the OBP API endpoint your deployment is configured to use.

### 3.2 Authentication Credentials

| Data Type | How Stored | Purpose |
|---|---|---|
| OBP Consumer Key | Encrypted environment variable (`OBP_CONSUMER_KEY`) — never in source code | API authentication |
| OBP Direct Login token | Stored in encrypted Room KMP datastore on-device; cleared on logout | Session authentication for API requests |
| Username (for login) | Transmitted to OBP API login endpoint; not stored persistently | Authentication |
| Password | Transmitted to OBP API login endpoint over HTTPS; never logged or stored | Authentication |

**Note:** We do not store your password. Authentication credentials are transmitted exclusively to the configured OBP API endpoint over TLS 1.2+.

### 3.3 Personal Identifiers

| Data Type | Source | Purpose |
|---|---|---|
| Display name / full name | OBP API — user profile | Profile screen display |
| Email address | OBP API — user profile | Profile display; account correspondence |
| Profile photo (if available) | OBP API | Profile screen |

For **Field Officers**, customer personal data accessed during onboarding and KYC workflows includes:

| Data Type | Purpose |
|---|---|
| Customer full name, date of birth, national ID | Customer onboarding and KYC verification |
| Customer address | Account application processing |
| Customer contact details (phone, email) | Customer record creation |
| KYC documents (images / references) | Regulatory compliance — AML/KYC |

All customer personal data accessed by Field Officers is transmitted to and processed by the OBP API backend. The App acts as a front-end interface; the banking institution is responsible for the lawful basis and retention of customer records.

### 3.4 Device Identifiers and Technical Data

| Data Type | Source | Purpose |
|---|---|---|
| Device crash data (stack traces, device model, OS version, App version) | Firebase Crashlytics SDK (Android only) | Crash reporting and bug fixing |
| App performance metrics (cold-start time, frame rates, network latency) | Firebase Performance Monitoring SDK (Android only) | Performance monitoring |
| Installation UUID (Firebase installation ID) | Firebase SDK (Android only) | Aggregating crash + performance telemetry |

Firebase Crashlytics and Firebase Performance Monitoring are **Android-only** features. These SDKs do not operate on iOS, desktop, or web builds of this App.

### 3.5 Local Storage

The App uses Room KMP (SQLite) encrypted local database for:
- Caching account and transaction data for offline display
- Storing user preferences (theme, language)
- Storing encrypted session token

Local database data does not leave your device except as part of normal OBP API interactions.

---

## 4. Third-Party Services

The App integrates with the following third-party services:

### 4.1 Open Bank Project (OBP) API

- **Provider:** Open Bank Project Community Interest Company / deploying financial institution
- **Purpose:** All banking data access — accounts, transactions, payments, cards, FX, customer onboarding
- **Data shared:** Authentication credentials (token), all financial queries
- **Privacy policy:** https://www.openbankproject.com/privacy-policy/
- **Data transfer:** All API calls are made over HTTPS (TLS 1.2+) to the configured OBP endpoint

### 4.2 Firebase Crashlytics (Android only)

- **Provider:** Google LLC
- **Purpose:** Crash reporting — automatic capture of unhandled exceptions and fatal errors
- **Data shared:** Crash stack traces, device model, Android OS version, App version, Firebase installation UUID
- **No PII in crash reports:** We do not log usernames, account numbers, or financial data to Crashlytics. Crash reports contain only technical diagnostics.
- **Privacy policy:** https://policies.google.com/privacy
- **Google Data Processing Terms:** https://business.safety.google/adsprocessorterms/

### 4.3 Firebase Performance Monitoring (Android only)

- **Provider:** Google LLC
- **Purpose:** App performance metrics — cold start time, screen rendering, network request latency
- **Data shared:** Anonymous performance traces, network request URLs (no request bodies or auth tokens), device class
- **No PII in performance traces:** Network URLs logged by Performance Monitoring are stripped of auth tokens and query parameters containing user data.
- **Privacy policy:** https://policies.google.com/privacy

---

## 5. Legal Basis for Processing (GDPR)

If you are located in the European Economic Area (EEA), United Kingdom, or Switzerland, we process your personal data under the following legal bases:

| Processing Activity | Legal Basis |
|---|---|
| Accessing account and transaction data | **Contract performance** (Art. 6(1)(b) GDPR) — necessary to provide banking services |
| Authentication credential handling | **Contract performance** (Art. 6(1)(b) GDPR) |
| KYC / customer onboarding data (Field Officer) | **Legal obligation** (Art. 6(1)(c) GDPR) — AML/KYC regulatory requirements |
| Firebase Crashlytics crash telemetry | **Legitimate interests** (Art. 6(1)(f) GDPR) — maintaining app stability and security |
| Firebase Performance telemetry | **Legitimate interests** (Art. 6(1)(f) GDPR) — app quality improvement |
| Local preference data | **Contract performance** / **Legitimate interests** |

---

## 6. Data Retention

| Data Category | Retention |
|---|---|
| OBP session token | Deleted on logout; maximum 24-hour session |
| Cached financial data (Room KMP) | Cleared on logout; maximum 30 days inactive |
| Firebase crash reports | 90 days in Firebase Console (Google's retention policy) |
| Firebase performance traces | 90 days in Firebase Console |
| Customer KYC records (Field Officer) | Retained by the banking institution per applicable AML/KYC regulation (typically 5–10 years) |

---

## 7. Data Transfers

Financial data is transmitted to and from the OBP API server operated by the banking institution deploying this App. If that server is located outside your country, data may be transferred internationally.

Firebase services (Crashlytics and Performance Monitoring) are provided by Google LLC, a US-based company. Google participates in the EU-US Data Privacy Framework. Data processing agreements are in place per GDPR Article 28.

---

## 8. Security

We implement the following technical safeguards:

- All network communications use HTTPS / TLS 1.2 or higher
- OBP session tokens are stored in an encrypted Room KMP datastore (Android Keystore / iOS Secure Enclave / platform-equivalent)
- Authentication credentials are transmitted only to the configured OBP API endpoint — never to any other server
- Passwords are never logged, stored on-device, or transmitted to any party other than the OBP login endpoint
- Firebase SDKs are configured to exclude sensitive fields from crash reports

---

## 9. Your Rights

### GDPR Rights (EEA / UK / Switzerland)

You have the following rights regarding your personal data:

- **Right of Access (Art. 15):** You may request a copy of the personal data we hold about you.
- **Right to Rectification (Art. 16):** You may request correction of inaccurate personal data.
- **Right to Erasure / "Right to be Forgotten" (Art. 17):** You may request deletion of your personal data where we no longer have a lawful basis to retain it.
- **Right to Restriction of Processing (Art. 18):** You may request that we restrict how we process your data in certain circumstances.
- **Right to Data Portability (Art. 20):** You may request your data in a machine-readable format.
- **Right to Object (Art. 21):** You may object to processing based on legitimate interests.
- **Right to Withdraw Consent:** Where processing is based on consent, you may withdraw it at any time.
- **Right to Lodge a Complaint:** You have the right to lodge a complaint with your national data protection authority (e.g., ICO in the UK, BfDI in Germany).

### CCPA Rights (California Residents)

If you are a California resident, you have the following rights under the California Consumer Privacy Act:

- **Right to Know:** You may request disclosure of the categories and specific pieces of personal information we have collected about you.
- **Right to Delete:** You may request deletion of personal information we have collected, subject to exceptions.
- **Right to Opt-Out of Sale:** We do **not** sell your personal information to third parties.
- **Right to Non-Discrimination:** You will not receive discriminatory treatment for exercising your CCPA rights.

To exercise any of these rights, contact: **privacy@mifos.org**

Response time: 30 days for GDPR requests; 45 days for CCPA requests.

---

## 10. Children's Privacy

This App is a banking application intended for adults (18+) and authorized banking professionals. We do not knowingly collect personal data from individuals under 18. If you believe a minor's data has been collected, contact privacy@mifos.org immediately.

---

## 11. Changes to This Policy

We will notify you of material changes to this policy via an in-app notification and by updating the "Effective Date" above. Continued use of the App after the effective date constitutes acceptance of the revised policy.

---

## 12. Contact

For privacy inquiries, data subject rights requests, or to report a data protection concern:

**Email:** privacy@mifos.org  
**Postal:** Mifos Initiative, c/o Conflux Foundation, 3040 Williams Drive Suite 610, Fairfax VA 22031, USA  
**Response time:** 30 days  

For EU/UK data protection inquiries, you may also contact the deploying financial institution's Data Protection Officer if applicable.
