# MongoDB Atlas Express API

Small Express API that connects to MongoDB Atlas and provides basic CRUD for a `cards` collection.

Setup
1. Copy `.env.example` to `.env` and fill in `MONGODB_URI` and other values.
2. From the `mongodb_api` folder install dependencies:

```powershell
npm install
```

Run

```powershell
npm start
# or for development with auto-reload
npm run dev
```

Endpoints
- GET /health — health check
- GET /cards?limit=100 — list cards (optional limit)
- GET /cards/:id — get card by ObjectId
- POST /cards — insert a card (JSON body) or array of cards
- DELETE /cards — delete all cards (clear all records)

Additional endpoint:
- GET /cardinfo — filter cards using query parameters similar to the ygoprodeck API. Returns JSON in the shape: { data: [ ... ] }

Examples:

- Get all cards (limit 100 by default):
	- GET /cardinfo
- Get a card by exact name:
	- GET /cardinfo?name=Dark%20Magician
- Fuzzy name search:
	- GET /cardinfo?fname=Magician
- Archetype search:
	- GET /cardinfo?archetype=Blue-Eyes
- Numeric comparisons (atk less than 2500):
	- GET /cardinfo?atk=lt2500

Notes:
- The endpoint implements a subset of parameters: name, fname, id, konami_id, type, atk, def, level, race, attribute, link, linkmarker, scale, cardset, archetype, staple, has_effect, sort, limit.
- linkmarker matching is case-insensitive; multiple markers can be comma-separated and will be matched using $all.

Notes
- The delete-all endpoint performs a deleteMany({}) and will remove all documents from `cards` collection. Use with caution.
