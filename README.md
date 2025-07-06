
# 🧪 Supabase Auth + Next.js Starter (Tailwind v4 Custom)
This project is based on the official [`with-supabase`](https://github.com/vercel/next.js/tree/canary/examples/with-supabase) example from the [Vercel Next.js examples](https://github.com/vercel/next.js/tree/canary/examples).


## 🔧 Modifications from the Original `with-supabase` Template

The following customizations have been made to improve structure, upgrade styling tools, and clean up unused code:

### ✅ Tailwind CSS Upgrade

- Upgraded **Tailwind CSS to v4** for the latest utility features and performance improvements.
- Removed the `tailwind.config.ts` file entirely and migrated to **pure CSS custom properties** for theming in `globals.css`.
- Introduced a more modular, modern theme system using `@theme` mappings and `@custom-variant`.

### ✅ Project Structure Cleanup

- Removed all **`tutorial` components** provided in the example to simplify the project and remove educational scaffolding.
- Achieved a cleaner, more decoupled structure focused solely on real-world usage.

### ✅ Auth Component Refactor

- Moved authentication-related components (such as `SignInButton`, `SignOutButton`, etc.) into a new organized directory:

  ```bash
  components/auth/
  ```

- This improves clarity and maintainability of the authentication logic.

---
## 🚀 Features

- ✅ Supabase Auth (Email/Password signup with email confirmation)
- ✅ SSR-ready authentication
- ✅ Protected routes using middleware
- ✅ Tailwind CSS v4 with fully custom `globals.css` theming (no `tailwind.config.ts`)
- ✅ Cleaner, more maintainable folder structure
- ✅ `auth/` component directory for SignIn / SignOut / Auth UI handling


---
## 📚 Use Cases

This repo is ideal for:
- Developers learning **Supabase Auth** and **Next.js App Router**
- Bootstrapping your own SaaS login system
- Building protected pages with server/client sessions

---

## 🛠️ Getting Started

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME
cd YOUR_REPO_NAME
npm install

# Set up your .env
cp .env.example .env.local
# Fill in your Supabase project URL and anon/public keys

npm run dev
````

Make sure you have a Supabase project created at [https://supabase.com](https://supabase.com), and configure your auth settings accordingly.

---

## 📄 License

MIT — feel free to use, modify, and share.


