# Deployment Guide

This guide provides step-by-step instructions for deploying the MERN stack application. The application is divided into a frontend (React) and a backend (Node.js/Express) which should be deployed separately.

## 1. Database: MongoDB Atlas

1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) and create a free account or log in.
2. Create a new Project, then build a Database (select the free shared tier).
3. Under **Security > Database Access**, create a new database user with a username and password. **Keep this password safe**.
4. Under **Security > Network Access**, click "Add IP Address" and select "Allow Access From Anywhere" (`0.0.0.0/0`) or enter the static IPs of your backend hosting provider.
5. Click **Connect > Connect your application** and copy the connection string. Replace `<password>` with your database user's password.

## 2. Backend: Render (or Railway)

Render is a great platform for hosting Node.js applications for free.

1. Push your entire project to a GitHub repository.
2. Go to [Render](https://render.com/) and sign up.
3. Click **New +** and select **Web Service**.
4. Connect your GitHub account and select your repository.
5. Configure the Web Service:
   - **Name**: `mern-app-backend`
   - **Root Directory**: `server`
   - **Environment**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `node server.js`
6. Scroll down to **Environment Variables** and add the following:
   - `PORT` = `10000` (Render defaults)
   - `MONGO_URI` = `[Your MongoDB Atlas Connection String]`
   - `JWT_SECRET` = `[A secure random string of your choice]`
   - `NODE_ENV` = `production`
7. Click **Create Web Service**. Render will build and deploy your backend.
8. Once deployed, copy the Render URL (e.g., `https://mern-app-backend.onrender.com`).

## 3. Frontend: Vercel

Vercel provides excellent hosting for React/Vite applications.

1. Go to [Vercel](https://vercel.com/) and sign up with GitHub.
2. Click **Add New... > Project**.
3. Import your GitHub repository.
4. Configure the Project:
   - **Framework Preset**: `Vite`
   - **Root Directory**: `client`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
5. Open **Environment Variables** and add:
   - `VITE_API_URL` = `[Your Render Backend URL]/api` (e.g., `https://mern-app-backend.onrender.com/api`)
6. Click **Deploy**. Vercel will build and deploy your frontend.
7. Once finished, Vercel will provide a live link to your application!

## Running Locally

1. Create a `.env` file in the `/server` directory and add:
   ```env
   PORT=5000
   MONGO_URI=your_local_or_atlas_mongo_uri
   JWT_SECRET=super_secret_key
   ```
2. Open two terminal instances:

   **Terminal 1 (Backend):**
   ```bash
   cd server
   npm run dev
   ```
   *(Note: You'll need to install `nodemon` locally or run `node server.js` if you don't have it.)*

   **Terminal 2 (Frontend):**
   ```bash
   cd client
   npm run dev
   ```
3. Visit `http://localhost:5173` in your browser.
