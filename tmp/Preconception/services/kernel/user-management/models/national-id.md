### National ID

## Model Type
Reference Model

- Fields:
  - id (integer)
  - iam_id (integer)
  - national_id_hash (string)
  - national_id_masked (string)
  - verified_by_nafath (bool)
  - created_at (timestamp)
  - updated_at (timestamp)
  - deleted_at (timestamp, nullable)

- Relations:
  - belongsTo iam (IAM) — Part of **User** core aggregate; access via `user.iam.nationalIdentity`

- Notes:
  - National identity information model; part of the **User** core aggregate.
  - Stores government-issued identification numbers.
  - Should stay internal to the service for security and compliance.
  - No ULID: references IAM via `iam_id`; internal-only model, never exposed externally.
