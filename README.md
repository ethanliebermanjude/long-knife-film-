# Long Knife — longknifefilm.com

Official site for the documentary **Long Knife** — a true crime film about the Osage Nation, the oil that was stolen from them, and Charles Koch.

Narrated by Robert De Niro. Directed by David Ambrose. Written & Produced by Greg Palast.

## Stack

- [Astro 5](https://astro.build) + TypeScript
- [Tailwind CSS 4](https://tailwindcss.com) (via the Vite plugin)
- Deployed on [Vercel](https://vercel.com), connected to this repo
- Domain: `longknifefilm.com`

## Local development

```bash
npm install
npm run dev
```

The site will be available at `http://localhost:4321`.

## Commands

| Command | What it does |
|---|---|
| `npm install` | Install dependencies |
| `npm run dev` | Start the local dev server |
| `npm run build` | Build the production site to `./dist/` |
| `npm run preview` | Preview the built site locally |

## Deployment

Pushes to `main` deploy automatically to Vercel.
Pushes to any other branch get a preview deployment.

## Planning

See [`PLAN.md`](./PLAN.md) for the full build plan, locked decisions, and open dependencies.
