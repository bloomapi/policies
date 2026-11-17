# AI Use Policy

This policy covers the artificial intelligence (AI) services BloomText uses to process Customer data, and the rules workforce members follow when using AI. It applies alongside the [Approved Tools Policy](approved_tools_policy.md) and the [Risk Management Policy](risk_management_policy.md).

## Applicable Standards from the HIPAA Security Rule

* 164.308(a)(1)(ii)(A) - Risk Analysis
* 164.308(a)(1)(ii)(B) - Risk Management
* 164.308(b)(1) - Business Associate Contracts and Other Arrangements

## Approved AI Systems

All approved AI services are Google Cloud services, used under BloomAPI's Google Cloud business associate agreement (BAA) (see [Subprocessors](subprocessors.md)).

| System | What it does | What it receives | What is kept | Region |
| --- | --- | --- | --- | --- |
| Google Gemini on Vertex AI: spam screening | Checks an outbound text from an organization that is not yet verified, when BloomText's rules flag the text as possible spam or as unrelated to patient care. It never blocks, delays, or changes a message. | That one message's text as written, the names of the rules that fired, the organization's age in days, and how many patients it has texted this billing period. It is not sent patient names, phone numbers, or keys as separate fields; the message text itself may contain PHI. Vertex AI prompt caching is turned off for the project. | Only the model's labels, its confidence, and a reason code from a fixed list. The model's own free text is never stored, posted, or logged. Results are deleted after 90 days. | us-central1 |
| Google Gemini on Vertex AI: form-field detection | Suggests fillable fields on a form page. It runs only when a staff member clicks Auto-detect on a draft form, with one model call per page. | The image of that form page. | The suggested fields, as part of the draft form. | Vertex AI US multi-region endpoint |
| Google Cloud Translation | Translates patient messages and staff replies for patients who use another language. Organization administrators can turn translation off for their organization. | The message text being translated. | The translation, stored with the message. | us-central1 |

A new AI service, or a new use of an existing one with Customer data, requires approval from the Security Officer and a privacy review by the Privacy Officer before use. The service is then added to this table and to [Subprocessors](subprocessors.md).

## Data Rules

1. AI services receive only the minimum Customer data needed for their task.
2. BloomAPI does not use Customer data to train or fine-tune AI models, and must not opt in to any provider program that would let a provider train on it.
3. Workforce members must not enter PHI or other Customer data into AI tools that are not approved (see the [Approved Tools Policy](approved_tools_policy.md)).

## Human Oversight

1. **Spam screening.** Every spam-screening result is posted to an internal staff review channel, without the message text. The AI takes no action on its own. Staff confirm or overturn each verdict before any action is taken on the organization.
2. **Form-field detection.** Every field the AI detects is marked for staff to check. Staff review the marked fields before the form is used.
3. **Failures.** If the spam model fails or times out, the check is recorded and posted as "not checked by AI" and is handled manually. If form-field detection fails, no fields are added and staff place them by hand.

## Trustworthy AI

BloomAPI maps its AI controls to the characteristics of trustworthy AI in the NIST AI Risk Management Framework (AI RMF 1.0):

* **Valid and reliable:** staff review every spam verdict and every detected field; accuracy and false positives are reviewed each year (see Review below).
* **Safe:** the AI never blocks, delays, or changes a message, and model failures fall back to manual handling.
* **Secure and resilient:** services run in Google Cloud under BloomAPI's access controls; failures and timeouts are handled without the AI.
* **Accountable and transparent:** the Security Officer owns this policy; each verdict, with its reason code and confidence, is posted to staff.
* **Explainable and interpretable:** spam verdicts carry a reason code from a fixed list and name the rules that fired.
* **Privacy-enhanced:** minimum necessary data, prompt caching off, no model free text stored, 90-day deletion of spam results, no training on Customer data, and a Privacy Officer review of each new AI use.
* **Fair, with harmful bias managed:** a human makes every decision that affects an organization, and false positives are reviewed each year.

## Training

AI rules, including the ban on putting Customer data into unapproved AI tools, are covered in onboarding and in the annual security and HIPAA training (see the [Employees Policy](employees_policy.md)).

## Review

The Security Officer owns this policy. AI risk, including accuracy and false positives, is reviewed at least annually as part of the HIPAA risk analysis and whenever an AI service or its use changes. The Privacy Officer reviews the privacy impact of each change (see the [Risk Management Policy](risk_management_policy.md)).
