# Terms and Conditions — Mifos-X Open Banking

**App Name:** Mifos-X Open Banking  
**Package:** org.mifos  
**Developer:** Mifos Initiative / openMF contributors  
**Contact:** legal@mifos.org  
**Effective Date:** 2026-05-30  
**Version:** 1.0.0  

---

## 1. Introduction and Agreement

Mifos-X Open Banking ("the App", "Software") is a Kotlin Multiplatform (KMP) open-source banking application that delivers two personas — Consumer (retail banking self-service) and Field Officer (agent banking) — from a single codebase on Android, iOS, desktop (macOS, Windows, Linux), and web platforms.

By installing, accessing, or using the App, you ("User", "you") agree to be bound by these Terms and Conditions ("Terms"). If you do not agree, do not install or use the App.

These Terms govern your use of the App software. Separate terms of service from your banking institution govern the financial products and banking services you access through the App.

---

## 2. Description of the Application

### 2.1 Solution

Mifos-X Open Banking is a **dual-persona KMP banking super-app** powered by the Open Bank Project (OBP) API v7.0.0. The App provides:

**Consumer Persona ("Banking for Everyone"):**
- Account overview with real-time balances
- Transaction history and spending insights
- Send Money (payment initiation via OBP)
- Beneficiary management
- Debit/credit card management
- Standing order management
- ATM locator
- Foreign exchange rate viewer

**Field Officer Persona (Agent Banking):**
- Customer search and detail view
- New customer onboarding (KYC collection)
- Corporate account onboarding
- KYC document review and compliance workflows
- Account application management
- Customer messaging
- Meeting and schedule management

The App connects exclusively to the OBP REST API endpoint configured by the deploying banking institution. It is a **client application only** — it does not own or operate a database, backend, or financial infrastructure.

### 2.2 Open-Source License

The App's source code is available at https://github.com/openMF/mifos-x-open-banking under the Mozilla Public License 2.0 (MPL-2.0). Use, modification, and distribution of the source code are governed by that license.

---

## 3. User Eligibility and Accounts

### 3.1 Eligibility

You must be at least 18 years old and legally capable of entering binding agreements to use this App. Field Officers must also hold a valid authorization credential issued by their employing banking institution.

### 3.2 Account Credentials

Your username, password, and OBP authentication token are issued by the banking institution whose OBP API instance you are connecting to. You are responsible for:
- Keeping your credentials confidential
- Not sharing your credentials with any third party
- Notifying your banking institution immediately if you suspect unauthorized access
- Logging out of the App when using shared devices

We are not responsible for losses resulting from unauthorized use of your credentials.

### 3.3 Consumer Key

The OBP Consumer Key embedded in your deployment of the App is a credential issued to the deploying organization by the OBP API operator. Do not attempt to extract, share, or misuse this credential.

---

## 4. Permitted and Prohibited Uses

### 4.1 Permitted Uses

You may use the App to:
- Access your own banking accounts and financial data via the connected OBP API
- Initiate payments and transactions for which you are authorized
- Perform Field Officer duties (if licensed) including customer onboarding and KYC as authorized by your employing institution
- Export or download your own financial data for personal record-keeping

### 4.2 Prohibited Uses

You must not use the App to:
- Access accounts or data belonging to other individuals without explicit authorization
- Attempt to reverse-engineer, decompile, or extract authentication credentials embedded in the App
- Perform automated scraping, bulk data extraction, or API abuse beyond normal single-user operation
- Circumvent security controls, authentication, or rate limits
- Use the Field Officer persona without valid institutional authorization
- Conduct any activity that violates applicable financial regulations (AML, KYC, sanctions screening)
- Upload malicious content or attempt to inject code through the App's interfaces
- Use the App for fraudulent, deceptive, or money-laundering activities

Violation of prohibited uses may result in termination of your access and may be referred to law enforcement.

---

## 5. Financial Services Disclaimer

### 5.1 App is a Client Interface Only

The App is a **front-end interface** to the OBP banking API. It does not:
- Hold, store, or process funds
- Execute financial transactions independently — all transactions are processed by the OBP API backend operated by your banking institution
- Provide investment advice, financial planning, or regulated financial advisory services
- Guarantee the accuracy, completeness, or timeliness of account and transaction data displayed

### 5.2 Banking Institution Responsibility

All financial services (account management, payment processing, card services) are provided by the banking institution operating the OBP API instance you are connected to. Their separate terms of service, product terms, and regulatory disclosures govern those services.

### 5.3 Transaction Finality

Payment transactions initiated through the App are submitted to the OBP API for processing. Once submitted, transactions may be irreversible. Review all payment details carefully before confirming. We are not liable for erroneous payments initiated by you.

---

## 6. Data and Privacy

Your use of the App is governed by our Privacy Policy (see `PRIVACY_POLICY.md` and https://mifos.org/privacy-policy). Key data practices:

- Authentication tokens are stored encrypted on-device and cleared on logout
- Financial data is cached locally for offline display and is not transmitted to any server other than the connected OBP API
- Crash and performance telemetry is collected on Android via Firebase Crashlytics and Firebase Performance Monitoring — no financial data is included in these reports
- We do not sell your personal data

---

## 7. Intellectual Property

### 7.1 App Source Code

The App source code is licensed under the Mozilla Public License 2.0 (MPL-2.0). See the full license at https://github.com/openMF/mifos-x-open-banking/blob/dev/LICENSE.

### 7.2 Third-Party Components

The App incorporates third-party open-source libraries including:
- Kotlin Multiplatform / Compose Multiplatform (Apache 2.0 — JetBrains)
- Ktor / Ktorfit (Apache 2.0)
- Koin (Apache 2.0)
- Store5 (Apache 2.0)
- Room KMP (Apache 2.0 — Google)
- Firebase Android SDKs (Apache 2.0 — Google)

A complete license inventory is available in the App's open-source acknowledgements screen.

### 7.3 Mifos Trademarks

"Mifos" and associated logos are trademarks of the Mifos Initiative. Use of these trademarks in derivative works requires prior written permission.

---

## 8. Disclaimers and Limitation of Liability

### 8.1 "As Is" Software

THE APP IS PROVIDED "AS IS" AND "AS AVAILABLE" WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND NON-INFRINGEMENT.

### 8.2 No Warranty on Financial Data Accuracy

WE DO NOT WARRANT THAT ACCOUNT BALANCES, TRANSACTION HISTORIES, OR OTHER FINANCIAL DATA DISPLAYED IN THE APP ARE ACCURATE, COMPLETE, OR CURRENT AT ALL TIMES. SUCH DATA IS RETRIEVED FROM THE CONNECTED OBP API AND IS SUBJECT TO TRANSMISSION DELAYS, API ERRORS, AND BANKING INSTITUTION PROCESSING TIMES.

### 8.3 Limitation of Liability

TO THE MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW, IN NO EVENT SHALL THE MIFOS INITIATIVE, OPENMF CONTRIBUTORS, OR AFFILIATED PARTIES BE LIABLE FOR:
- LOSS OF FUNDS ARISING FROM UNAUTHORIZED ACCESS TO YOUR ACCOUNT CREDENTIALS
- ERRONEOUS PAYMENT TRANSACTIONS INITIATED BY YOU
- BUSINESS INTERRUPTION, DATA LOSS, OR LOST PROFITS ARISING FROM USE OF OR INABILITY TO USE THE APP
- INDIRECT, INCIDENTAL, SPECIAL, OR CONSEQUENTIAL DAMAGES

Where consumer protection law prohibits limitation of liability for certain losses, such limitations shall not apply to the extent prohibited.

---

## 9. Indemnification

You agree to indemnify and hold harmless the Mifos Initiative, openMF contributors, and their directors, employees, and agents from any claims, damages, or expenses arising from:
- Your violation of these Terms
- Your use of the App in a manner not authorized by these Terms
- Your violation of applicable law, including financial regulations
- Infringement of any third-party right by your use of the App

---

## 10. Termination

### 10.1 By You

You may stop using the App at any time by uninstalling it from your device. Uninstalling the App clears the local encrypted database (cached financial data and session tokens).

### 10.2 By Us

We reserve the right to discontinue, suspend, or modify the App at any time, with or without notice. We may release updated versions that supersede prior versions.

---

## 11. Updates and Changes

We may update these Terms from time to time. Material changes will be communicated via an in-app notification and by updating the "Effective Date" above. Continued use of the App after the effective date of revised Terms constitutes acceptance.

---

## 12. Governing Law and Dispute Resolution

These Terms are governed by the laws of the State of Virginia, United States, without regard to conflict of law provisions. Disputes arising from these Terms shall be resolved by binding arbitration administered by the American Arbitration Association under its Commercial Arbitration Rules, except that either party may seek injunctive relief in a court of competent jurisdiction.

If you are located in the European Economic Area, mandatory consumer protection laws of your country of residence may apply in addition to or instead of the above.

---

## 13. Regulatory Compliance (Field Officers)

Field Officers using this App for customer onboarding, KYC, and account applications must comply with:
- Their employing institution's internal compliance policies
- Anti-Money Laundering (AML) and Know Your Customer (KYC) regulations applicable in their jurisdiction
- Any applicable data protection regulations when processing customer personal data

The App provides tooling; regulatory compliance responsibility rests with the deploying banking institution and its authorized staff.

---

## 14. Contact

For questions about these Terms:

**Email:** legal@mifos.org  
**Postal:** Mifos Initiative, c/o Conflux Foundation, 3040 Williams Drive Suite 610, Fairfax VA 22031, USA  

For banking service inquiries, contact your banking institution directly.
