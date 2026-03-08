### Name

## Model Type
Reference Model

- Fields:
  - id (integer)
  - user_id (integer)
  - locale (string)
  - name (string)

- Relations:
  - belongsTo user (User)

- Notes:
  - Flexible separated table for localized user names (e.g. ar, en).
  - Replaces name_ar / name_en columns. Query by locale for display; search across locales via joins.
  - Part of the **User** core aggregate. Accessed via `user.names`; never exposed directly in APIs/URLs.
  - No ULID: lookup table; use `user.iam.ulid` when external identifier is needed.
