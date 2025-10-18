# Data Relationships - Gigs Analytics

## Entity Relationship Diagram

```
┌─────────────────────────────────────┐
│         PROJECTS                    │
│─────────────────────────────────────│
│ PK: project_id__hashed              │
│─────────────────────────────────────│
│ • project_type                      │
│ • organization_name                 │
│ • device_type                       │
└─────────────────────────────────────┘
           │                    │
           │ 1                  │ 1
           │                    │
           │ N                  │ N
           ▼                    ▼
┌─────────────────────┐   ┌──────────────────────────────────────┐
│ PLAN_CHANGE_EVENTS  │   │ USAGE_BY_SUBSCRIPTION_PERIOD         │
│─────────────────────│   │──────────────────────────────────────│
│ PK: plan_id         │   │ PK: subscription_id                  │
│─────────────────────│   │──────────────────────────────────────│
│ FK: project_id__    │   │ FK: project_id__hashed               │
│     hashed          │◄──┤ FK: plan_id                          │
│                     │ N │                                      │
│ • plan_created_at   │ 1 │ • reporting_date                    │
│ • event_type        │   │ • subscription_period_start         │
│ • event_timestamp   │   │ • subscription_period_end           │
│ • plan_name         │   │ • subscription_period_number        │
│ • network_provider  │   │ • cumulative_data_usage_megabyte    │
│ • price_currency    │   │ • cumulative_voice_usage_minutes    │
│ • plan_price_amount │   │ • cumulative_sms_usage              │
│ • data_allowance_mb │   │ • number_of_addons_activated        │
│ • is_unlimited_data │   │                                      │
│ • voice_allowance   │   │                                      │
│ • sms_allowance     │   │                                      │
│ • validity_value    │   │                                      │
│ • validity_unit     │   │                                      │
│ • _valid_from       │   │                                      │
│ • _valid_to         │   │                                      │
│ • _is_current_state │   │                                      │
└─────────────────────┘   └──────────────────────────────────────┘
```

## Relationships

### 1. PROJECTS ↔ PLAN_CHANGE_EVENTS (1:N)

- **Cardinality**: One project can have many plans
- **Foreign Key**: `project_id__hashed` in PLAN_CHANGE_EVENTS → `project_id__hashed` in PROJECTS
- **Description**: Each project/organization can create and manage multiple mobile plans over time. The plan_change_events table tracks all lifecycle events (created, updated, published, archived) for each plan.

### 2. PROJECTS ↔ USAGE_BY_SUBSCRIPTION_PERIOD (1:N)

- **Cardinality**: One project can have many subscriptions
- **Foreign Key**: `project_id__hashed` in USAGE_BY_SUBSCRIPTION_PERIOD → `project_id__hashed` in PROJECTS
- **Description**: Each project can have multiple subscriptions tracking usage data across different subscription periods.

### 3. PLAN_CHANGE_EVENTS ↔ USAGE_BY_SUBSCRIPTION_PERIOD (1:N)

- **Cardinality**: One plan can be used by many subscriptions
- **Foreign Key**: `plan_id` in USAGE_BY_SUBSCRIPTION_PERIOD → `plan_id` in PLAN_CHANGE_EVENTS
- **Description**: Each plan can have multiple subscriptions, with each subscription tracking usage metrics over specific time periods.

## Key Characteristics

### PROJECTS (3 records)

- **Primary Key**: `project_id__hashed` (hashed identifier for privacy)
- **Purpose**: Represents organizations/companies using the platform
- **Types**: API (People Mobile), Connect (ACME Phone, SmartDevices Inc.)
- **Device Types**: Phones, Wearables

### PLAN_CHANGE_EVENTS (211 records shown, temporal/event-sourced)

- **Primary Key**: `plan_id`
- **Purpose**: Event-sourced table tracking complete lifecycle of mobile plans
- **Event Types**: `plan.created`, `plan.updated`, `plan.published`, `plan.archived`
- **Temporal Fields**: `_valid_from`, `_valid_to`, `_is_current_state` for time-based queries
- **Plan Features**: Data, Voice, SMS allowances with pricing information

### USAGE_BY_SUBSCRIPTION_PERIOD (Large dataset, 53,000+ records)

- **Primary Key**: `subscription_id`
- **Purpose**: Tracks actual usage metrics per subscription period
- **Metrics**: Data usage (MB), voice usage (minutes), SMS count, add-ons
- **Time Tracking**: Subscription periods with start/end dates and period numbers

## Data Model Notes

1. **Many-to-Many Relationship**: PROJECTS and PLAN_CHANGE_EVENTS are connected through USAGE_BY_SUBSCRIPTION_PERIOD, forming a many-to-many relationship where:

   - Projects define plans
   - Plans are subscribed to by users
   - Usage data links specific projects to specific plans through subscriptions

2. **Temporal Data**: PLAN_CHANGE_EVENTS uses event sourcing with `_valid_from` and `_valid_to` timestamps to maintain historical state changes.

3. **Privacy**: Project identifiers are hashed for data privacy/security.
