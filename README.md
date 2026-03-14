# distributeEase — Frontend

A React + Vite single-page application for managing distribution operations. Built with a dark theme UI and role-based navigation.

---

## Tech Stack

| Technology | Purpose |
|---|---|
| React 19 | UI framework |
| Vite 7 | Build tool |
| Axios | HTTP client |
| CSS Variables | Theming |

---

## Project Structure

```
frontend/distribteEase/
├── src/
│   └── App.jsx          # Entire app — components, styles, routing
├── public/
├── .env                 # Environment variables (not in git)
├── .env.example         # Example env file
├── index.html
├── vite.config.js
└── package.json
```

---

## Setup — Local Development

### 1. Clone and navigate
```bash
git clone https://github.com/yourname/Distri-Ease.git
cd frontend/distribteEase
```

### 2. Install dependencies
```bash
npm install
```

### 3. Create `.env` file
```env
VITE_API_URL=http://localhost:8000
```

### 4. Run dev server
```bash
npm run dev
```

App runs at: `http://localhost:5173`

> Make sure backend is running at `http://localhost:8000`

---

## Environment Variables

| Variable | Description |
|---|---|
| `VITE_API_URL` | Backend API base URL |

For production set this to your Render backend URL:
```env
VITE_API_URL=https://distributeease-backend-1.onrender.com
```

---

## Features

### Authentication
- JWT login with role detection
- Auto redirect based on role
- Styled sign out confirmation modal

### Dashboard
- Today's orders count
- Active shops count
- Revenue today
- Pending packing count
- Recent orders table
- 7-day revenue bar chart

### Orders
- Place new order with searchable shop + product dropdowns
- Add new shop/product inline from order modal
- Edit existing orders
- Delete orders
- View all orders per shop (click shop name)
- Orders sorted newest first
- Telegram notification on order placed

### Shops
- Add, edit, delete shops
- View shop details + full order history (click shop name on mobile)
- Place order directly from shop list
- Edit orders from shop detail view
- Mobile: phone/address hidden in table, shown under shop name

### Products
- Add, edit, delete products
- Stock management

### Summary
- Daily packing summary by date
- Telegram notification on fetch

### Users (Admin only)
- Add new users with role assignment
- Delete users
- Cannot delete own account

---

## Components

| Component | Description |
|---|---|
| `SearchSelect` | Searchable dropdown with add-new option |
| `ProductRows` | Dynamic product + quantity rows |
| `ConfirmModal` | Styled confirmation dialog (replaces browser alert) |
| `Modal` | Reusable modal with header/footer |
| `Card` | Content card wrapper |
| `Btn` | Button with variants (primary, danger, small) |
| `Field` | Labeled input field |
| `Badge` | Status badge |
| `Spin` | Loading spinner |
| `ErrMsg` | Error message display |
| `Toast` | Auto-dismiss notification |

---

## Roles & Navigation

| Role | Pages |
|---|---|
| `admin` | Dashboard, Orders, Shops, Products, Summary, Users |
| `salesman` | Dashboard, Orders, Shops, Summary |
| `packing_team` | Dashboard, Summary |

---

## Build for Production

```bash
npm run build
```

Output goes to `dist/` folder.

---

## Deployment (Vercel)

1. Push to GitHub
2. Go to vercel.com → New Project → Import repo
3. Set Root Directory: `frontend/distribteEase`
4. Framework: **Vite** (auto detected)
5. Add environment variable:
   ```
   VITE_API_URL = https://distributeease-backend-1.onrender.com
   ```
6. Click Deploy

Auto-deploys on every `git push`. ✅

---

## API Integration

All API calls go through a single axios instance:

```javascript
const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL || "http://localhost:8000"
});

// JWT token auto-attached
api.interceptors.request.use(cfg => {
  const token = localStorage.getItem("de_token");
  if(token) cfg.headers.Authorization = `Bearer ${token}`;
  return cfg;
});
```

---

## Local Storage

| Key | Value |
|---|---|
| `de_token` | JWT access token |
| `de_user` | `{ name, role }` JSON string |

---

## CSS Theme Variables

```css
--bg        /* page background */
--s1        /* surface 1 — cards */
--s2        /* surface 2 — inputs */
--border    /* border color */
--text      /* primary text */
--muted     /* secondary text */
--accent    /* green #00e5a0 */
--a2        /* accent variant */
--a3        /* red for danger */
--font      /* body font */
--display   /* heading font */
```

---

## Scripts

```bash
npm run dev      # start dev server
npm run build    # production build
npm run preview  # preview production build
npm run lint     # run eslint
```
