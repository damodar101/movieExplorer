**Movie Explorer**

A small static web project that fetches movie data from an API and displays results in a card-style layout with a search bar. The app is implemented with plain HTML/CSS/JS and lives in the project root (`index.html`) and the `assests/` folder for styles and scripts.

**Features**
- **Card Layout**: Movies are shown as responsive cards (poster, title, year, short overview).
- **Search**: Live search field to query the API or filter the currently loaded list.
- **API-backed**: Fetches data from an external movie API (e.g., OMDb). API key integration is described below.
- **Minimal Dependencies**: Plain JS/CSS — no build step required.

**Files**
- **`index.html`**: Main page — markup and search input.
- **`assests/css/app.css`**: Styles for the card layout, grid, and responsive behavior.
- **`assests/js/app.js`**: JavaScript that queries the API, renders movie cards, and wires the search UI.
- **`assests/images/`**: Static images (if any).

**Getting Started**

- **Prerequisites**: A modern browser. For local development you can serve files with a simple HTTP server (recommended to avoid CORS issues when fetching remote APIs).

- **Run a quick local server (PowerShell)**:

```powershell
# Python 3 built-in server
python -m http.server 8000

# OR using Node (if you have `http-server` installed)
npx http-server -p 8000

# Then open:
Start-Process http://localhost:8000
```

**API configuration**

This project expects to call a public movie API. Two common choices are:

- OMDb (http://www.omdbapi.com/) — needs an API key (free for limited usage).
- The Movie Database (TMDb, https://developers.themoviedb.org/) — needs an API key.

You can wire the API key into the app in one of two simple ways:

- Edit `assests/js/app.js` and set a constant (quick & dirty):

```js
// at top of assests/js/app.js
const API_KEY = '49da69f5';
```

- Or add a small `config.js` next to `index.html` and include it before `app.js`:

```js
// config.js
window.MOVIE_EXPLORER_CONFIG = { apiKey: 'YOUR_API_KEY_HERE' };
```

Then inside `app.js` use `window.MOVIE_EXPLORER_CONFIG.apiKey`.

Security note: This project is a static front-end. Embedding API keys in client-side code is convenient for demos but not secure for production — consider using a backend proxy for private keys.

**How the search works**

- The search box in `index.html` calls an API search endpoint (or filters the already loaded dataset).
- The UI performs debounced queries to avoid spamming the API and updates the card grid with results.

**Customizing**

- To change the card layout, edit `assests/css/app.css`.
- To change the API or modify the request parameters, edit `assests/js/app.js`.

**Troubleshooting**

- If movie posters or API responses fail to load, check your browser console for CORS errors or network errors.
- If you get an HTTP 401/403 from the API, verify your API key and usage limits.

**Next steps / Enhancements**

- Add pagination or infinite scroll for larger result sets.
- Add a detail modal or separate detail page for each movie.
- Persist favorites to `localStorage`.
- Move API calls to a lightweight backend (for secure API key handling).



