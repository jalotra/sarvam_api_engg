## Session Table : 

| Column Name | Data Type |
|-------------|-----------|
| uid | character varying |
| account_uid | character varying |
| title | character varying |
| created_at | timestamp with time zone |
| deleted_at | timestamp with time zone |


## Agent Turns

| Column Name | Data Type |
|-------------|-----------|
| uid | character varying |
| session_uid | character varying |
| parent_uid | character varying |
| active_child | character varying |
| liked | boolean |
| created_at | timestamp with time zone |

## Human Turns

| Column Name | Data Type |
|-------------|-----------|
| uid | character varying |
| session_uid | character varying |
| parent_uid | character varying |
| active_child | character varying |
| prompt | character varying |
| created_at | timestamp with time zone |

## Steps

| Column Name | Data Type |
|-------------|-----------|
| agent_turn_uid | character varying |
| idx | integer |
| tpe | integer |
| content | character varying |
| created_at | timestamp with time zone |