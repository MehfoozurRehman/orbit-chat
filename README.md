# orbit-chat

A React and Vite front end for a three-column messaging app: a login screen and a chat room layout, with the routing and build setup behind them. The UI is in place. Messaging itself is not wired up yet.

## The problem

A chat product has to lay out contacts, a conversation and some kind of activity feed on one screen, and it has to make those panels behave well at different sizes. This repo covers that front-end layer on its own, so the layout, routing and styling can be worked on before any backend exists.

## What it does

- **Login screen**: An email and password form. Submitting it navigates to the chat room. It does not check credentials yet.
- **Three-column chat room**: A recent-messages list on the left, a conversation pane in the middle, and an activity column on the right with a stories section. The list and story entries are static placeholders.
- **Convention-based routing**: `src/router` builds routes from files in `src/screens` using `import.meta.glob`. Filename suffixes choose lazy-loaded (`.lazy`) and protected (`.protected`) routes.
- **Protected layout**: `src/layouts/protected.jsx` renders its child routes only when a user is set, and redirects to `/` otherwise. The user value is currently hard-coded to `null`.
- **Per-page metadata**: The router sets page titles and meta tags with `react-helmet`, using defaults from `src/layouts/app.jsx`.

## How it's built

- **Stack**: React 18, React Router 6.8, Vite 4, TypeScript mixed with JSX, SCSS, and Feather icons from `react-feather`.
- **Build**: Vite with chunk splitting, Brotli compression, image minification, and a webfont download plugin.
- **Decision: file-based routes.** Adding a screen means adding a file under `src/screens`, and the filename is the route. There is no central route table, which keeps screens easy to add and makes the naming convention the contract.
- **Layout**: The app lives in `client/`. The repo root only holds the README, the license and an editor config.

## Running it locally

Requires Node.js 18 or later.

```bash
cd client
npm install
npm run dev        # Vite dev server at http://localhost:5173
```

Other scripts in `client/package.json`:

- `npm run build` for a production build.
- `npm run preview` to serve the production build locally.
- `npm run formate` to format the code with Prettier.

## What I learned and what I'd do next

- **No backend yet.** There is no authentication, no message storage and no real-time transport. Adding a WebSocket or similar channel is the main missing piece.
- **Placeholder content.** The chat list and conversation panes render repeated placeholder components. These should be driven by data.
- **The protected layout has no source of truth.** Until a real session exists, the redirect always applies.
- **A dead script.** `npm start` points at `build/server.js`, which is not in the repo.
- **Mixed file types.** Screens and layouts are `.jsx` while the entry point and router are `.tsx`. Picking one, or converting gradually, would make the codebase easier to follow.
- **No tests.** Component tests for the login form and the routing conventions would be a good start.

## Author

Created by [Mehfooz-ur-Rehman](https://github.com/MehfoozurRehman).
