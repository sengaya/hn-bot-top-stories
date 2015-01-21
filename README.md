Hacker News Bot Top Stories
===========================

This program is used to run a bot which posts the top stories of Hacker News to
Twitter. It uses the ~~unofficial HN API at http://api.ihackernews.com/~~ official HN API at https://github.com/HackerNews/API. The bot
posts stories to Twitter that reach a certain rank "N" on Hacker News.

Follow @hn_bot_top1 to see the bot in action:
https://twitter.com/hn_bot_top1

# Dependencies
pip install python-twitter

# Configuration
The bot needs some credentials for posting to Twitter:
- filename: hn-bot-top-stories.credentials
- ini-style:

```
    [hn_bot_topN]
    consumer_key = ...
    consumer_secret = ...
    access_token_key = ...
    access_token_secret = ...
```

- one section per bot (twitter account)

# Run
./hn-bot-top-stories N [...]
- need at least one argument N
- for multiple bots make sure to have a corresponding section in the credentials
  file
- usually invoked by cron

# Seen files
The program stores already posted stories in a simple file: seenN.db

# Known Bugs
As this bot runs every ~~5 minutes and uses api.ihackernews.com (which is great,
but quite often returns with an error 500)~~ 2 minutes (in my setup via cron), it can happen that the bot misses
stories that are on a certain rank only for a short time.

# Example
./hn-bot-top-stories 1 5 30
- requires 3 Twitter credentials (section [hn-bot-top1], [hn-bot-top5]
  and [hn-bot-top30])
- creates 3 seen files (seen1.db, seen5.db and seen30.db)
- fetch a list of current top stories
- if rank 1 is not in seen1.db, fetch story and post it to Twitter
- repeat this for rank 1-5 and 1-30
