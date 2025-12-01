**Database**: `analytics`  
**Type**: View  
**Schema**: `analytics`  
**Tags**: `analytics`  
**Owner**: Data Insights Team

## Data Quality

### Unique Keys
- `known_step_guid` - Primary unique identifier for each step record

### Non-Null Fields
- `rms_person_id` - Must always have a value

## Column Overview

| Column Name | Description | Type |
|------------|-------------|------|
| [known_step_guid](./columns/known_step_guid.md) | Unique identifier (GUID) | STRING |
| [known_step_id](./columns/known_step_id.md) | Step identifier | INTEGER |
| [rms_person_id](./columns/rms_person_id.md) | Person's RMS identifier | INTEGER |
| [primary_person_alias](./columns/primary_person_alias.md) | Person's primary alias | STRING |
| [name](./columns/name.md) | Full name of person | STRING |
| [known_step_type_name](./columns/known_step_type_name.md) | Type of step taken | STRING |
| [known_step_status](./columns/known_step_status.md) | Status of the step | STRING |
| [campus](./columns/campus.md) | Campus location | STRING |
| [start_date_time](./columns/start_date_time.md) | When step started | TIMESTAMP |
| [known_class_date](./columns/known_class_date.md) | Date of Known class | DATE |
| [known_class_size](./columns/known_class_size.md) | Number of attendees | INTEGER |
| [known_category](./columns/known_category.md) | Category of Known class | STRING |
| [known_next_step](./columns/known_next_step.md) | Next step information | STRING |
| [known_step_note](./columns/known_step_note.md) | Additional notes | STRING |

## Common Use Cases

### Track New Attendee Progress
Filter by `known_step_status` to see who has completed their next steps

### Campus-Level Reporting
Group by `campus` to see engagement by location

### Follow-Up Lists
Query records where `known_step_status` is "Started" but not "Completed"

## Related Views
- (Add related views here as they are documented)

## Questions?
Contact the **Data Insights Team** for more information about this view.