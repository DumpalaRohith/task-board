# Task Board
A simple Kanban style task board for teams or personal use. Create tasks, drag them across columns, track priority and due dates, see charts on the Metrics page, and ask a small built in chatbot about your board.

## Features
* Login and signup with secure passwords
* Drag and drop tasks across columns
* Columns are fully customizable, add or delete your own beyond the default four
* Task priority levels (P0 to P3) and optional due dates with overdue highlighting
* Search and filter tasks by assignee or priority
* Metrics page with charts for status, priority, and assignee breakdown
* A small chatbot that answers questions like "what is overdue" or "how many tasks are in progress"
* Works locally or fully dockerized

## Tech Stack
Frontend: React, TypeScript, Vite, Tailwind CSS, dnd kit for drag and drop, Recharts for charts

Backend: Node.js, Express, TypeScript, Mongoose

Database: MongoDB (Atlas cloud or local)

Auth: JWT tokens with bcrypt password hashing

Containers: Docker and docker compose (optional)

## Project Structure
    task-board/
      backend/            Express API, talks to MongoDB
      frontend/           React app, the actual UI
      docker-compose.yml  optional, runs mongo, backend, and frontend together

## Environment Files
Both `backend` and `frontend` need a small `.env` file for local settings like the database URL, the login secret, and the API URL. These files are never committed to GitHub since they can hold sensitive values. Instead, create your own based on the variables below.

`backend/.env`

    PORT=4100
    MONGO_URI=your_mongodb_connection_string_here
    JWT_SECRET=replace_this_with_a_real_secret

`MONGO_URI` can point to a free [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register) cluster, or a local MongoDB instance (e.g. `mongodb://localhost:27017/task-board`) if you'd rather not use the cloud.

`frontend/.env`

    VITE_API_URL=http://localhost:4100/api

## Running Locally
Make sure `MONGO_URI` in `backend/.env` points to a working database (Atlas cluster or local Mongo).

Start the backend.

    cd backend
    npm install
    npm run build
    npm start

Start the frontend in a new terminal.

    cd frontend
    npm install
    npm run dev

Then open the app at `http://localhost:5173`.

## Running With Docker
If you'd rather not manage MongoDB yourself, the whole app (including a local Mongo container) can run with one command.

    docker compose up --build

This starts MongoDB, the backend, and the frontend together, all connected. Update your `.env` files first if you're using this alongside Atlas, since Docker's internal networking may need a different `MONGO_URI` (typically `mongodb://mongo:27017/task-board` referencing the compose service name instead of `localhost`).

## Improvements
* If two people drag the same task into different columns at almost the same time, whoever clicks last just quietly wins and the other person never finds out their change got erased.
* If a task sits untouched for too long, its card could slowly change color as a gentle nudge that it is being ignored.
* For things you repeat every week, like a report, you set it up once and the board just makes a fresh task automatically each time, no retyping it forever.
