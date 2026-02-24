# Undead Literature Networks

> A password-protected web platform for network-based distant reading of vampiric and revenant figures across transnational literary traditions — from Romanian *strigoi* to the Gothic canon.

**Founded by** Anca-Simina Martin & Andrei-Nicolae Martin-Căluțiu · Sibiu, Romania

---

## Overview

This repository powers a private research portal for the *Undead Literature Networks* project. It hosts interactive character network visualisations built on top of structured literary data, allowing researchers to explore relationships, communities, and narrative patterns across texts in the vampire/revenant tradition.

The first published analysis is an interactive character network for **Vampirul** (Al. Biciurescu & G.M. Vlădescu), mapping direct dialogue and co-presence relationships across all characters in the novel.

---

## Features

* 🔐 **Password-protected access** — session-based authentication, no public exposure of research data
* 🕸️ **Interactive D3.js network graph** — force-directed layout with zoom, pan, and drag
* 🎛️ **Dynamic filters** — filter by dialogue count, relationship weight, and relationship type (direct vs. co-presence)
* 👥 **Character drawer** — click any node to inspect connections, community membership, sentiment data, and vampire identity tabs
* 🧛 **Vampire identity merge** — toggle to collapse all avatar identities of the vampire into a single merged node
* 📤 **Export** — download the network as SVG or PNG
* 🏠 **Home portal** — a landing page listing all available analyses with status indicators

---

## Project Structure

```
.
├── api/
│   └── index.js                          # Express app — routes & auth middleware
├── private/                              # Protected files (never served without auth)
│   ├── home.html                         # Portal landing page
│   ├── vampirul-character-network.html   # Vampirul network visualisation
│   └── network_data.json                 # Graph data (nodes, edges, metadata)
├── public/                               # Publicly served static files
│   ├── login.html                        # Login page
│   └── favicon.png                       # Site favicon
├── server.js                             # Entry point — starts the HTTP server
├── package.json
└── .env                                  # Environment variables (never commit this)
```

---

## Getting Started

### Prerequisites

* [Node.js](https://nodejs.org/) v18 or higher
* npm

### Installation

```bash
git clone https://github.com/andreimartincalutiu/vampirul-network-analysis.git
cd vampirul-network-analysis
npm install
```

### Configuration

Create a `.env` file in the project root (see `.env.example`):

```env
APP_USER=your_username
APP_PASS=your_password
SESSION_SECRET=a_long_random_secret_string
NODE_ENV=development
PORT=3000
```

> ⚠️ Never commit `.env` to version control. Make sure it's in your `.gitignore`.

### Running locally

```bash
npm start
```

Then open [http://localhost:3000](http://localhost:3000/) in your browser. You will be redirected to the login page.

---

## Routes

| Method   | Path                                              | Auth required | Description                           |
| -------- | ------------------------------------------------- | :-----------: | ------------------------------------- |
| `GET`  | `/login`                                        |      No      | Login page                            |
| `POST` | `/login`                                        |      No      | Authenticate and create session       |
| `POST` | `/logout`                                       |      Yes      | Destroy session and redirect to login |
| `GET`  | `/home`                                         |      Yes      | Portal landing page                   |
| `GET`  | `/vampirul-character-network`                   |      Yes      | Interactive Vampirul network          |
| `GET`  | `/vampirul-character-network/network_data.json` |      Yes      | Graph data for Vampirul network       |

---

## Deployment

The app is structured to deploy on [Vercel](https://vercel.com/) with a `vercel.json` configuration (or similar Node-compatible platforms like Railway or Render).

Set the environment variables (`APP_USER`, `APP_PASS`, `SESSION_SECRET`, `NODE_ENV=production`) in your platform's dashboard.

When `NODE_ENV=production`, session cookies are automatically set to `secure: true` (HTTPS only).

---

## Data Format

`network_data.json` follows this structure:

```json
{
  "metadata": {
    "title": "...",
    "total_nodes": 42,
    "total_edges": 130,
    "total_communities": 6
  },
  "nodes": [
    {
      "id": "character_id",
      "label": "Character Name",
      "dialogue_count": 38,
      "community": 1,
      "gender": "M",
      "is_vampire_avatar": false
    }
  ],
  "edges": [
    {
      "source": "character_a",
      "target": "character_b",
      "weight": 12,
      "direct": 8,
      "copresence": 4
    }
  ]
}
```

---

## Planned Analyses

| Analysis                                                        | Status         |
| --------------------------------------------------------------- | -------------- |
| Vampirul — Character Network (Al. Biciurescu & G.M. Vlădescu) | ✅ Live        |
| Narrative Space Mapping                                         | 🔄 In progress |
| Transnational Comparisons                                       | 📋 Planned     |

---

## Security Notes

* Credentials are stored as environment variables and compared server-side.
* All private files (HTML, JSON data) are gated behind `requireAuth` middleware.
* Session cookies use `httpOnly`, `sameSite: lax`, and `secure` (in production).
* Sessions expire after 8 hours.

---

## License

This project is licensed under the [GNU General Public License v3.0](https://claude.ai/chat/LICENSE).

---

## Contact

For access requests or research inquiries: [andreinicolae@tuta.io](mailto:andreinicolae@tuta.io)
