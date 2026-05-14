You are working on a new reusable service-business booking platform. Read `CLAUDE.md` and `ROADMAP.md` first. Follow the project rules exactly.

Task: Build Phase 1 only — the Backend Data Model.

Current goal:
Create the backend data model for a reusable appointment booking engine that can support Jones Barber Shop first, but must also support other service businesses later.

Default stack:
- TypeScript
- Node.js
- PostgreSQL
- Prisma ORM
- REST API later, but do not build API routes yet unless needed for project scaffolding

Scope for this task:
1. Inspect the repo.
2. Create a plan file in `plans/` named with today’s date and the task slug, for example `plans/YYYY-MM-DD-backend-data-model.md`.
3. Scaffold the minimum backend structure if it does not exist.
4. Add Prisma if not already present.
5. Create or update `prisma/schema.prisma`.
6. Define the core data models and enums.
7. Add `.env.example` entries for database connection only.
8. Create or update `docs/DATA_MODEL.md` explaining every model and relation.
9. Create or update `docs/ARCHITECTURE.md` only if backend structure is introduced.
10. Validate the Prisma schema.
11. Report changed files, validation result, risks, and next recommended slice.

Required models:
- Business
- Location
- Service
- StaffMember
- StaffService
- AvailabilityRule
- BlackoutWindow
- Customer
- Appointment
- SlotHold
- Payment
- NotificationEvent
- WebhookEvent

Required enums:
- BusinessStatus
- LocationStatus
- ServiceStatus
- StaffStatus
- AppointmentStatus
- PaymentStatus
- PaymentProvider
- NotificationChannel
- NotificationStatus
- WebhookProvider

Model requirements:
- The platform must support multiple businesses.
- A business can have multiple locations.
- A business can have multiple services.
- A business can have multiple staff members.
- A staff member can offer only selected services through `StaffService`.
- Services need duration, price, optional deposit, buffer before, and buffer after.
- Availability rules must be separate from appointments.
- Blackout windows must support blocking staff time, location time, or business-level time where practical.
- Customers must be scoped to a business.
- Appointments must reference business, location, service, customer, and optionally staff if “any available” is supported later.
- Appointment status must be separate from payment status.
- Slot holds must have expiration timestamps.
- Payments must support provider references such as Stripe payment intent/session IDs later.
- Webhook events must store provider event IDs so duplicate webhook processing can be prevented.
- Notification events must track SMS/email attempts separately from appointments.

Suggested appointment statuses:
- held
- pending_payment
- confirmed
- cancelled
- completed
- no_show
- expired

Suggested payment statuses:
- not_required
- requires_payment
- pending
- paid
- failed
- refunded
- partially_refunded

Rules:
- Do not build live availability calculation yet.
- Do not build payment checkout yet.
- Do not build Stripe webhooks yet.
- Do not send SMS or email yet.
- Do not build the frontend widget yet.
- Do not build an admin dashboard yet.
- Do not hardcode Jones Barber Shop into the core schema.
- Sample seed data may reference Jones Barber Shop only if it is clearly marked as sample data.
- Store timestamps in UTC.
- Store the business timezone explicitly.
- Prefer clear reusable naming: use `StaffMember`, not `Barber`, in the platform schema.

Validation:
- Run Prisma schema validation/generation.
- Run TypeScript checks if a TS project exists.
- Confirm no secrets were committed.
- Confirm the schema can support Phase 2 availability work.

Completion report format:
1. What was inspected
2. What was created or changed
3. Files changed
4. Validation run
5. Validation result
6. Known risks
7. Next recommended slice

Start by creating the plan, then implement only Phase 1.
