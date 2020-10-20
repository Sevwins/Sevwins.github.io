# Sevwins Support Engineering Interview

_It might take you an hour to run through some bubble tutorials. Don’t spend more than 8 hours on the total exercise. This is the max I would expect anyone to contribute to a development interview test.
If you don’t get everything completed, be prepared to explain why you picked the completed items based on some prioritization logic.
If Bubble is too much of a learning curve then focus on the other exercises so I can understand how you approach prioritizing your workload._

**Before you start, anticipate how long it will take to complete and [schedule a follow up meeting](https://calendly.com/jr-sevwins/interview) with John to review your work.**

Email: [john@sevwins.com](mailto:john@sevwins.com) with questions


## Exercises
#### 1. Learn Sevwins Concepts
Review the [Sevwins Demo App](https://demo.sevwins.com/) and [How it Works](https://www.sevwins.com/how-it-works) video to understand what we are building.

#### 2. Learn some Bubble

Pick any aspect of the demo app to replicate. It doesn’t have to look like it, just try to build some component of it that you think you might be able to tackle while learning something about Bubble.

  Some examples are:

  - Replicate one of the text-based input forms, storing the inputs and the user in a new database table (Bubble calls tables “Things”)
  - Build the team roster list view. Create a database table with some sample data and display the data in a list table view

- think and explain

  - What challenges or limitations might you predict based on what you built?
What would you do differently to make it more reliable and/or scalable?
What are some security-related concerns or questions might you have with this data?


#### 3. Onboarding Controls

- think and explain

  - Notice that the first time you hit a page there are popup onboarding tips. No need to build. Explain how you might track each of these for a user so they only show up once.

#### 4. Usage Analytics

- think and explain

  - Review the entire demo, build a list of events (clicks, views, ..) that might be worth tracking to better understand how users are using the product. What might you be able to tell from these usage metrics?
  - How could we capture, store, and report on the events to learn more about the user experience?

#### 5. Architecture

- think and explain

  - Bubble provides the ability to run workflows on the client or server. Not unique to bubble, just standard web site/app logic without code. List some cases where it is better to process on the client-side (browser) and explain why.
  - Same with server (backend) processing.
  - We send SMS notifications to all users based on the program schedule. For example, all daily assessments are sent at 12:00pm in the user’s time zone. As we scale the user base if we start to experience bottlenecks at these peak times what are some options to reduce the peak bottleneck?

#### 6. Coding
Build a function to accomplish the following in Javascript or Python (select language of your choice if you aren't proficient in these):

You receive the following payload representing two new user accounts

**Users**

```javascript
[
  {"full_name": "Coach LA",
  "Organization": "Test",
  "_id": "1589492405498x518184698125008450",
  "timezone": "America/Los_Angeles"},
  {"full_name": "Coach NY",
    "Organization": "Test",
    "_id": "1589492405498x518184698125008367",
    "timezone": "America/New_York"}
]
```

**Topics**

You get the following payload representing schedule configurations

- start_day_int - day of week for when this task runs for the first time (0=Sunday)
- hour - time of day this task runs
- weekly_count - how many times the task runs every week

```javascript
[
  {"active": "True", "name": "Weekly Goals", "program": "1577400952751x443095658217689900", "start_day": "Monday", "Created Date": "2019-12-26T22:59:17.757Z", "Created By": "1574873635764x839567162674233300", "Modified Date": "2020-07-20T17:47:51.810Z", "form": "form_goals", "start_day_int": 0, "weekly_count": 1, "hour": 8, "category": "Goals", "_id": "1577401157757x608309369383979100", "_type": "custom.sw_prgm_topic"},

  {"active": "True", "name": "Daily Assessment", "program": "1577400952751x443095658217689900", "start_day": "Monday", "Created Date": "2019-12-26T22:59:56.758Z", "Created By": "1574873635764x839567162674233300", "Modified Date": "2020-07-20T17:47:47.798Z", "form": "form_assess", "start_day_int": 0, "weekly_count": 7, "hour": 12, "category": "Assess", "_id": "1577401196758x439688071809190660", "_type": "custom.sw_prgm_topic"},

  {"active": "True", "name": "Weekly Reflection", "program": "1577400952751x443095658217689900", "start_day": "Sunday", "Created Date": "2019-12-26T23:01:12.534Z", "Created By": "1574873635764x839567162674233300", "Modified Date": "2020-07-20T17:47:43.033Z", "form": "form_reflect", "start_day_int": 6, "weekly_count": 1, "hour": 20, "category": "Reflect", "_id": "1577401272534x606016218540235800", "_type": "custom.sw_prgm_topic"}
]
```


**Logic to Build**

- For each user, generate a list of tasks for the next week starting on the following Sunday
- For reference, Reflection happens on Sunday, Weekly Goals happen on Monday, and Daily Assessments happen every day

**Output**

  - name: name from topic record
  - topic: id from topic record
  - date: calculated epoch ms date value based on the topic start_day_int, weekly_count, and hour in the user's timezone
  - calculate based on the users timezone, must be dynamic for any timezone, don't just simple use hour offset
  - user: id from the user list

```javascript
[
  {"name":"Weekly Goals","topic":"1577401157757x608309369383979100","status":"Waiting","date":1601294400000,"user":"1589492405498x518184698125008450"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601308800000,"user":"1589492405498x518184698125008450"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601395200000,"user":"1589492405498x518184698125008450"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601481600000,"user":"1589492405498x518184698125008450"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601568000000,"user":"1589492405498x518184698125008450"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601654400000,"user":"1589492405498x518184698125008450"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601740800000,"user":"1589492405498x518184698125008450"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601827200000,"user":"1589492405498x518184698125008450"},
  {"name":"Weekly Reflection","topic":"1577401272534x606016218540235800","status":"Waiting","date":1601856000000,"user":"1589492405498x518184698125008450"},
  {"name":"Weekly Goals","topic":"1577401157757x608309369383979100","status":"Waiting","date":1601294400000,"user":"1589492405498x518184698125008367"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601308800000,"user":"1589492405498x518184698125008367"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601395200000,"user":"1589492405498x518184698125008367"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601481600000,"user":"1589492405498x518184698125008367"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601568000000,"user":"1589492405498x518184698125008367"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601654400000,"user":"1589492405498x518184698125008367"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601740800000,"user":"1589492405498x518184698125008367"},
  {"name":"Daily Assessment","topic":"1577401196758x439688071809190660","status":"Waiting","date":1601827200000,"user":"1589492405498x518184698125008367"},
  {"name":"Weekly Reflection","topic":"1577401272534x606016218540235800","status":"Waiting","date":1601856000000,"user":"1589492405498x518184698125008367"}
]
```

**Integration**

POST the payload to a test REST API endpoint such as [Requestbin](https://requestbin.com) to replicate sending the payload to a 3rd party system

**Share**

Be prepared to share your script and demonstrate pushing the output to requestbin or other test endpoint.
