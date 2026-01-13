### ServiceCost

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - service_id (integer)
  - country_id (integer, nullable)
  - cost (integer)
  - vat_required (boolean, default: false)
  - points (integer, nullable)
  - period_in_days (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo service (Service)

## External Data Dependencies

- Country Context
  - Required fields:
    - country_id
  - Source module: location
  - Usage: Identifies the country for which the service cost is defined
  - Access pattern: read-only
- Notes:
  - Country-specific pricing for services
  - Defines cost, VAT, points, and period
  - Should stay internal to the service
