### Service

## Model Type
Reference Model

- Fields:
  - id (integer)
  - ulid (string, unique)
  - code (string, nullable)
  - title (translatable)
  - description (translatable, nullable)
  - period_related (boolean, default: false)
  - points_related (boolean, default: false)
  - published (boolean, default: false)
  - cover (string, nullable)
  - targets (json, nullable)
  - service_provider_id (integer, nullable)
  - created_at (timestamp)
  - updated_at (timestamp)
- Relations:
  - belongsTo serviceProvider (ServiceProvider)
  - hasMany serviceCosts (ServiceCost)
  - belongsToMany requirements (Service) via service_requirement
  - belongsToMany packages (Package) via package_service

## External Data Dependencies

- Permission Context
  - Required fields:
    - (via permission_service pivot)
  - Source module: roles-permissions
  - Usage: Links service to permissions for feature-based access control
  - Access pattern: read-only

- School Context
  - Required fields:
    - (via morphToMany as subscriber)
  - Source module: school-management
  - Usage: Links service to schools that subscribe to it
  - Access pattern: read-only
- Notes:
  - Service catalog item
  - Supports period-based and points-based subscriptions
  - Can have service requirements (dependencies)
  - Core service definition - should stay internal to the service
