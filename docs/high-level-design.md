# Igniflo – Order Management System (OMS)

## 📐 Architecture Overview

The system is divided into two main layers:


- **Frontend (React + MUI)**: Handles user interface for both admin and customer roles.
- **Backend (Express.js)**: Provides RESTful API endpoints and WebSocket event broadcasting.
- **Database (MongoDB)**: Stores orders, products, and customers.

---

## 🔁 Request-Response Flow

**Placing an order:**
1. Customer fills form on frontend.
2. React sends POST to `/api/orders`.
3. Express checks stock & creates order.
4. Inventory is locked, order saved in MongoDB.
5. WebSocket emits `order-updated` to all connected clients.

**Updating status:**
1. Admin changes status in UI.
2. React PATCHes to `/api/orders/:id/status`.
3. Express updates MongoDB & emits `order-updated`.

---

## 🧩 Component Breakdown

### Client Pages

| Page        | Description                          |
|-------------|--------------------------------------|
| `/`         | Customer order tracker               |
| `/admin`    | Admin dashboard to manage orders     |

### Shared Components

- `OrderStatusBadge.js`: Reusable status chip.

### State Management

- Simple useState/useEffect + Socket.io

---

## 🚦 API Layers

- **Routes** → `/routes/*.routes.js`
- **Controllers** → `/controllers/*.controller.js`
- **Services** → `/services/order.service.js`
- **DB Layer** → `/models/*.model.js`

---

## 🗃️ Database Schema (ERD)


---

## 🔌 API Contract

| Endpoint                  | Method | Description               | Body / Params                         |
|---------------------------|--------|---------------------------|----------------------------------------|
| `/api/customers`          | POST   | Create customer           | `{ name, email, phone }`              |
| `/api/customers`          | GET    | List customers            | –                                      |
| `/api/products`           | POST   | Create product            | `{ name, sku, stock, price }`         |
| `/api/products`           | GET    | List products             | –                                      |
| `/api/orders`             | POST   | Create order              | `{ customer, items, paymentReceived }`|
| `/api/orders`             | GET    | List all orders           | –                                      |
| `/api/orders/:id/status` | PATCH  | Update order status       | `{ status }`                           |

---

## 🔄 Sequence Diagram – Place Order


---

## 🌐 Deployment Topology

- **Client**: React app hosted on Vercel/Netlify
- **Server**: Express API on Render/Railway
- **MongoDB**: MongoDB Atlas (or Render MongoDB)
- **WebSocket**: Built-in via `socket.io` on Express
- **Env Variables**: Managed via `.env` or deploy dashboard

---

## 🔒 Security & Observability

| Concern         | Solution                             |
|----------------|--------------------------------------|
| Auth            | *(Optional enhancement)*             |
| Access Control  | Client separates Admin vs Customer   |
| Rate Limiting   | *(To be added: express-rate-limit)*  |
| Logging         | `morgan` logs all requests           |
| Health Check    | Add `/healthz` route                 |

---

## 📤 Deployment Steps

- Use **Render** for backend (Express)
- Use **Vercel** for frontend (React)
- MongoDB hosted on **MongoDB Atlas**
- CI/CD via **GitHub Actions**

---

## ✅ Done

