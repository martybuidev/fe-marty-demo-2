# Marty Frontend

Next.js App Router with TypeScript and Tailwind CSS.

## Requirements

- Node.js 22.23.1, pinned in `.nvmrc`.
- pnpm 11.22.0, pinned in `package.json`.

## Development

```bash
nvm use
pnpm install --frozen-lockfile
pnpm dev
```

Open <http://localhost:3000>.

## Verification

```bash
pnpm lint
pnpm exec next typegen
pnpm exec tsc --noEmit
pnpm build
```

For a production smoke check, run `pnpm start` after building.

## Structure

- `src/app/`: routes, root layout, and global styles.
- `@/*`: imports relative to `src/`.

Keep configuration and future `public/` assets at the project root. Shared,
module, and feature folders will be introduced when their functionality is added.
