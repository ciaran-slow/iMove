<p align="center">
  <img src="./imove.jpg" width="100%">
</p>

# iMove GymMonkey

A full-stack gym workout tracker. Sign up, log your workouts with reps, load and an optional photo, edit or delete them, and comment on each one.

> An early project (2024), built to practise full-stack fundamentals with the MERN stack.

## Features

- **Accounts:** sign up and log in with email and password. Passwords are hashed with bcrypt, and login issues a JWT valid for 3 days.
- **Workouts (CRUD):** create, view, edit and delete workouts with a title, reps and load.
- **Photo upload:** attach an image to a workout, stored in AWS S3 via multer-s3.
- **Comments:** add, edit and delete comments on a workout.
- **Responsive React UI** with protected routes (logged-out users are redirected to log in).

## Tech stack

| Layer | Tools |
|---|---|
| Frontend | React, Vite, React Router, Axios, date-fns |
| Backend | Node.js, Express, Mongoose |
| Database | MongoDB Atlas |
| Storage | AWS S3 (multer-s3) |
| Auth | bcryptjs, jsonwebtoken, validator |
| Hosting | Vercel |

## Project structure

```
backend/    Express API (routes, controllers, Mongoose models)
frontend/   React app (components, context, hooks)
```

## Running it locally

You'll need Node.js, a MongoDB Atlas cluster and an S3 bucket.

**Backend** (runs on port 4000)

```sh
cd backend
npm install
npm run dev
```

Create `backend/.env`:

```
MONGODB_USERNAME=
MONGODB_PASSWORD=
SECRET=              # any long random string, used to sign JWTs
AWS_REGION=
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
```

Note: the Atlas cluster host is set in `backend/server.js` and the S3 bucket name in `backend/routes/workouts.js`. Change both to your own.

**Frontend**

```sh
cd frontend
npm install
npm run dev
```

Create `frontend/.env`:

```
VITE_API_BASE_URL=http://localhost:4000
VITE_APP_URL=
VITE_AWS_BUCKET_NAME=
VITE_AWS_REGION=
```

## API

| Method | Route | Purpose |
|---|---|---|
| POST | `/api/user/signup`, `/api/user/login` | Create an account / log in |
| GET, POST | `/api/workouts` | List workouts / create one (multipart, optional `image`) |
| GET, PATCH, DELETE | `/api/workouts/:id` | Read, update or delete a workout |
| POST | `/api/comments/workouts/:workoutId/comments` | Add a comment |
| PATCH, DELETE | `/api/comments/workouts/:workoutId/comments/:commentId` | Edit or delete a comment |
