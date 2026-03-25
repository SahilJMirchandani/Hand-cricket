Here is the full README content:

🏏 Hand Cricket Online
Real-Time Multiplayer Web Game — FSWD Mini Project
4th Semester | Computer Engineering | VESIT Mumbai | 2025–26

📌 Project Overview
Hand Cricket Online is a real-time multiplayer web game built as a Full Stack Web Development (FSWD) Mini Project. Players choose numbers 0–6 each turn — if both pick the same number, the batsman is OUT; otherwise the batsman scores the runs they chose.

🛠️ Tech Stack
LayerTechnologyFrontendReact.js 18, React Router v6, CSS3BackendNode.js, Express.jsReal-timeSocket.IO (WebSockets)DatabaseMongoDB with Mongoose ODMAuthJWT (JSON Web Tokens) + bcryptjs

📁 Project Structure
hand-cricket-online/
├── server/
│   ├── index.js                  ← Express + Socket.IO server entry
│   ├── models/
│   │   ├── User.js               ← User schema with stats
│   │   └── Match.js              ← Match schema with innings
│   ├── routes/
│   │   ├── auth.js               ← /api/auth (register, login, me)
│   │   └── matches.js            ← /api/matches (history, detail)
│   ├── middleware/
│   │   └── auth.js               ← JWT protect middleware
│   └── socket/
│       └── gameSocket.js         ← All Socket.IO game logic
│
├── client/
│   ├── public/
│   │   └── index.html
│   └── src/
│       ├── App.js                ← Routes + PrivateRoute guard
│       ├── index.js              ← React entry point
│       ├── index.css             ← Global cricket-theme styles
│       ├── context/
│       │   ├── AuthContext.js    ← Auth state + JWT storage
│       │   └── SocketContext.js  ← Socket.IO connection manager
│       ├── components/
│       │   ├── Navbar.js         ← Top navigation bar
│       │   ├── Scoreboard.js     ← Live score display
│       │   ├── TimerRing.js      ← SVG countdown timer
│       │   └── NumPad.js         ← 0-6 number selection pad
│       └── pages/
│           ├── LoginPage.js      ← Login / Sign Up
│           ├── Dashboard.js      ← Main menu + stats
│           ├── CreateRoom.js     ← Host a room + room code
│           ├── JoinRoom.js       ← Join with room code
│           ├── GamePage.js       ← Live gameplay screen
│           ├── ResultPage.js     ← Winner + match summary
│           └── HistoryPage.js    ← Match history + detail
│
├── vercel.json                   ← Vercel deployment config
├── .env.example                  ← Environment variable template
├── package.json                  ← Root (server) dependencies
└── README.md

🚀 Getting Started (Run Locally)
Prerequisites

Node.js v18+ and npm
MongoDB running locally (mongod) or a free MongoDB Atlas URI

1. Extract and enter the project
bashcd hand-cricket-online
2. Set up environment variables
bashcp .env.example .env
# Open .env and fill in your MONGO_URI and JWT_SECRET
3. Install all dependencies
bashnpm run install:all
4. Run both server + client together
bashnpm run dev:all
Or run them separately in two terminals:
bash# Terminal 1 – backend (port 5000)
npm run dev

# Terminal 2 – frontend (port 3000)
cd client && npm start
Open http://localhost:3000 in your browser.

☁️ Deploy to Vercel (Free, Shareable Link)
Step 1 — Free MongoDB (2 min)

Go to mongodb.com/atlas → create a free account
Create a free M0 cluster → click Connect → copy the connection string
Replace <username> and <password> in the string

Step 2 — Push to GitHub
bashgit init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/hand-cricket-online.git
git push -u origin main
Step 3 — Deploy on Vercel

Go to vercel.com → sign in with GitHub
Click New Project → import your repository
Add these Environment Variables:

KeyValueMONGO_URIYour MongoDB Atlas connection stringJWT_SECRETAny long random string e.g. hc_secret_2026_vesitNODE_ENVproductionCLIENT_URLYour Vercel URL e.g. https://hand-cricket.vercel.app

Click Deploy → get your live link like hand-cricket-online.vercel.app
Share that link with anyone — they can sign up and play instantly!

🎮 How to Play
Multiplayer (2 players)

Player A → Dashboard → Create Room → share the 6-character code
Player B → Dashboard → Join Room → enter the code
Game starts automatically when both players are in the room

vs Computer (1 player)

Dashboard → vs Computer — starts instantly, no room code needed

Gameplay Rules

2 innings, 6 balls each
Each turn: both players secretly pick a number from 0 to 6
Numbers are revealed simultaneously
Same number = OUT (wicket falls, innings ends)
Different numbers = batsman scores their own picked number
After inning 1: batting and bowling roles swap, inning 2 has a target to chase
Player with the highest total score after 2 innings wins


🔌 Socket.IO Events Reference
EventDirectionDescriptioncreate_roomClient → ServerHost creates a new roomroom_createdServer → ClientReturns generated room codejoin_roomClient → ServerGuest joins with a codestart_vs_computerClient → ServerStart single-player vs AIgame_startServer → ClientMatch begins, sends initial stateplayer_pickClient → ServerPlayer submits their numberpick_registeredServer → ClientConfirms pick was receivedturn_startServer → ClientNew turn begins, timer resetstimer_tickServer → ClientCountdown tick every 1 secondturn_resultServer → ClientBoth picks revealed + outcomeinning_changeServer → ClientInning 1 ends, inning 2 startsgame_overServer → ClientMatch complete, sends resultopponent_disconnectedServer → ClientOther player left the match

📡 REST API Endpoints
MethodEndpointAuthDescriptionPOST/api/auth/registerNoRegister new userPOST/api/auth/loginNoLogin, returns JWT tokenGET/api/auth/meYesGet current user + statsGET/api/matches/historyYesGet last 20 matchesGET/api/matches/:idYesGet single match detailGET/api/healthNoServer health check

📄 License
This project is developed for academic purposes at VESIT. All rights reserved.
