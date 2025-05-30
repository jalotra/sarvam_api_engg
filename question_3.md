### Define key queries that should be supported for analytics and evaluation? For the latter, refer to the offerings of vendors like Langfuse and Arize. Provide query examples and discuss how they would be optimised in both relational and NoSQL environments

For Analytics : 
Sessions : 
1. Unique sessions in a day 
2. Average agent turns per session in last day 
3. average like rate per session in last day 
Step Type Histogram 
1. averae steps taken per agent run in last day 
1. average content size generated per step

SQL for these : 
1. select count(*) from conversation where deleted_at is null and created_at >= now() - interval '1' day;
2. select avg(agent_turns) from conversation where deleted_at is null and created_at >= now() - interval '1' day;
3. select avg(like_rate) from conversation where deleted_at is null and created_at >= now() - interval '1' day;
4. select agent_turn_id, avg(step_count) from steps where deleted_at is null and created_at >= now() - interval '1' day 
group by agent_turn_id;
5. select agent_turn_id, avg(content_size) from steps where deleted_at is null and created_at >= now() - interval '1' day 
group by agent_turn_id;





