### ProductCost

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - product_id (integer)
  - country_id (integer)
  - cost (decimal)
  - vat_required (boolean, default: false)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo product (Product)

## External Data Dependencies

- Country Context
  - Required fields:
    - country_id
  - Source module: location
  - Usage: Identifies the country for which the product cost is defined
  - Access pattern: read-only
- Notes:
  - Country-specific product pricing
  - Should stay internal to the service
