### Package

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - parent_id (integer, nullable)
  - title (translatable)
  - description (translatable, nullable)
  - cover (string, nullable)
  - cost (decimal)
  - vat_required (boolean, default: false)
  - country_id (integer, nullable)
  - published (boolean, default: false)
  - targets (json, nullable)
  - unlimited_used (boolean, default: false)
  - max_used (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo mainPackage (Package)
  - hasMany subPackages (Package)
  - belongsToMany services (Service) via package_service
  - belongsToMany transactions (Transaction) via transaction_package

## External Data Dependencies

- Country Context
  - Required fields:
    - country_id
  - Source module: location
  - Usage: Identifies the country for which the package is defined
  - Access pattern: read-only
- Notes:
  - Service package/bundle
  - Supports parent-child package relationships
  - Can include multiple services
  - Should stay internal to the service
