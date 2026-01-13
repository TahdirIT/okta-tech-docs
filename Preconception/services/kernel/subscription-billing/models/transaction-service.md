### TransactionService

## Model Type
Operational Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - transaction_id (integer)
  - service_id (integer)
  - service_cost_id (integer, nullable)
  - cost (integer)
  - vat (integer, nullable)
  - vat_percentage (decimal, nullable)
  - discount_amount (decimal, nullable)
  - points (integer, nullable)
  - days (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo transaction (Transaction)
  - belongsTo service (Service)
  - belongsTo serviceCost (ServiceCost)
- Notes:
  - Individual service purchases within a transaction
  - Tracks cost, VAT, and discounts per service
  - Should stay internal to the service
