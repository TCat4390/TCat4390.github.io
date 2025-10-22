Bridge (Beta) — Privacy Policy

Effective Date: 2025-10-22
Last Updated: 2025-10-22

This Privacy Policy applies to the Bridge mobile application distributed via Apple TestFlight (the “App”) for testing/evaluation purposes only. By using the App, you agree to this Policy.

We do not sell personal data and we do not run advertising or third-party trackers in this beta.

⸻

1) What We Process (Data Categories)

A. Voice (Speech-to-Text for translation)
	•	Source. Recorded via iOS microphone when you tap record (44.1 kHz, mono AAC). Ambient sounds may be captured.
	•	Path. App → Cloudflare Worker /stt (relay only; no storage) → OpenAI STT API → Worker returns text → App. No alternate routes.
	•	On-device processing. No VAD/peak limiting/redaction performed locally.
	•	Worker behavior. For STT, the Worker forwards the multipart body without unpacking; no persistence.
	•	Retention. The temporary .m4a file is deleted immediately after transcription (SpeechManager.cleanupRecording). Worker 0 seconds. OpenAI may retain limited data per its own policy (commonly up to 30 days) and is not used for model training where such API settings are available. We cannot force third-party deletion.

B. Photos / Images (Photo explanation)
	•	Source. In-app camera capture only (no photo-library import at this time).
	•	EXIF/GPS. After capture we re-encode via jpegData(compressionQuality: 0.8) and normalize/crop; original EXIF/GPS/device metadata are removed.
	•	Optimization. App performs CapturedPhoto.optimizedData() (long edge 1600 px, ~0.8 quality), base64-encodes.
	•	Path. App → Cloudflare Worker (pass-through) → OpenRouter (model provider) → Worker → App. Worker does no compression, no caching; it simply wraps the base64 (e.g., data:image/...;base64,) and forwards.
	•	Payload size. Typical 300–600 KB after optimization.
	•	Protection. No automated redaction or screenshot detection yet; we present UI prompts reminding you not to upload sensitive IDs (passports, credit cards, etc.).
	•	Retention. Worker 0 seconds (memory only). Locally, the App may store the imageData alongside your inquiry and results until you delete them.

C. Text (User inputs, LLM replies, translation history)
	•	Local storage. Stored with SwiftData (StoredChat, StoredPhotoInquiry), including user inputs, results, summaries/follow-ups, and any associated imageData. Stored in the App container with iOS Data Protection (encrypted when device is locked).
	•	Tokens / IDs. JWT, refresh tokens, and an App-generated device UUID are stored in Keychain (kSecAttrAccessibleAfterFirstUnlock).
	•	Backups. We do not sync ourselves; your data may be included in iOS/iCloud backups based on your own device settings.
	•	Uploads. Besides the minimal context needed to complete a specific request, we do not upload conversation history to our servers; no model-training or analytics uploads.

D. Device & Network Data
	•	App creates a non-reversible bridge.device.uuid stored in Keychain (we do not read hardware serials).
	•	At the Worker, we HMAC the sub from Sign in with Apple before writing to D1; refresh-token table stores token SHA-256 and device UUID only.
	•	IP addresses are visible to Cloudflare POPs for routing; we do not enable Logpush. The Worker does not store IP/User-Agent; any UA presented upstream is not persisted by us.

E. Logs & Telemetry
	•	Worker. Optional DEBUG_TRANSLATE console logs (off by default). When off, no payload/response content is logged. We do not persist logs to R2/Logpush.
	•	App. OSLog/Logger for errors and byte sizes (flagged .private). No Firebase Crashlytics/Analytics or other trackers.
	•	Database. D1 holds only business data (credits/ledger/refresh tokens), not request bodies.

F. Payments / Credits
	•	IAP. Apple In-App Purchases in TestFlight and production.
	•	Records. We maintain: ledger(id, hashed_user_id, delta, reason, meta JSON, timestamp), credits(balance), refresh_tokens(token_hash, expires_at, device_id), users(hashed_user_id, device_id, email, created_at).
	•	Receipts. /iap/redeem verifies against Apple immediately; we do not store the original base64 receipt.
	•	Retention. Planned 5 years for accounting/fraud-prevention. (Purge jobs to be added before GA.)

⸻

2) Why We Process (Purposes & Legal Bases)
	•	Provide core features (speech transcription, translation, photo explanation) — performance of a contract/your request; consent.
	•	Account & credits (top-ups, usage, fraud prevention) — performance of a contract; legal obligation; legitimate interests.
	•	Security/abuse control (rate-limit, request validation) — legitimate interests.
	•	Beta quality (basic reliability metrics) — legitimate interests.

We do not use your content for marketing or our own model training.

⸻

