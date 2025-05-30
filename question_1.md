## question : 
Suggest secondary indices based on expected query patterns. Consider factors such as
read performance, write amplification and storage overhead. How would you measure
the tradeoffs of adding these indices? Provide specific examples of queries that benefit
from indexing.


Sessions Table : 
1. read performance :
    should be able to fetch sessions for a given account_uid
    should be able to fetch session for a given account_uid and title
    should be able to fetch sessions for a given account_uid and deleted_at is null
- create index idx_sessions_account_uid on sessions (account_uid)
- create index idx_sessions_account_uid_title on sessions (account_uid, title)
- create index idx_sessions_account_uid_deleted_at on sessions (account_uid, deleted_at)

query pattern the indexes would help in : 
1. search all sessions for a account_uid
2. find the session for a account_uid with title as 'abc'
3. mark a session as deleted for a given account_uid


Agent Turns Table : 
1. read performance : 
    should be able to fetch agent turns for a given session_uid
    should be able to fetch agent turns for a given session_uid and parent_uid
    should be able to fetch agent turns for a given session_uid and active_child
- create index idx_agent_turns_session_uid on agent_turns (session_uid)
- create index idx_agent_turns_session_uid_parent_uid on agent_turns (session_uid, parent_uid)
- create index idx_agent_turns_session_uid_active_child on agent_turns (session_uid, active_child)

query pattern the indexes would help in : 
1. search all agent turns for a session_uid
2. find the agent turn for a session_uid with parent_uid as 'abc'
3. find the agent turn for a session_uid with active_child as 'abc' (this could be used to filter out agent turns which are actually working)

Human Turns Table : 
1. read performance : 
    should be able to fetch human turns for a given session_uid
    should be able to fetch human turns for a given session_uid and parent_uid
    should be able to fetch human turns for a given session_uid and active_child
- create index idx_human_turns_session_uid on human_turns (session_uid)
- create index idx_human_turns_session_uid_parent_uid on human_turns (session_uid, parent_uid)
- create index idx_human_turns_session_uid_active_child on human_turns (session_uid, active_child)

query pattern the indexes would help in : 
1. search all human turns for a session_uid
2. find the human turn for a session_uid with parent_uid as 'abc'
3. find the human turn for a session_uid with active_child as 'abc' (this could be used to filter out human turns which are actually working)

Steps Table : 
1. read performance : 
    should be able to fetch steps for a given agent_turn_uid
    should be able to fetch steps for a given agent_turn_uid and idx
- create index idx_steps_agent_turn_uid on steps (agent_turn_uid)
- create index idx_steps_agent_turn_uid_idx on steps (agent_turn_uid, idx)

query pattern the indexes would help in : 
1. search all steps for a agent_turn_uid
2. find the step for a agent_turn_uid with idx as 'abc'
