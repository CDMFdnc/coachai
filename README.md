# coachai
# CoachAI

An AI fitness and life coaching app. You set up your profile and goal, and the app builds your training and nutrition plan, then keeps coaching you day to day.

> Status: working mobile app running against a local backend. Tested with a small group of users.


<p>
  <img src="docs/onboarding.png" width="200">
  <img src="docs/plan.png" width="200">
  <img src="docs/coach-chat.png" width="200">
  <img src="docs/food-scan.png" width="200">
</p>

## Features

- Onboarding that builds a personalized training and nutrition plan
- 24/7 coach chat
- Food photo scanning for macros
- "Today" view with the day's plan
- Journal and habit tracking

## Architecture

```
React Native (Expo) app
        │
     FastAPI  ──────  PostgreSQL
        │
  Celery workers  ──  Redis (queue)
        │
     LLM / vision APIs
```

Slow work (plan generation, image analysis) runs in Celery workers so the API stays responsive. Everything runs in Docker.

## What testers changed

I put the app in front of a small group before building further. Their feedback reshaped the focus toward emotional support and features for women, and set the pricing range. Building the next feature only after people actually used the last one saved me a lot of wasted work.

## Running locally

```bash
git clone https://github.com/CDMFdnc/coachai.git
cd coachai
cp .env.example .env        # add your own API keys
docker compose up --build   # backend: FastAPI, Celery, Redis, Postgres

cd mobile
npm install
npx expo start              # open in Expo Go on your phone
```

## Tech

React Native (Expo) · FastAPI · Celery · Redis · PostgreSQL · Docker
