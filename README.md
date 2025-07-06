## 🔧 Modifications from the Original `with-supabase` Template

This project is based on the official [`with-supabase`](https://github.com/vercel/next.js/tree/canary/examples/with-supabase) example from the [Vercel Next.js examples](https://github.com/vercel/next.js/tree/canary/examples).

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
