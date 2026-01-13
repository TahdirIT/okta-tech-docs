### Product

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - name (translatable)
  - description (translatable, nullable)
  - delivery_required (boolean, default: false)
  - assembly_required (boolean, default: false)
  - customizable (boolean, default: false)
  - published (boolean, default: false)
  - targets (json, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany productCosts (ProductCost)

## External Data Dependencies

- Country Context
  - Required fields:
    - (via product_costs pivot)
  - Source module: location
  - Usage: Links product to countries through product costs
  - Access pattern: read-only
- Notes:
  - Physical/digital product catalog
  - Supports country-specific pricing
  - Should stay internal to the service
