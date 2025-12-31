# Nuxt UI Layer

A reusable Nuxt layer for maintaining consistent design systems across projects.

## Using this Layer in Your Project

To integrate this layer into your Nuxt project, follow these steps:

### 1. Install Dependencies

First, install the required dependencies:

```bash
npm install @nuxt/ui tailwindcss
# or
pnpm add @nuxt/ui tailwindcss
# or
yarn add @nuxt/ui tailwindcss
```

### 2. Create CSS File

Create a `app/assets/css/main.css` file in your project with the following imports:

```css
@import "tailwindcss";
@import "@nuxt/ui";
```

### 3. Extend the Layer

Add this layer to your `nuxt.config.ts` by extending it from GitHub:

```ts
export default defineNuxtConfig({
  extends: ['github:kissle/nuxt-ui-layer'],
  css: ['~/app/assets/css/main.css']
})
```

That's it! Your project will now use this Nuxt UI layer with all its components and styling.

## Setup

Make sure to install the dependencies:

```bash
pnpm install
```

## Working on your layer

Your layer is at the root of this repository, it is exactly like a regular Nuxt project, except you can publish it on NPM.

The `.playground` directory should help you on trying your layer during development.

Running `pnpm dev` will prepare and boot `.playground` directory, which imports your layer itself.

## Distributing your layer

Your Nuxt layer is shaped exactly the same as any other Nuxt project, except you can publish it on NPM.

To do so, you only have to check if `files` in `package.json` are valid, then run:

```bash
npm publish --access public
```

Once done, your users will only have to run:

```bash
npm install --save nuxt-ui-layer
```

Then add the dependency to their `extends` in `nuxt.config`:

```ts
defineNuxtConfig({
  extends: 'nuxt-ui-layer'
})
```

## Development Server

Start the development server on http://localhost:3000

```bash
pnpm dev
```

## Production

Build the application for production:

```bash
pnpm build
```

Or statically generate it with:

```bash
pnpm generate
```

Locally preview production build:

```bash
pnpm preview
```

Checkout the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