3) Where Your Data Goes (Vendors & Transfers)

We rely on carefully selected third-party processors solely to deliver the functions described above:
	•	Cloudflare Workers (and D1/Durable Objects as applicable) — request relay & minimal account/credits records. We configure Workers not to persist request/response bodies. Cloudflare may keep limited network-level logs for operations.
	•	OpenAI — speech-to-text (STT) processing.
	•	OpenRouter — routing translation/LLM inference to model providers.

These providers process data under their own terms/policies. We configure available API settings to disable data retention and training where possible, but we cannot guarantee their internal handling or deletion timelines. By using voice/photo features, you consent to these transfers.

International transfers. Traffic may traverse Cloudflare POPs globally; OpenAI/OpenRouter endpoints may reside outside your country (e.g., US/EU). For users in regions with cross-border rules, we rely on standard contractual safeguards where available.

⸻

4) Retention
	•	Voice temp file (App): deleted immediately after transcription (0 s).
	•	Worker content: 0 s (in-memory only).
	•	OpenAI (STT): may retain limited data per its policy (often up to 30 days); not used for training where disabled.
	•	Photos & conversation records (App): retained locally until you delete them (no auto-expiry).
	•	Refresh tokens: each token valid 30 days; revoked tokens kept to prevent replay.
	•	Credits & ledger: intended 5 years (accounting/fraud).
	•	System logs: no persistent app/worker content logs; Cloudflare may keep short operational metrics.

⸻

5) Your Choices & Controls
	•	Delete in App. You can delete individual items or “Delete All” for conversations/photo insights.
	•	Delete account. In Settings, “Delete Account” calls /me/delete to remove your hashed user records from D1 (users/credits/ledger/refresh_tokens).
	•	Email requests. Contact privacy@bridge.app; we target 5 business days to respond during beta.
	•	Third-party deletion. OpenAI/OpenRouter do not currently offer per-request deletion we can enforce; we state their independent retention and will pass along your requests, without guarantee of outcome.
	•	Backups. Your local/iCloud backups are under your device settings.

⸻

6) Security
	•	In transit. HTTPS/TLS end-to-end (App ↔ Worker ↔ third-party APIs).
	•	At rest. App data protected by iOS Data Protection; Keychain for tokens/IDs. D1 is encrypted at rest by the platform.
	•	Secrets. API keys/JWT secrets in Cloudflare Encrypted Secrets; manual quarterly review and rotation planned before GA.
	•	Access control. Only two core engineers have production access (MFA enabled). No back-office UI to view user content.
	•	Abuse control. Rate-limits (Durable Objects), Apple JWT validation, credits checks. We plan max size checks (e.g., ≤ 1.5 MB images) and stricter MIME validation before GA.
	•	Incident response. If a breach is suspected, we will revoke keys, investigate within 48 h, and—where required—notify regulators and affected users within 72 h.

⸻

7) Children

The App is intended for users 16+ and is not directed to children. Do not upload minors’ sensitive data. If you believe such data was submitted, please delete it in-app and contact us.

⸻

8) Region-Specific Notes

We operate one global policy and implement region-specific requirements where applicable (e.g., access/deletion rights; cross-border safeguards). If local laws grant you additional rights, we will honor them to the extent required.

⸻

9) Changes to This Policy

Because this is a beta, features and data handling may change. We will update this page with the effective date and, for material changes, provide a notice in-app.

⸻

10) Contact

Bridge Developer Team
privacy@bridge.app

⸻

Appendix — Data Map (Developer-Readable Summary)

Area	What	Stored Where	Kept For
Voice (STT)	.m4a temp → Worker relay → OpenAI STT	App temp (then deleted), Worker memory only, OpenAI systems	App: 0 s; Worker: 0 s; OpenAI: up to ~30 days (per its policy)
Photo	1600 px base64; EXIF/GPS removed	App SwiftData (optional); Worker memory only; OpenRouter transit	App: until user deletes; Worker: 0 s
Text & History	Inputs, results, summaries, imageData	App SwiftData (iOS Data Protection)	Until user deletes
Tokens/IDs	JWT/refresh/device UUID	iOS Keychain; D1 stores hashes and device IDs	Refresh tokens 30 days; revoked retained to prevent replay
Credits/Ledger	Balance, deltas, reasons, meta	Cloudflare D1 (encrypted at rest)	Target 5 years
Logs	Minimal error/metrics; no content	App OSLog; Worker console (debug-off by default)	No persistent content logs


⸻

Note on third-party models. We use OpenAI and OpenRouter to process content as described. We configure available settings to disable retention/training where possible. However, we do not control their internal operations and cannot guarantee deletion timelines. Use voice/photo features only if you consent to such processing.

⸻

End of Policy

⸻
