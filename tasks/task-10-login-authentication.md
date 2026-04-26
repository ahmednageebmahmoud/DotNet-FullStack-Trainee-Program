# Task 10 — Login Page & Auth State

---

## Task Information

| Field | Details |
|---|---|
| **Level** | 🟢 Beginner to Intermediate |
| **Estimated Duration** | 2 Days |
| **Type** | Frontend Only |
| **Depends On** | Backend Task 07 — Login with JWT |
| **Deliverable** | Login page + shared auth state |

---

## Goal

Build the Angular login experience on top of the completed backend. Authenticate against the API, store the session on the client, and expose the current user state across the app.

---

## Required Technologies

### Frontend — Angular
| Technology | Description |
|---|---|
| **Angular 17+** | Main frontend framework |
| **Reactive Forms** | Build and validate the login form |
| **Angular Router** | Move between login and protected pages |
| **Auth Service** | Manage login, logout, and current user state |
| **BehaviorSubject / Signal** | Track the current user reactively |
| **localStorage / sessionStorage** | Persist the session on refresh |
| **SCSS** | Global styling format for the Angular project |
| **Tailwind CSS** | Style the page |

---

## Project Setup

Use this task as the starting point for the frontend project.

### Create the Angular Project

1. Install Node.js LTS if it is not already installed.
2. Install Angular CLI:

```bash
npm install -g @angular/cli
```

3. Create a new Angular project:

```bash
ng new frontend --routing --style scss
cd frontend
```

4. Start the development server to confirm the app works:

```bash
ng serve -o
```

### Install Tailwind CSS

1. Follow the official Tailwind installation guide for Angular.
2. Install Tailwind in the Angular project.
3. Add Tailwind to the global styles configuration in `src/styles.scss`.
4. Confirm Tailwind works by applying a few utility classes to the login page.

### Suggested Setup Notes

- Keep the frontend in its own Angular project folder.
- Enable routing when creating the project because later tasks need route guards and protected pages.
- Use SCSS as the Angular style format from the start so later components stay consistent.
- Keep the environment file ready for the API base URL.
- Finish the basic project setup before starting the login page implementation.

---

## API Dependencies

- `POST /api/auth/login`

---

## Deliverables

- [ ] Create a `login` page with email and password fields
- [ ] Create `AuthService` with `login()`, `logout()`, `isLoggedIn()`, `getCurrentUser()`, and `getToken()`
- [ ] Persist the login response in `localStorage` or `sessionStorage`
- [ ] Restore the current user from storage on app refresh
- [ ] Redirect authenticated users away from `/login`
- [ ] Add a logout action that clears the stored session
- [ ] Create a basic auth guard that blocks anonymous users from protected routes

---

## Data Models

### Login Request Fields

`email` and `password`.

### Login Response Fields

`id`, `fullName`, `email`, `role`, `claims`, `token`, and `expiresAt`.

---

## Validation Requirements

| Field or Case | Rule |
|---|---|
| **Email** | Required, valid email |
| **Password** | Required, min 8 |
| Wrong credentials | Show one general error message |
| Submit while loading | Disable the submit button |
| Existing session | Redirect away from `/login` |

---

## Tips

### Angular
1. Keep token storage and current-user parsing in one service.
2. Restore the session when the app starts so refresh does not log the user out immediately.
3. Keep this task focused on authentication state; permission-based UI comes later in Task 17.

---

## Helper URLs

- Tailwind UI Blocks: https://tailwindcss.com/plus/ui-blocks
- Tailwind Grid Template Columns: https://tailwindcss.com/docs/grid-template-columns
- Tailwind Sign In Forms: https://tailwindcss.com/plus/ui-blocks/application-ui/forms/sign-in-forms