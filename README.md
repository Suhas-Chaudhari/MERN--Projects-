# 🌍 TravelMemory — MERN Stack Deployment on AWS EC2

A full-stack Travel Memory application built with the **MERN stack** (MongoDB, Express, React, Node.js) and deployed on **AWS EC2**.

---

## 📋 Table of Contents

- [EC2 Instance Details](#ec2-instance-details)
- [Configuring EC2](#configuring-ec2)
- [Configure MongoDB Database](#configure-mongodb-database)
- [Deploy Node.js Backend](#deploy-nodejs-backend)
- [Deploy React Frontend](#deploy-react-frontend)

---

## 🖥️ EC2 Instance Details

| Property | Value |
|----------|-------|
| **EC2 Name** | Ec2-Mern-APP |
| **Public IP** | 3.239.188.217 |
| **OS** | Ubuntu |

### Security Group — Inbound Rules

| Port | Protocol | Source | Description |
|------|----------|--------|-------------|
| 22 | TCP | 0.0.0.0/0 | SSH Access |
| 3000 | TCP | 0.0.0.0/0 | Frontend Application |
| 3001 | TCP | 0.0.0.0/0 | Backend Application |

---

## ⚙️ Configuring EC2

### Step 1: Update Your EC2 Instance

Connect to your EC2 instance via SSH and run:

```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2: Install Node.js 22 and npm

```bash
# Add NodeSource Repository
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -

# Install Node.js
sudo apt install -y nodejs
```

**Verify installation:**

```bash
node -v
npm -v
```

---

## 🍃 Configure MongoDB Database

### Step 1: Create a Cluster on MongoDB Atlas

1. Sign in at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Click **"Build a Cluster"**
3. Choose **AWS** as the cloud provider and select the nearest region
4. Select the free tier option **(M0)**
5. Click **"Create Cluster"** and wait for provisioning

> **Note:** Skip this step if the cluster is already set up.

### Step 2: Allow Access from Anywhere

**Database Access:**
1. Navigate to **"Database Access"** in the left sidebar
2. Click **"Add New Database User"**
3. Enter a username and password *(alphanumeric only — no special characters)*
4. Under **"Database User Privileges"**, select **"Read and write to any database"**
5. Click **"Add User"**

**Network Access:**
1. Navigate to **"Network Access"** in the left sidebar
2. Click **"Add IP Address"**
3. Select **"Allow Access from Anywhere"** or add your specific IP
4. Confirm and save changes

### Step 3: Create a Database Using MongoDB Compass

1. Download [MongoDB Compass](https://www.mongodb.com/try/download/compass)
2. Follow the installation instructions for your OS
3. Open Compass and enter your connection URI:

```
mongodb+srv://<username>:<password>@cluster0.mongodb.net/travelmemory?retryWrites=true&w=majority
```

4. Replace `<username>` and `<password>` with your credentials
5. Click **"Connect"**
6. Click **"Create Database"** → Name it `travelmemory`
7. Create a collection (e.g., `trips`)

### Step 4: Save Your Cluster Connection URI

Store your MongoDB URI securely for future use:

```
mongodb+srv://travelmemory:<password>@cluster0.hfeojne.mongodb.net/travelmemory?retryWrites=true&w=majority
```

> ⚠️ **Important:** Never commit your MongoDB URI with credentials to GitHub. Always use `.env` files and add them to `.gitignore`.

---

## 🚀 Deploy Node.js Backend

### Step 1: Clone the Repository

```bash
git clone https://github.com/UnpredictablePrashant/TravelMemory.git
```

### Step 2: Navigate to the Backend Folder

```bash
cd TravelMemory/backend
```

### Step 3: Create the .env File

```bash
sudo vi .env
```

Add the following content:

```env
MONGO_URI='mongodb+srv://travelmemory:<password>@cluster0.hfeojne.mongodb.net/travelmemory?retryWrites=true&w=majority'
PORT=3001
```

### Step 4: Install Necessary Packages

```bash
sudo npm install
```

### Step 5: Run the Backend Application

```bash
# Run in background using nohup
nohup node index.js &
```

### Step 6: Test the API Endpoint

Open your browser and navigate to:

```
http://3.239.188.217:3001/hello
```

> ✅ **Expected Output:** `Hello World`

---

## ⚛️ Deploy React Frontend

### Step 1: SSH to Your EC2 Instance

```bash
ssh -i /path/to/your-key.pem ubuntu@3.239.188.217
```

> **Note:** Skip if already connected.

### Step 2: Navigate to the Frontend Directory

```bash
cd TravelMemory/frontend
```

### Step 3: Create the .env File

```bash
echo "REACT_APP_BACKEND_URL=http://3.239.188.217:3001" > .env
```

### Step 4: Install Required Packages

```bash
npm install
```

### Step 5: Run the Application

```bash
npm start
```

### Step 6: Access Your Application

Open your browser and navigate to:

```
http://3.239.188.217:3000
```

> ✅ **Expected Output:** TravelMemory React application loads successfully.

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **MongoDB Atlas** | Cloud Database |
| **Express.js** | Backend Framework |
| **React.js** | Frontend Framework |
| **Node.js** | Runtime Environment |
| **AWS EC2** | Cloud Hosting |
| **MongoDB Compass** | Database GUI |

---

## 📁 Project Structure

```
TravelMemory/
├── backend/
│   ├── index.js
│   ├── package.json
│   └── .env          # (not committed to GitHub)
└── frontend/
    ├── src/
    ├── package.json
    └── .env          # (not committed to GitHub)
```

---

## ⚠️ Important Notes

- Never commit `.env` files to GitHub
- Add `.env` to your `.gitignore` file
- Restrict **Port 22 (SSH)** to your specific IP in production
- Use `nohup` to keep the backend running after closing the SSH session

---

## 👨‍💻 Author

Completed MERN app setup on AWS EC2 — **08 June 2026**
