# CodePlay — AI-Powered Gamified Programming Learning Platform

A responsive PHP + MySQL learning platform based on the supplied SE-331 project proposal. It includes student registration/login, dashboard, HTML/CSS/JavaScript beginner games, deterministic server-side scoring, progress records, points/levels, contextual AI hints, and fixed fallback hints.

## Requirements
- XAMPP (Apache, PHP 8+, MySQL)
- PHP PDO MySQL extension enabled
- cURL extension (only needed for live AI API requests)

## Run locally with XAMPP
1. Extract the `codeplay` folder into `C:\xampp\htdocs\`.
2. Start **Apache** and **MySQL** in the XAMPP Control Panel.
3. Open `http://localhost/phpmyadmin`.
4. Import `database/codeplay.sql` (it creates the `codeplay` database and tables).
5. Check `config/db.php`. Default XAMPP credentials are `root` with an empty password.
6. Open `http://localhost/codeplay/` in your browser.
7. Create an account and start playing.

## Enable the AI Tutor (optional)
The games work without an AI API. When no key is configured, the tutor returns topic-specific fixed hints. To enable an OpenAI-compatible Chat Completions API, set these environment variables in the PHP/Apache environment:
- `OPENAI_API_KEY` — secret API key (server-side only)
- `OPENAI_API_URL` — optional; defaults to `https://api.openai.com/v1/chat/completions`
- `OPENAI_MODEL` — optional; defaults to `gpt-4o-mini`

Restart Apache after changing environment variables. Never put API keys in JavaScript or commit them to source control. The AI tutor only generates learning guidance; challenge scoring remains deterministic in PHP.

## Main structure
- `index.php` — landing page
- `auth/` — registration, login, logout
- `dashboard.php` — points, level, progress, recent activity
- `games/` — HTML Puzzle, CSS Designer, JavaScript Quest
- `api/submit.php` — server-side challenge validation and scoring
- `api/tutor.php` — AI tutor integration with fixed-hint fallback
- `config/db.php` — database connection
- `database/codeplay.sql` — MySQL schema
- `assets/` — styles and browser scripts

## Notes
- Passwords use PHP `password_hash()` / `password_verify()`.
- Sessions are used for authentication; form/API requests use a CSRF token.
- Points are awarded only after server-side answer validation and only once per passed challenge.
- This is an academic beginner-learning prototype, not a full IDE or compiler. AI responses may be inaccurate and should be treated as assistance.
