### Evaluate the tradeoffs of moving the Agent Turns, Human Turns and Steps table to ScyllaDB. Propose a denormalised schema, specifying partition and clustering keys. Discuss how data consistency, query performance and scalability would be affected. How would you measure the tradeoffs?


Denormalised Schema Observations : 
Session would also have some human and agent turns within it. 
And Agent Turns and Human Turns are kinda same table with some fields that are unique to each table
So we should be able to denormalise the agent turns and human turns table and session into a single table
Steps table is a child table of agent turns table

calling agent_turn and human_turn and session as conversation  
// this table should be able to solve all our query needs from question 1
CREATE TABLE conversation (
    session_id text,
    account_id text,
    turn_id text,
    turn_type text, <could be agent or human>
    parent_turn_id text,
    active_child_id text,
    liked boolean, <agent field>
    prompt text, <human field>, 
    turn_timestamp timestamp,
    created_at timestamp,
    deleted_at timestamp,
    session_title text,
    PRIMARY KEY ((session_id, account_id), turn_timestamp, turn_id)
) WITH CLUSTERING ORDER BY (turn_timestamp ASC, turn_id ASC);


CREATE TABLE steps (
    agent_turn_id text,
    session_id text,
    step_index int,
    step_type int,
    content text,
    created_at timestamp,
    account_id text,
    PRIMARY KEY ((session_id, agent_turn_id), step_index)
) WITH CLUSTERING ORDER BY (step_index ASC);

Measuring tradeoffs : 
1. will check for read and write latencies from moving to scylladb
    - Will check these numbers (p50, p95, p99)
2. will check storage amplification (write time)
    - exact data stored / requested by app layer should be minimal 
3. will check on network I/O usage 
    - will write materialised views for DTOs to reduce network I/O
4. will check write and read throughput 
    - which is the number of requests per second that we have hold in write and read path and then scale out (sycalla nodes) eventually

