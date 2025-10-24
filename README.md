Bridge — Privacy Policy

Effective Date: 2025-10-22
Last Updated: 2025-10-24 (rev B)

Thank you for using Bridge (the “App”).
This Privacy Policy explains how we handle your information when you use the App, currently distributed for testing and limited public use.

Bridge is built with privacy-first principles: we do not run advertisements, do not sell personal data, and minimize all forms of storage.

⸻

1. Overview

Bridge enables on-device and cloud-assisted translation of voice, photos, and text.
We process limited data only as necessary to deliver these functions, and we delete or anonymize it once no longer needed.

⸻

2. Data We Handle

Voice and Audio

When you use voice translation:
	•	The App records short audio segments while you hold or tap the record button.
	•	These recordings are securely transmitted to our relay service, which forwards them to a trusted speech-recognition provider to convert speech into text, then returns the result.
	•	The relay service does not store or log audio content.
	•	Temporary audio files on your device are deleted immediately after conversion.
	•	The external provider may retain limited data for a short period in accordance with its own policy; we configure our systems to minimize such retention.

Photos

When you use photo translation or description:
	•	Images are captured through the App’s built-in camera.
	•	All location (EXIF/GPS) and device metadata are automatically removed before upload.
	•	The processed image is transmitted securely to our relay service, which forwards it to a language-processing provider for interpretation and then returns the result.
	•	The relay service does not persist or log image data.
	•	A copy of the photo and its translation/insight may remain in your local SwiftData storage until you delete it.

Text and History
	•	Your input text and prior messages are packaged into each translation request to preserve context and sent securely through our Cloudflare Worker to an external language-model provider (e.g., OpenRouter or equivalent).
	•	Bridge itself does not permanently store this content after the request completes, and our worker forwards it without additional logging in production.
	•	In limited developer builds, a debug flag (DEBUG_TRANSLATE) may temporarily log translation payloads to Cloudflare logs for testing. This flag is disabled in all public releases.
	•	On your device, translation results and history remain in protected local storage until you delete them.
	•	Bridge does not use analytics, advertising identifiers, or behavior-tracking SDKs.

Device & Diagnostic Data
	•	We collect minimal technical data (device type, system version, language, time zone) required to ensure compatibility and detect abuse.
	•	Network information such as IP addresses is handled transiently by our infrastructure provider for routing and security, not by Bridge itself.

Payment, Credits, and Trial Protection
	•	If you purchase translation credits or subscriptions, payment processing is handled entirely by Apple through In-App Purchase.
	•	We record transaction references, anonymized account identifiers, and credit balances to operate the service.
	•	To prevent abuse of free trial credits, we store a hashed, non-reversible user identifier and a flag indicating whether a user has already claimed a trial credit package.
	•	This hashed identifier contains no personally identifiable information and cannot be used to reconstruct your identity.
	•	We never store card numbers or billing details.
	•	Transaction and minimal account records are retained for up to five years for accounting and fraud prevention.

⸻

3. Why We Process Data

We process information solely for:
	1.	Delivering translations, transcriptions, and photo explanations through external AI providers.
	2.	Operating user accounts, credits, subscriptions, and trial eligibility.
	3.	Protecting our systems from abuse (including repeated trial redemption) and maintaining service reliability.
	4.	Meeting legal and accounting obligations.

We never use your data for model training or targeted marketing.

⸻

4. How Data Is Stored and Retained

Type	Storage Location	Retention
Audio & photo uploads (server relay)	In-memory transit via Cloudflare Worker	Deleted immediately after processing
Saved photos & insights (local)	On your device (SwiftData encrypted storage)	Until deleted by user
Text (translation requests)	Transit through Cloudflare Worker to provider	Transient, deleted after response
Local text & history	On your device (encrypted)	Until deleted by user
Account / credits / trial status	Encrypted database (minimal fields)	Up to 5 years
Access tokens	Secure system keychain	Rotated or invalidated within 30 days
Logs	Operational metrics (non-content)	Short-term, aggregated


⸻

5. Security Measures

We employ:
	•	End-to-end HTTPS/TLS encryption for all transmissions.
	•	OS-level encryption for on-device storage.
	•	Encrypted secrets and keys with scheduled rotation.
	•	Strict access control (limited to two authorized engineers).
	•	Rate limits, hashing, and validation to prevent automated abuse or duplicate trial claims.
	•	A security response plan for timely notification in case of any breach.

⸻

6. Third-Party Services

Bridge uses a small number of infrastructure and AI service providers:
	•	Cloud infrastructure provider – for secure request relaying, minimal database storage, and hashed-ID trial validation.
	•	Speech recognition provider – for converting audio to text.
	•	Language model provider (e.g., OpenRouter) – for processing text translation requests that may include previous conversation context.
	•	Apple – for authentication and payment processing.

Each provider processes data under its own privacy policy and may temporarily store data as described in their documentation.
We configure available options to disable logging and model training wherever possible, but cannot fully control their internal practices.
By using features that require these services, you consent to such processing.

⸻

7. International Transfers

Data may be routed through servers located in different countries to ensure global performance.
We rely on standard contractual safeguards or equivalent protection for such transfers when required by law.

⸻

8. Your Rights and Choices
	•	Delete locally: You may delete individual or all conversations and photos within the App.
	•	Delete account: Selecting “Delete Account” removes your account and credit data from our database.
	•	The trial eligibility record may be retained in hashed, anonymous form solely to prevent repeated free-trial claims.
	•	This record is no longer linked to any account or personal identifier.
	•	Data requests: Contact us to access or delete remaining records.
	•	Third-party data: Requests relating to external AI providers will be forwarded where feasible, but we cannot guarantee their deletion schedules.
	•	Opt-out: We do not sell, share, or use your information for advertising.

⸻

9. Children’s Privacy

Bridge is intended for users aged 16 and above.
We do not knowingly collect data from children.
If you believe a minor has submitted personal data, please delete the content and contact us for assistance.

⸻

10. Changes to This Policy

We may update this Policy to reflect feature or legal changes.
The “Last Updated” date will always indicate the current version.
Material updates will be announced within the App.

⸻

11. Contact

Bridge Developer Team
📧 nex.anointer850@passinbox.com

⸻

Summary Table (for App Store Transparency)

Category	Used For	Shared With Third Parties	Retention
Audio & photo uploads (server relay)	Speech and image processing via worker	Yes – speech / language provider	Transient (0 s after processing)
Saved photos & insights (local)	Viewing previous translations	No	Until deleted by user
Text inputs & prior messages	Translation via external AI model	Yes – language provider	Transient, deleted after response
Local text history	Local reference	No	Until deleted by user
Account & credits	Authentication / billing	Infrastructure provider	Up to 5 years
Hashed user ID & trial flag	Prevent duplicate trial redemption	Infrastructure provider	Retained in anonymous form after deletion
Diagnostic data	Reliability / abuse prevention	Infrastructure provider	Short-term, aggregated


⸻

Key principle: Bridge processes the minimum information required to function.
We do not permanently store voice or photo data on our servers, do not build behavioral profiles, and do not use your content to train AI models.

⸻

End of Privacy Policy
