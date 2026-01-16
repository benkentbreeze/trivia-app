# Trivia App (Node.js + Socket.IO)

Realtime drop-in/drop-out trivia game with a live leaderboard.

## Features
- Express server with Socket.IO websockets
- Players join anytime with a name
- Timed questions on a continuous loop
- Rank-based scoring for correct answers (first 100, second 50, third 25, ...)
- Live leaderboard updates
- Simple, responsive browser UI

## Requirements
- Node.js 18+ recommended

## Install
```bash
npm install
```

## Run
```bash
npm start
```

Then open `http://localhost:3000` in your browser. Open multiple tabs or devices to play together.

## How It Works
- The server cycles through questions from `src/questions.js`.
- Each question lasts 20 seconds.
- Scoring is based on the order of correct submissions:
  - 1st correct: 100 points
  - 2nd correct: 50 points
  - 3rd correct: 25 points
  - Then it continues halving (rounded down) to a minimum of 1 point.
- After a short reveal, the next question starts automatically.
- Disconnecting keeps your score; rejoin with the same name to reclaim it (if not currently in use).

## Project Structure
```
server.js            # Express + Socket.IO server, game loop, scoring, leaderboard
src/questions.js     # Question set
public/              # Browser client (HTML/CSS/JS)
  index.html
  styles.css
  client.js
```

## Customizing
- Questions: Edit `src/questions.js` to add or change questions.
- Durations and points: Tweak constants in `server.js`:
  - `QUESTION_DURATION_MS`
  - `REVEAL_DURATION_MS`
  - Scoring sequence is defined via the `pointsForRank(rank)` function.

## Notes
- This demo uses in-memory state. For persistence across server restarts, add a database or file storage layer.

