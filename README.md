# TheMovieMatcher

## What is TheMovieMatcher

**TheMovieMatcher** is a Telegram Mini App designed to revolutionize how groups of friends choose movies. Forget endless debates and complicated polls. You get a fun, engaging, and surprisingly accurate way to find the perfect film for your next movie night!

## Features

*   **Tinder-like Swiping:**  Swipe right to vote for a movie, left to vote against. It's that simple!
*   **Dynamic Pair Selection:**  Our intelligent algorithm prioritizes movies with fewer comparisons, close Elo ratings, and those that spark the most debate (controversial picks!).
*   **Elo Rating System:**  A sophisticated Elo-based system ranks movies based on group preferences, ensuring accurate and fair results.
*   **Real-time Results:**  Track your group's preferences as they evolve.
*   **Fuzzy Search:**  Find movies quickly, even with typos, thanks to smart fuzzy search.
*   **Manual Movie Addition:** Add movies not found in the database.
*   **English and Russian Language Support:**  Search and get suggestions in two languages.
*   **Session Persistence:**  Leave and come back without losing your progress.
*   **Anonymous or Open Voting:** Choose to keep votes private or reveal them for added fun.
*   **Built with:** React, Node.js, TypeScript, PostgreSQL, Telegram Mini Apps SDK, TMDb API.


## Why TheMovieMatcher?

*   **No More Decision Paralysis:**  Quickly narrow down choices and find a movie everyone will enjoy.
*   **Fun and Engaging:** The swiping interface makes the selection process interactive and fun.
*   **Fair and Accurate:** The Elo rating system ensures that the final ranking reflects the group's collective preferences.
*   **Great for Telegram Groups:**  Seamlessly integrates into your existing Telegram chats.

## How it Works (Technical Overview)

1. **Movie Search:** Users search for movies using the TMDb API (proxied through the backend). Fuzzy matching and language-aware suggestions enhance the search experience.
2. **Movie Suggestion:** Users can add movies to a group's list, either from search results or manually.
3. **Voting:** The mini-app presents users with pairs of movies. The dynamic pair selection algorithm prioritizes:
    *   Movies with fewer comparisons.
    *   Movies with similar Elo ratings.
    *   "Controversial" movies (those with high vote variance).
4. **Elo Rating Calculation:** After each vote (or in batches for larger groups), Elo ratings are updated using a dynamic K-factor that adjusts based on the number of comparisons a movie has.
5. **Results:** The app displays individual and group results, including the winning movie, overall ranking, and the most "controversial" picks.

## Getting Started

### Prerequisites

*   Node.js (v18 or higher recommended)
*   pnpm (or npm/yarn)
*   PostgreSQL (or another database of your choice)
*   Telegram Bot Token (from BotFather)
*   TMDb API Key

### Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/octrow/TheMovieMatcher.git
    cd TheMovieMatcher
    ```

2. Install frontend dependencies:

    ```bash
    cd frontend && pnpm install
    ```

3. Install backend dependencies:

    ```bash
    cd ../backend && pnpm install
    ```

4. Set up the environment variables:

    *   Create a `.env` file in the `backend` directory.
    *   Add the following variables (replace with your actual values):

    ```
    DATABASE_URL=postgres://user:password@host:port/database
    BOT_TOKEN=YOUR_TELEGRAM_BOT_TOKEN
    TMDB_API_KEY=YOUR_TMDB_API_KEY
    PORT=5000
    ```

5. Set up the database:

    *   Create the database and tables using the provided SQL schema (you might need to adjust this based on your database):
    ```sql
    -- In the 'backend/prisma' directory, you might have a 'schema.prisma' file
    -- Use Prisma to create the database tables:
    npx prisma migrate dev --name init

    -- Or, if you prefer raw SQL, create a file named 'schema.sql' with content like this:

    CREATE TABLE "Users" (
        "userId" TEXT PRIMARY KEY,
        "username" TEXT,
        "currentMovieSuggestions" TEXT[],
        "votingProgress" JSONB
    );

    CREATE TABLE "Groups" (
        "groupId" TEXT PRIMARY KEY,
        "movieSuggestions" TEXT[],
        "votingData" JSONB,
        "status" TEXT,
        "settings" JSONB,
        "eloRatings" JSONB
    );

    CREATE TABLE "Movies" (
        "movieId" TEXT PRIMARY KEY,
        "title" TEXT,
        "year" INTEGER,
        "poster" TEXT,
        "description" TEXT,
        "tmdbRating" REAL,
        "tmdbPopularity" REAL,
        "voteCount" INTEGER,
        "controversyScore" REAL
    );
    ```

6. Run the backend:
    ```bash
    pnpm run start:server
    ```

7. Run the frontend:
    ```bash
    pnpm run start:client
    ```

### To run application on your local computer with HTTPS:

1. Create a `.env` file in `frontend` directory.

2. Set `HTTPS` variable to `true` and `PORT` to `443`.

3. Run this command in project's `frontend` directory:
```bash
mkcert -install && mkcert localhost
```
4. Run this command in project's `frontend` directory:
```bash
pnpm run start
```

This will create local CA and generate SSL certificate for `localhost`.

8. Access the mini-app in your Telegram client by opening the bot you created and attaching the mini-app using the URL provided by the development server (e.g., `https://your-ngrok-url.ngrok.io`).

## Contributing

We welcome contributions! Please open an issue or a pull request!


## Acknowledgements

*   [Telegram Mini Apps SDK](https://docs.telegram-mini-apps.com/)