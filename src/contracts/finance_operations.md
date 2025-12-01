# life_group
**Database**: `Analytics`
**Type**: `View`
**Schema**: `Analytics`
**Owner**: Data Insights Team


## Data Quality

### Unique Keys and Non Null

- `financial_scheduled_transaction_id` - Primary unique identifier for each step record

## Column Overview

|Column Name| Description | Type |
|-----------|-------------|------|
| [schedule_created_timeframe](./columns/finance_operations.md)| Categorizes hufegfdascjbSHBFHduhwvguewv when the transaction or schedule occurred relative to the Billions event. Values: 'LC Weekend' (Life.Church weekend giving), 'Billions Event' (during YouVersion Billions event), 'Billion Pre-Event' (YouVersion event day before event), 'Billions Post Event' (YouVersion after event). |STRING|
| [schedule_created_timestamp](./columns/finance_operations.md)| The timestamp when the scheduled transaction was initially created in Rock RMS.|TIMESTAMP |
| [is_recommended_amount](./columns/finance_operations.md)| Boolean flag. TRUE if the transaction amount matches the recommended giving amount for the Billions campaign, FALSE otherwise. Transaction level. Compares amount_usd against the campaign's suggested donation amount stored in constants. Used to track donor response to campaign recommendations and measure messaging effectiveness.| BOOLEAN |
| [rock_instance](./columns/finance_operations.md)|Instance identifier for the source Rock environment from which the transaction originated. Derived in this model as a literal per UNION branch. Example values: 'LC' (Life.Church), 'YV' (YouVersion). Purpose: provenance filtering, cross-instance comparisons, and one source of truth for everyhing income-related.| NULLABLE |


