# Next

**Next** is the private owner intelligence application within the Otya ecosystem, owned by Otya Hold Ltd.

## Ecosystem boundaries

- **Otya OS** is the unified platform.
- **Otya End** is the shared backend and integration layer (the current `Otya-Server` GitHub repository slug is a compatibility identifier, not the canonical product name).
- **OtyaPoint** is the shop/business operations application. Next may surface approved health and operational summaries, but must not bypass OtyaPoint's authorization or directly expose customer, staff, inventory, or financial records.
- **Otya Media** is the local-first media player; local playback must not depend on Next or a live backend.
- **OtyaHub** is the public developer/partner surface and must never receive owner-only controls, private infrastructure details, or credentials.
- **Next** is private and owner-only. It is an interface to approved backend capabilities, not a second backend or a privileged bypass.

Keep existing app IDs, repository slugs, API paths, and Cloudflare resource names unchanged until a separately reviewed compatibility migration is approved. Coordinate cross-product work through https://github.com/PeterSmartLink/Otya-Server/issues/236.

It is not a second backend and it is not a browser admin dashboard. Next is the secure Android-first interface to the existing OTYA intelligence and operations plane: conversation, voice, approvals, incidents, support, releases, system health, connected services, memory and device actions.

## Product direction

Next should feel like a persistent intelligent partner rather than a command console:

- natural text and real-time voice conversation
- interruption / barge-in during voice replies
- stable personality: friendly, professional, calm and lightly humorous when appropriate
- persistent context and operational memory
- proactive but restrained notifications
- system awareness across OTYA services
- reflection, verification and confidence-aware answers
- owner-only action approvals and biometric step-up
- Android assistant role and device capabilities where the OS permits them
- no secrets or infrastructure credentials stored in the APK

## Technology

### App

- Flutter 3.47.x / Dart for the primary UI and feature architecture
- Riverpod for application state and dependency injection
- go_router for navigation and deep links
- Dio + WebSocket for authenticated REST and real-time agent sessions
- Android Kotlin for assistant-role, voice interaction, notification access and device-level capabilities
- Android BiometricPrompt through Flutter local_auth for sensitive approvals
- Firebase Cloud Messaging for proactive owner alerts when the app is not active

### Backend

Next connects to the existing OTYA Cloudflare backend. Server-side intelligence remains server-side.

Target backend building blocks:

- Cloudflare Workers / existing OTYA services
- Cloudflare Agents SDK + Durable Objects for durable agent identity, state and real-time sessions
- Workers AI for default inference
- AI Gateway for observability, fallback/routing and provider control
- Cloudflare Voice for real-time STT / LLM / TTS transport where appropriate
- AI Search / Vectorize for private product and long-term semantic knowledge
- Workflows for durable multi-step operations
- D1 / Durable Object SQLite for structured state and audit history
- R2 for larger owner artifacts and reports
- FCM for Android wake-up notifications and urgent incident delivery

## Security boundary

The public OTYA Player and public Next surfaces must never inherit owner permissions.

Next uses the normal OTYA identity, then obtains a separate short-lived owner authorization after server-side role checks and step-up verification. High-impact operations require explicit approval and may require fresh biometric/server verification.

Never commit:

- Cloudflare API tokens
- Firebase Admin credentials
- Resend keys
- GitHub tokens / private keys
- signing keys
- internal service secrets
- owner access / refresh tokens

## Initial feature areas

- **Talk** — persistent owner conversation, voice and multimodal context
- **Pulse** — what needs attention now: health, incidents, crashes, releases and support
- **Activity** — what Next observed, investigated, changed, verified or is waiting on
- **Approvals** — sensitive actions awaiting owner authorization
- **Memory** — decisions, incidents, lessons and unresolved work
- **Connections** — GitHub, Cloudflare, Gmail/Resend, Firebase, Telegram and OTYA service status
- **Device** — assistant role, wake experience, notifications, media and approved phone actions
- **Settings** — personality, voice, permissions, autonomy, interruption policy, privacy and security

## Migration rule

Existing AI/admin capabilities are not copied into the client. Their browser UI is retired; Next is the sole owner experience. Privileged execution remains behind authenticated server APIs, with short-lived owner authorization, biometric step-up and explicit approval for high-impact actions.

See `docs/ARCHITECTURE.md` and `docs/MIGRATION_MAP.md`.
