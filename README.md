# FreeLanceHub — Frontend

React frontend for the **FreeLanceHub** marketplace platform.
Built by **Shivam** as Phase 4B of the SDLC (Frontend UI).

---

## Tech Stack
- **React 18** with React Router v6
- **CSS Modules** (scoped styles — no leakage when embedded)
- Inter font via Google Fonts

---

## Project Structure

```
src/
  App.js                     # All routes
  index.js / index.css       # Entry + global design tokens
  data/
    mockData.js              # All mock data — swap each export for a real API call
  components/
    Avatar / Badge / StatCard / RatingBar
    TalentCard / ProductCard / Pagination
    Navbar / Footer
    DashboardTopbar / DashboardSidebar
    layout/
      PublicLayout            # Header + main + footer
      DashboardLayout         # Topbar + sidebar + main + footer
  pages/
    FindTalent/               # Screen 01 — talent listing + filters
    ConsultantProfile/        # Screen 02 — freelancer profile
    GigDetail/                # Screen 03 — single gig page
    PostGig/                  # Screen 04 — 4-step gig creation
    SellerDashboard/          # Screen 05 — overview + active orders
    Messages/                 # Screen 06 — inbox + chat thread
    Products/                 # Screen 07 — digital products grid
    Checkout/                 # Screen 08 — payment form
    OrderTracking/            # Screen 09 — order timeline
    Notifications/            # Screen 10 — notification feed
    Earnings/                 # Screen 11 — bar chart + payout table
    Signup/                   # Screen 12 — onboarding
    Settings/                 # Screen 13 — profile settings
    Contact/                  # Screen 15 — contact / support
    Login/                    # Login page
```

---

## Getting Started

```bash
npm install
npm start        # → http://localhost:3000
```

---

## Connecting to the Backend (Ketan's APIs)

All mock data lives in `src/data/mockData.js`.
Each named export maps 1-to-1 to an API endpoint.

| Export | Endpoint |
|---|---|
| `talents` | `GET /api/talents` |
| `talentProfile` | `GET /api/talents/:id` |
| `gig` | `GET /api/gigs/:id` |
| `products` | `GET /api/products` |
| `order` | `GET /api/orders/:id` |
| `activeOrders` | `GET /api/orders?status=active` |
| `dashboardStats` | `GET /api/dashboard/stats` |
| `conversations` | `GET /api/messages/conversations` |
| `notifications` | `GET /api/notifications` |
| `earnings` | `GET /api/earnings` |
| `settingsProfile` | `GET /api/profile` |

### Example swap (FindTalent.jsx):

```js
// Before (mock)
import { talents } from "../../data/mockData";

// After (real API)
const [talents, setTalents] = useState([]);
useEffect(() => {
  fetch("/api/talents")
    .then((r) => r.json())
    .then(setTalents);
}, []);
```

---

## Design Tokens (CSS Variables)

Defined in `src/index.css`:

| Token | Value | Usage |
|---|---|---|
| `--orange` | `#e2581e` | CTAs, active states, prices |
| `--navy` | `#16263a` | Top bar, dark badges, footer |
| `--bg` | `#ffffff` | Page background |
| `--border` | `#e5e7eb` | Card borders, dividers |

---

## Notes

- **CSS Modules** used throughout — safe to embed as a `<script>` widget (Phase 5B)
- `useParams()` is already wired on profile/gig/order pages — just replace the mock constant with a real fetch
- No auth guard added yet — add a `ProtectedRoute` wrapper around dashboard routes once Yash's LinkedIn OAuth is live
