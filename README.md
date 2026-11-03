# React Admin Dashboard

Admin panel UI built with **React + TypeScript**, using **Recharts** for charts and **MUI X Data Grid** for tables. The app currently runs on mock data from `src/data.ts`; API integration (via TanStack Query) is prepared but commented out.

## Tech stack

- [React 18](https://react.dev/) + [TypeScript](https://www.typescriptlang.org/)
- [Vite](https://vitejs.dev/) — dev server and build
- [React Router v6](https://reactrouter.com/) — routing (`createBrowserRouter`)
- [Recharts](https://recharts.org/) — line, area, bar and pie charts
- [MUI X Data Grid](https://mui.com/x/react-data-grid/) — tables with search, export, pagination and row selection
- [TanStack Query v4](https://tanstack.com/query/v4) — data fetching layer (prepared for a REST API)
- [Sass (SCSS)](https://sass-lang.com/) — styles, shared variables and responsive mixins
- ESLint — code linting

## Features

- **Dashboard** (`/`) — grid of widgets:
  - top deals (users list);
  - mini line charts: total users, total products, ratio, revenue — with value and percentage change;
  - pie chart: leads by source;
  - big area chart: revenue analytics;
  - bar charts: total visits and profit earned.
- **Users** (`/users`) and **Products** (`/products`) — Data Grid tables:
  - quick filter (search) with debounce;
  - export (CSV / print) via the toolbar;
  - pagination and checkbox selection;
  - actions column: view details / delete;
  - "Add new" modal with a form generated from the table columns.
- **User / Product details** (`/users/:id`, `/products/:id`) — info card, line chart and latest activities timeline.
- Layout: navbar, sidebar menu, footer.
- Responsive layout (breakpoints in `src/styles/responsive.scss`).
- `/login` — placeholder page.

## Getting started

Requirements: **Node.js 18+** and npm.

```bash
# install dependencies
npm install

# start dev server (http://localhost:5173)
npm run dev
```

## Scripts

| Command           | Description                                 |
| ----------------- | ------------------------------------------- |
| `npm run dev`     | Start Vite dev server with HMR              |
| `npm run build`   | Type-check (`tsc`) and build for production |
| `npm run preview` | Preview the production build locally        |
| `npm run lint`    | Run ESLint on `src`                         |

## Project structure

```
public/                 # icons and images (svg/png)
src/
├── components/
│   ├── add/            # "Add new" modal form
│   ├── barChartBox/    # bar chart widget
│   ├── bigChartBox/    # big area chart widget
│   ├── chartBox/       # mini line chart widget
│   ├── dataTable/      # MUI Data Grid wrapper with actions column
│   ├── footer/
│   ├── menu/           # sidebar navigation
│   ├── navbar/
│   ├── pieCartBox/     # pie chart widget
│   ├── single/         # details view (info + chart + activities)
│   └── topBox/         # top deals list
├── pages/
│   ├── home/           # dashboard
│   ├── login/
│   ├── product/        # single product
│   ├── products/       # products table
│   ├── user/           # single user
│   └── users/          # users table
├── styles/
│   ├── global.scss
│   ├── responsive.scss # breakpoint mixins
│   └── variables.scss  # colors
├── data.ts             # mock data for charts, tables and menu
├── App.tsx             # router and layout
└── main.tsx            # entry point
```

## Connecting a backend API

Pages and components already contain commented-out TanStack Query code (marked `// TEST THE API`) that expects a REST API at `http://localhost:8800/api`:

| Method   | Endpoint                | Used in                      |
| -------- | ----------------------- | ---------------------------- |
| `GET`    | `/api/users`            | `pages/users/Users.tsx`      |
| `GET`    | `/api/products`         | `pages/products/Products.tsx`|
| `POST`   | `/api/{slug}s`          | `components/add/Add.tsx`     |
| `DELETE` | `/api/{slug}/{id}`      | `components/dataTable/DataTable.tsx` |

To switch from mock data to the API, uncomment these blocks and replace the `rows` passed to `DataTable` with the fetched `data`.
