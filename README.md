# Trending Posts Leaderboard — Scaffold

Build a trending leaderboard backed by a Redis **sorted set** (ranking) + a **hash per post** (metadata), reading the whole board in **one pipelined round trip**.

## Setup

```bash
npm install
cp .env.example .env       # local Redis works out of the box
docker start redis-m4      # make sure Redis is running (from LU 4.0.1)
```

## What to implement

- **`leaderboard.js`** — `upvote(postId)` (one atomic `ZINCRBY`) and `getTop(n)` (`ZREVRANGE` + one pipelined `HGETALL` per id).
- **`seed.js`** — load 100 fake posts (a hash per post + a sorted-set member each), using one pipeline.

## Run it

```bash
npm run seed    # loads 100 posts
npm test        # upvotes post:50 fifty times, asserts it reaches the top 10
```

Expected: the test prints the top 10 and ends with `PASS ✅`.

## Submit

Fork → branch → commit → open a PR against your fork. Submit the PR link. Do **not** commit `.env` or `node_modules/`.
