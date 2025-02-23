# Prostore

A full featured Ecommerce website built with Next.js, TypeScript, PostgreSQL and Prisma.

<img src="/public/images/screen.png" alt="Next.js Ecommerce" />

This project is from my **Next.js Ecommerce course**

- Traversy Media: [https://www.traversymedia.com/nextjs-ecommerce](https://www.traversymedia.com/nextjs-ecommerce)
- Udemy: [https://www.udemy.com/course/nextjs-ecommerce-course](https://www.udemy.com/course/nextjs-ecommerce-course)

## Table of Contents

<!--toc:start-->

- [Features](#features)
- [Usage](#usage)
  - [Install Dependencies](#install-dependencies)
  - [Environment Variables](#environment-variables)
    - [PostgreSQL Database URL](#postgresql-database-url)
    - [Next Auth Secret](#next-auth-secret)
    - [PayPal Client ID and Secret](#paypal-client-id-and-secret)
    - [Stripe Publishable and Secret Key](#stripe-publishable-and-secret-key)
    - [Uploadthing Settings](#uploadthing-settings)
    - [Resend API Key](#resend-api-key)
  - [Run](#run)
- [Prisma Studio](#prisma-studio)
- [Seed Database](#seed-database)
- [Demo](#demo)
- [Bug Fixes And Course FAQ](#bug-fixes-and-course-faq)
  - [Fix: Edge Function Middleware Limitations on Vercel](#fix-edge-function-middleware-limitations-on-vercel)
  - [Bug: A newly logged in user can inherit the previous users cart](#bug-a-newly-logged-in-user-can-inherit-the-previous-users-cart)
  - [Bug: Any user can see another users order](#bug-any-user-can-see-another-users-order)
  - [Bug: Cart add and remove buttons share loading animation](#bug-cart-add-and-remove-buttons-share-loading-animation)
- [License](#license)
<!--toc:end-->

## Features

- Next Auth authentication
- Admin area with stats & chart using Recharts
- Order, product and user management
- User area with profile and orders
- Stripe API integration
- PayPal integration
- Cash on delivery option
- Interactive checkout process
- Featured products with banners
- Multiple images using Uploadthing
- Ratings & reviews system
- Search form (customer & admin)
- Sorting, filtering & pagination
- Dark/Light mode
- Much more

## Usage

### Install Dependencies

```bash
npm install
```

Note: Some dependencies may have not yet been upadated to support React 19. If you get any errors about depencency compatability, run the following:

```bash
npm install --legacy-peer-deps
```

### Environment Variables

Rename the `.example-env` file to `.env` and add the following

#### PostgreSQL Database URL

Sign up for a free PostgreSQL database through Vercel. Log into Vercel and click on "Storage" and create a new Postgres database. Then add the URL.

**Example:**

```
DATABASE_URL="postgresql://username:password@host:port/dbname"
```

#### Next Auth Secret

Generate a secret with the following command and add it to your `.env`:

```bash
openssl rand -base64 32
```

**Example:**

```
NEXTAUTH_SECRET="xmVpackzg9sdkEPzJsdGse3dskUY+4ni2quxvoK6Go="
```

#### PayPal Client ID and Secret

Create a PayPal developer account and create a new app to get the client ID and secret.

**Example:**

```
PAYPAL_CLIENT_ID="AeFIdonfA_dW_ncys8G4LiECWBI9442IT_kRV15crlmMApC6zpb5Nsd7zlxj7UWJ5FRZtx"
PAYPAL_APP_SECRET="REdG53DEeX_ShoPawzM4vQHCYy0a554G3xXmzSxFCDcSofBBTq9VRqjs6xsNVBcbjqz--HiiGoiV"
```

#### Stripe Publishable and Secret Key

Create a Stripe account and get the publishable and secret key.

**Example:**

```
STRIPE_SECRET_KEY="sk_test_51QIr0IG87GyTererxmXxEeqV6wuzbmC0TpkRzabxqy3P4BpzpzDqnQaC1lZhmYg6IfNarnvpnbjjw5dsBq4afd0FXkeDriR"
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY="pk_test_51QIr0Ids7GyT6H7X6R5GoEA68lYDcbcC94VU0U02SMkrrrYZT2CgSMZ1h22udb5Rg1AuonXyjmAQZESLLj100W3VGVwze"
```

#### Uploadthing Settings

Sign up for an account at https://uploadthing.com/ and get the token, secret and app ID.

**Example:**

```
UPLOADTHING_TOKEN='tyJhcGlLZXkiOiJza19saXZlXzQ4YTE2ZjhiMDE5YmFiOgrgOWQ4MmYxMGQxZGU2NTM3YzlkZGI3YjNiZDk3MmRhNGZmNGMwMmJlOWI2Y2Q0N2UiLCJhcHBJZCI6InRyejZ2NHczNzUiLCJyZWdpb25zIjpbInNlYTEiXX0='
UPLOADTHIUG_SECRET='gg'
UPLOADTHING_APPID='trz6vd475'
```

#### Resend API Key

Sign up for an account at https://resend.io/ and get the API key.

**Example:**

```
RESEND_API_KEY="re_ZnhUfrjR_QD2cDqdee3iYCrkfvPYFCYiXm"
```

### Run

```bash

# Run in development mode
npm run dev

# Build for production
npm run build

# Run in production mode
npm start

# Export static site
npm run export
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## Prisma Studio

To open Prisma Studio, run the following command:

```bash
npx prisma studio
```

## Seed Database

To seed the database with sample data, run the following command:

```bash
npx tsx ./db/seed
```

## Demo

I am not sure how long I will have this demo up but you can view it here:

[ https://prostore-one.vercel.app/ ](https://prostore-one.vercel.app/)

## Bug Fixes And Course FAQ

### Fix: Edge Function Middleware Limitations on Vercel

After deploying your app you may be getting a build error along the lines of:

> The Edge Function "middleware size is 1.03 MB and your plan size limit is 1MB

For the solution to resolve this please see Brads [Gist here](https://gist.github.com/bradtraversy/16e3c89b9b25bc79cf86f5f36e14e83d)

There is also a new lesson added for this fix at the end of the course -
**Vercel Hobby Tier Fix**

### Bug: A newly logged in user can inherit the previous users cart

If a logged in user adds items to their cart and logs out then a different user
logs in on the same machine, they will inherit the first users cart.

To fix this we can delete the current users **Cart** from the database in our **lib/actions/user.actions.ts** `signOutUser` action.

> Changes can be seen in [lib/actions/user.actions.ts](https://github.com/bradtraversy/prostore/blob/a498d4362d1485b2bd3152124cb5c3a75f8fdd70/lib/actions/user.actions.ts#L45)

### Bug: Any user can see another users order

If a user knows the `Order.id` of another users order it is possible for them to
visit **/order/<Order.id>** and see that other users order. This isn't likely to
happen in reality but should be something we protect against by redirecting the
user to our **/unauthorized** page if they are not the owner of the order.

In **app/(root)/order/[id]/page.tsx** we can import the `redirect` function from Next:

```ts
import { notFound, redirect } from 'next/navigation';
```

Then check if the user is the owner of the order and redirect them if not:

```ts
// Redirect the user if they don't own the order
if (order.userId !== session?.user.id) {
  return redirect('/unauthorized');
}
```

> Changes can be seen in [app/(root)/order/[id]/page.tsx](<https://github.com/bradtraversy/prostore/blob/main/app/(root)/order/%5Bid%5D/page.tsx>)

### Bug: Cart add and remove buttons share loading animation

On our **/cart** page you may notice that when you increment or decrement the
quantity of an item in the cart, then the loader shows for all buttons after we
click. This is because all the buttons use the same **pending** state from our
use of `useTransition` in our [app/(root)/cart/cart-table.tsx](<https://github.com/bradtraversy/prostore/blob/main/app/(root)/cart/cart-table.tsx>)

We can solve this by breaking out the Buttons into their own `AddButton` and
`RemoveButton` components, each using their own `useTransition` and so having
their own **pending** state.

You can if you wish move these components to their own files/modules but for
ease of following along they can be seen in the same file.

> Changes can be seen in [app/(root)/cart/cart-table.tsx](<https://github.com/bradtraversy/prostore/blob/main/app/(root)/cart/cart-table.tsx>)

## License

MIT License

Copyright (c) [2025] [Traversy Media]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall
