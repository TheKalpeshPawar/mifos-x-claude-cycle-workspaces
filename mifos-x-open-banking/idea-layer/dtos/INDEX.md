# DTO Registry — mifos-x-open-banking

> Auto-maintained by `/idea generate-dtos`. 66 DTOs registered.
> Last run: 2026-05-30 — manual registration — added 5 new DTOs to resolve D2 unregistered refs (LobbyHours, DriveUpHours, BranchRouting, FaceImage, CreditRating) + remapped Address→PostalAddress and LatLng→GeoLocation in atm-locator/api.yaml + fixed D5 stale used_by on Account, Counterparty, Transaction, StandingOrderDetail.

| Name | Version | Origin | Consumers | PII |
|------|---------|--------|-----------|-----|
| Account | 1.0.0 | project | 3 | - |
| AccountApplication | 1.0.0 | project | 2 | - |
| AccountRouting | 1.0.0 | project | 2 | - |
| Agent | 1.0.0 | project | 1 | phone_number |
| AtmLocation | 1.0.0 | project | 1 | - |
| Branch | 1.0.0 | project | 1 | - |
| BranchRouting | 1.0.0 | project | 1 | - |
| CancelMandateResponse | 1.0.0 | project | 1 | - |
| Card | 1.0.0 | project | 2 | bank_card_number, name_on_card |
| CreditRating | 1.0.0 | project | 1 | - |
| ChangePasswordRequest | 1.0.0 | project | 1 | current_password, new_password |
| ChangePasswordResponse | 1.0.0 | project | 1 | - |
| Consent | 1.0.0 | project | 1 | - |
| Counterparty | 1.0.0 | project | 2 | name, other_account_routing_address |
| Currency | 1.0.0 | project | 1 | - |
| Customer | 1.0.0 | project | 4 | legal_name, mobile_phone_number, email, date_of_birth |
| CustomerMessage | 1.0.0 | project | 1 | from_person |
| DirectDebit | 1.0.0 | project | 1 | - |
| DriveUpHours | 1.0.0 | project | 1 | - |
| FaceImage | 1.0.0 | project | 1 | url |
| FxRate | 1.0.0 | project | 2 | - |
| GeoLocation | 1.0.0 | project | 1 | - |
| IbanCheckResult | 1.0.0 | project | 1 | - |
| KycDocument | 1.0.0 | project | 2 | number, date_of_birth |
| LobbyHours | 1.0.0 | project | 1 | - |
| MandateDetail | 1.0.0 | project | 1 | counterparty_name |
| Meeting | 1.0.0 | project | 2 | - |
| MeetingInvitee | 1.0.0 | project | 1 | - |
| MoneyAmount | 1.0.0 | shared | 5 | - |
| OidcToken | 1.0.0 | project | 1 | access_token, id_token, refresh_token |
| PasswordResetConfirmRequest | 1.0.0 | project | 1 | token, new_password |
| PasswordResetRequest | 1.1.0 | project | 1 | email |
| PasswordResetResponse | 1.0.0 | project | 1 | - |
| PersonalDataField | 1.0.0 | project | 2 | - |
| PostalAddress | 1.0.0 | project | 2 | - |
| Product | 1.0.0 | project | 1 | - |
| SepaTransactionRequest | 1.0.0 | project | 2 | to_iban, to_name |
| SignalChannel | 1.0.0 | project | 1 | - |
| StandingOrder | 1.0.0 | project | 2 | to_iban, to_name |
| StandingOrderDetail | 1.0.0 | project | 1 | beneficiary_name, beneficiary_iban |
| StandingOrderExecution | 1.0.0 | project | 1 | - |
| StandingOrderStatusResponse | 1.0.0 | project | 3 | - |
| Transaction | 1.0.0 | project | 3 | - |
| TransactionAccount | 1.1.0 | project | 1 | - |
| TransactionComment | 1.0.0 | project | 2 | - |
| TransactionCounterparty | 1.0.0 | project | 1 | holder_name |
| TransactionDetails | 1.0.0 | project | 2 | - |
| TransactionMetadata | 1.0.0 | project | 2 | - |
| TransactionTag | 1.0.0 | project | 4 | - |
| UserProfile | 1.1.0 | project | 3 | email, display_name |
| AccountInfo | 1.0.0 | project | 1 | - |
| AmountOfMoney | 1.0.0 | project | 1 | - |
| CardReplacement | 1.0.0 | project | 1 | - |
| Challenge | 1.0.0 | project | 2 | - |
| Charge | 1.0.0 | project | 2 | - |
| Comment | 1.0.0 | project | 1 | - |
| ConsentRedirect | 1.0.0 | project | 1 | - |
| CustomerAccountLink | 1.0.0 | project | 1 | - |
| DirectDebitCounterparty | 1.0.0 | project | 2 | - |
| Payment | 1.0.0 | project | 1 | - |
| ProductDetails | 1.0.0 | project | 1 | - |
| ProductMeta | 1.0.0 | project | 1 | - |
| StandingOrderSchedule | 1.0.0 | project | 2 | - |
| StandingOrderUpdateRequest | 1.0.0 | project | 1 | - |
| Tag | 1.0.0 | project | 2 | - |
| TagAuthorUser | 1.0.0 | project | 2 | display_name |
