### Coupon

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - code (string)
  - title (translatable, nullable)
  - type (enum)
  - value (decimal)
  - max_discount (decimal, nullable)
  - min_balance (decimal, nullable)
  - active (boolean, default: false)
  - unlimited_discount (boolean, default: false)
  - unlimited_used (boolean, default: false)
  - applied_generally (boolean, default: false)
  - start_at (datetime, nullable)
  - end_at (datetime, nullable)
  - max_used (integer, nullable)
  - targets (json, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - hasMany transactions (Transaction)
  - morphToMany services (Service) via couponable
  - morphToMany serviceCosts (ServiceCost) via couponable
  - morphToMany packages (Package) via couponable
  - morphToMany products (Product) via couponable

## External Data Dependencies

- School Context
  - Required fields:
    - (via transactions)
  - Source module: school-management
  - Usage: Links coupon to schools through transactions
  - Access pattern: read-only
- Notes:
  - Discount coupon management
  - Supports fixed amount and percentage discounts
  - Can be applied to services, packages, and products
  - Supports usage limits and expiration dates
  - Should stay internal to the service
