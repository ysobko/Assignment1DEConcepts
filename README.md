# Assignment1DEConcepts

I found nested json dataset on github and downloaded with this link https://www.gharchive.org.
The one https://data.gharchive.org/2015-01-01-15.json.gz which is 26,1 mb.

1. Data Loading

First i loaded the JSON file into DuckDB as raw unstructured data. Query:

<img width="589" height="88" alt="Screenshot 2026-01-28 at 15 13 19" src="https://github.com/user-attachments/assets/6b22a9c0-c0d4-4fed-9d9d-7d41fffa69f6" />

From the output we can see that there are nested fields are actor, repo, and payload, they store objects and arrays inside objects.

<img width="1446" height="717" alt="Screenshot 2026-01-28 at 15 02 45" src="https://github.com/user-attachments/assets/d8e00df6-9659-4679-8e41-4a56246ff021" />


2. Data Parsing

Here i extracted nested fields actor and repo and converted timestamps to SQL TIMESTAMP. I didn't change payload field as i would do it later. Query:

<img width="469" height="265" alt="Screenshot 2026-01-28 at 15 14 24" src="https://github.com/user-attachments/assets/e8ff7082-d19d-4caf-8c0b-0ccf58906869" />

Now we can see a structured and readable data in separate columns with actor_login, actor_id, repo_name, repo_url and repo_id info.

<img width="1396" height="690" alt="Screenshot 2026-01-28 at 15 19 10" src="https://github.com/user-attachments/assets/44b69de0-c0bd-4875-a9a9-3f848af92c77" />


Also in payload commit field the commits were stored as a list. I made so that each commit becomes a separate row in the table. It also skips events without commits. (null) Query:

<img width="356" height="249" alt="Screenshot 2026-01-28 at 15 20 49" src="https://github.com/user-attachments/assets/ac04312d-34d9-4795-bfea-bfb19b655cc9" />

So the output shows commit data where each row represents a single commit from a github event with an additional info about author login.

<img width="1415" height="694" alt="Screenshot 2026-01-28 at 15 26 29" src="https://github.com/user-attachments/assets/ee84e415-c78d-418d-8bed-4c8be016f804" />


3. Data Analysis Using Window Functions

1 Insight: Top 10 repositories by number of events. Query:

<img width="535" height="188" alt="Screenshot 2026-01-28 at 15 32 01" src="https://github.com/user-attachments/assets/5824e50a-15ac-4894-820c-be1c90d131bf" />

The result shows top 10 most active repos based on the total number of github events. They are the most active.

<img width="752" height="367" alt="Screenshot 2026-01-28 at 15 31 56" src="https://github.com/user-attachments/assets/c6fcc208-110f-49e8-a4a7-3541fa73ed64" />

2 Insight: Top 3 users per event type. Query:

<img width="342" height="613" alt="Screenshot 2026-01-28 at 15 36 10" src="https://github.com/user-attachments/assets/284d106b-5bf1-4144-8276-85c0e1bbfd58" />

Here the result ranks top 3 users by their activity for each event type. It shows the most active users inside each category of github events.

<img width="958" height="750" alt="Screenshot 2026-01-28 at 15 37 13" src="https://github.com/user-attachments/assets/44417282-11b0-49c4-8c3d-e2573859f537" />

4. Optional Task Visualization

I created a bar chart to visualize top 10 repositories by number of events.

<img width="978" height="609" alt="Screenshot 2026-01-28 at 15 39 50" src="https://github.com/user-attachments/assets/3bee08c7-8f84-408a-aad4-869cb9fba87e" />





