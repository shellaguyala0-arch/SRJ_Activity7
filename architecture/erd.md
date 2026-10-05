# Diagram 11 – Entity Relationship Diagram (DRAFT)

```mermaid
erDiagram

    users {
        uuid id PK
        string full_name
        string email UK "PII"
        string phone_number "PII"
        string password_hash
        string role "UserRole"
        timestamp created_at
    }

    driver_profiles {
        uuid id PK
        uuid user_id FK
        string plate_number "PII"
        string vehicle_type
        boolean is_available
    }

    ride_bookings {
        uuid id PK
        uuid rider_id FK
        uuid driver_profile_id FK "nullable"
        string pickup_point "PII"
        string destination
        timestamp scheduled_at
        decimal estimated_fare
        string status "BookingStatus"
        timestamp created_at
    }

    location_updates {
        uuid id PK
        uuid driver_profile_id FK
        decimal latitude "PII"
        decimal longitude "PII"
        timestamp recorded_at
    }

    notifications {
        uuid id PK
        uuid user_id FK
        string message
        boolean is_read
        timestamp sent_at
    }

    users ||--o| driver_profiles : has
    users ||--o{ ride_bookings : requests
    users ||--o{ notifications : receives
    driver_profiles ||--o{ ride_bookings : serves
    driver_profiles ||--o{ location_updates : reports
```

### Key

- **PK** = Primary Key
- **FK** = Foreign Key
- **UK** = Unique Key
- **PII** = Personal Information; restrict access
- `o` = zero allowed
- `|` = exactly one
- Crow's foot = many
