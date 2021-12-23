# NaNoWrim.io
#### By Donovan Gallaway

## Project Summary

![Writing](https://i.imgur.com/A6Oox8l.jpeg)

This is a writing accountability app that tracks word count quotas for a given day and lets you know when you're done. In this way, it's designed to keep you accountable.

The inspiration was for National Novel Writing Month (November), the challenge is to write 50k words in a month. It's a lot, but the hardest thing about it is consistency. As such, this helps track daily progress.

I put it together with Svelte for a nice SPA feel, but allowing for much faster rendering than React for longer state changes in forms, as well as just a generally fast experience. You know, sleek. Even "svelte"

## Models

In current implementation, it's one CRUD model

- Username: (String)
- Word Goal: (Number)
- Goal Met: (Boolean)
- Text: (String)
- File Link: (String)

User Auth is the next logical step, though there were some issues.

## Route Table

### Backend Routes

| url | method | action |
|-----|--------|--------|
| /goals/ | get | show all available goals in database (index)|
| /goals/ | post | add goal to database (create)|
| /goals/:id | get | API request to edit information about the goal (update)|
| /goals/:id | delete | delete a goal (delete/destroy)|


## User Stories

A user should be able to:
- Add a goal
- Type directly into the text area for his goal (or paste text)
- Set a word count goal for the day
- Be updated when that goal has been met (though not annoyingly, so as to allow them to continue writing)

## Challenges

Some minor things, mostly just learning curve for Svelte. However, the biggest unsolved problem is just User Auth. I have it fully functioning in terms of token authentication, but I haven't been able to work out getting the queries passed anonymously. The 

## List of Technologies

- MongoDB/Mongoose
- Express.JS
- Svelte.JS