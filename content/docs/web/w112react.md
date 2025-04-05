---
title: "React"
description: ""
summary: ""
date: 2025-03-08T15:48:39+08:00
lastmod: 2025-03-08T15:48:39+08:00
draft: false
weight: 112
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

{{< inline-svg src="svgs/logos/react.svg" width="100px" height="79px" class="svg-inline-custom" >}}

### Syntax

React is a JS library for building UI. It uses JSX to translate a `.js` file into html through JSX syntax. A `.jsx` file is a combination of `.js` and JSX syntax. Hooks is a allows you to use state. Below shows an example of a React application. Source from official react website [tic-tac-toe](https://react.dev/learn/tutorial-tic-tac-toe)

{{< details "React Application Example">}}

```js
import { useState } from 'react';

// Square component, props is sent through parameters
function Square({ value, onSquareClick }) {
  return (
    <button className="square" onClick={onSquareClick}>
      {value}
    </button>
  );
}

// Board component, returns in <> </> for multiples elements
function Board({ xIsNext, squares, onPlay }) {
  function handleClick(i) {
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    const nextSquares = squares.slice();
    if (xIsNext) {
      nextSquares[i] = 'X';
    } else {
      nextSquares[i] = 'O';
    }
    onPlay(nextSquares);
  }

  const winner = calculateWinner(squares);
  let status;
  if (winner) {
    status = 'Winner: ' + winner;
  } else {
    status = 'Next player: ' + (xIsNext ? 'X' : 'O');
  }

  return (
    <>
      <div className="status">{status}</div>
      <div className="board-row">
        <Square value={squares[0]} onSquareClick={() => handleClick(0)} />
        <Square value={squares[1]} onSquareClick={() => handleClick(1)} />
        <Square value={squares[2]} onSquareClick={() => handleClick(2)} />
      </div>
      <div className="board-row">
        <Square value={squares[3]} onSquareClick={() => handleClick(3)} />
        <Square value={squares[4]} onSquareClick={() => handleClick(4)} />
        <Square value={squares[5]} onSquareClick={() => handleClick(5)} />
      </div>
      <div className="board-row">
        <Square value={squares[6]} onSquareClick={() => handleClick(6)} />
        <Square value={squares[7]} onSquareClick={() => handleClick(7)} />
        <Square value={squares[8]} onSquareClick={() => handleClick(8)} />
      </div>
    </>
  );
}

// Usestate is a hook, history is the reactive variable, setHistory is the function to set the reactive variable
export default function Game() {
  const [history, setHistory] = useState([Array(9).fill(null)]);
  const [currentMove, setCurrentMove] = useState(0);
  const xIsNext = currentMove % 2 === 0;
  const currentSquares = history[currentMove];

  function handlePlay(nextSquares) {
    const nextHistory = [...history.slice(0, currentMove + 1), nextSquares];
    setHistory(nextHistory);
    setCurrentMove(nextHistory.length - 1);
  }

  function jumpTo(nextMove) {
    setCurrentMove(nextMove);
  }

  const moves = history.map((squares, move) => {
    let description;
    if (move > 0) {
      description = 'Go to move #' + move;
    } else {
      description = 'Go to game start';
    }
    return (
      <li key={move}>
        <button onClick={() => jumpTo(move)}>{description}</button>
      </li>
    );
  });

  return (
    <div className="game">
      <div className="game-board">
        <Board xIsNext={xIsNext} squares={currentSquares} onPlay={handlePlay} />
      </div>
      <div className="game-info">
        <ol>{moves}</ol>
      </div>
    </div>
  );
}

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

{{< /details >}}

### Getting started

There is two way to get started in react: starting with a framework or start from scratch. Some common frameworks are `Next.js`, `React Router`, `Expo` (for universal app). Starting from scratch is more complicated and requires to choose build tools, routing, etc.

In this part, we'll use Next.js by Vercel to make a react application. Next.js is a react framework with dev tool, and able to host on Vercel easily. Follow the tutorial on [Next.js](https://nextjs.org/docs/app/getting-started/installation) to get started, as tutorial in this page is based on the vercel tutorial website. We'll use typescript, eslint, tailwind, next project structure, app router and set out initial settings.

### Next.js

```bash
# Use npx to install Next.js template
npx create-next-app@latest nextjs-dashboard --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example" --use-pnpm

# pnpm is more efficient than npm
pnpm i
pnpm dev
```

#### CSS

There is two different way of styling in Next.js

1. Using Tailwind

```css {title="/app/ui/global.css"}
@tailwind base;
@tailwind components;
@tailwind utilities;
```

2. Using CSS Modules

```css {title="/app/ui/home.module.css"}
.shape {
  height: 0;
}
```

Import global styles in loot layout

```tsx {title="app/layout.tsx"}
import '@/app/ui/global.css';                   // Tailwind
import styles from '@/app/ui/home.module.css';  // CSS Modules
 
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
      <div className={styles.shape} />
    </html>
  );
}
```

Use `clsx` library to toggle class names based on condition to change the appearance.

```tsx {title="/app/ui/invoices/status.tsx"}
import clsx from 'clsx';
 
export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-gray-100 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}
```

#### Utilities

Some tools in React provide better functionaly to control the website, like SEO, rendering optimization, etc. Use those such as Font, Image, Link, Skeleton for good.

Vercel also provide database, analytics, etc. Just click on the platform and seamlessly integrate with your Next.js app.

#### Routing

```txt
src/
│── app/  (if using App Router - Next.js 13+)
│   ├── page.jsx           → "/"
│   ├── about.jsx          → "/about"
│   ├── blog/
│   │   ├── page.jsx       → "/blog"
│   │   ├── [id].jsx       → "/blog/:id" (Dynamic Route)
│   ├── dashboard/
│   │   ├── (overview)       → "/dashboard"
|   │   │   ├── page.jsx     → "/dashboard"
|   │   │   ├── loading.jsx  → "/dashboard/loading"
│   │   ├── (random)       → "/dashboard"
|   │   │   ├── settings.jsx → "/dashboard/settings"
│   ├── api/               → API Routes
│   │   ├── hello.jsx       → "/api/hello"
│   ├── _app.jsx            → Custom App Component (for global state or layout)
│   ├── _document.jsx       → Custom Document (for meta tags, fonts)
│── components/
│── public/
│── styles/
│── next.config.jsx
```

#### Fallback

Component will render skeleton while awaiting for data to be fetched. To make it feel like streaming, only fallback the components to be updated.

```tsx
<div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
  <Suspense fallback={<RevenueChartSkeleton />}>
    <RevenueChart />
  </Suspense>
  <LatestInvoices latestInvoices={latestInvoices} />
</div>
```

#### Rendering

In default, `Next.js` is SSR. Add the line `'use client';` in the first line of the page file to set as CSR.

#### Path API

Next.js provide path API to generate dynamic routes.

- `useSearchParams` access the parameters of current URL. For example, `/dashboard/invoices?page=1&query=pending` is `{page: '1', query: 'pending'}`.
- `usePathname` read the current URL's pathname.
- `useRouter` navigation between routes within client components programmatically.

The code belows how search component should be programmed.

```tsx {title="/app/ui/search.tsx"}
'use client';

import { useSearchParams, usePathname, useRouter } from 'next/navigation';

export default function Search({ placeholder }: { placeholder: string }) {
  const searchParams = useSearchParams();
  const pathname = usePathname();
  const { replace } = useRouter();
  
  const handleSearch = useDebouncedCallback((term) => {
    const params = new URLSearchParams(searchParams);
    params.set('page', '1');
    if (term) {
      params.set('query', term);
    } else {
      params.delete('query');
    }
    replace(`${pathname}?${params.toString()}`);
  }, 300);
  
  return (
      <input
        className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
        placeholder={placeholder}
        onChange={(e) => {
          handleSearch(e.target.value);
        }}
        defaultValue={searchParams.get('query')?.toString()}
      />
  );
}
```

The code below show how the page shoud be programmed.

```tsx {title="/app/page.tsx"}
import Pagination from '@/app/ui/invoices/pagination';
import Search from '@/app/ui/search';
import Table from '@/app/ui/invoices/table';
import { CreateInvoice } from '@/app/ui/invoices/buttons';
import { InvoicesTableSkeleton } from '@/app/ui/skeletons';
import { Suspense } from 'react';
import { fetchInvoicesPages } from '@/app/lib/data';
 
export default async function Page(props: {
  searchParams?: Promise<{
    query?: string;
    page?: string;
  }>;
}) {
  const searchParams = await props.searchParams;
  const query = searchParams?.query || '';
  const currentPage = Number(searchParams?.page) || 1;
  const totalPages = await fetchInvoicesPages(query);

  return (
    <>
      <div>
        <Search placeholder="Search invoices..." />
        <CreateInvoice />
      </div>
       <Suspense key={query + currentPage} fallback={<InvoicesTableSkeleton />}>
        {/* Props goes here */}
        <Table query={query} currentPage={currentPage} />
      </Suspense>
      <div>
        <Pagination totalPages={totalPages} />
      </div> 
    </>
  );
}
```

#### Server Action

Next.js allow for server-side data CRUD without using API. In the file, add `'use server';` line to mark all the exported functions within the file as Server Action.

Form validation can be done using Zod. `revalidatePath` can be used to refresh the page.

```tsx {title="/app/lib/actions.tsx"}
"use server";

import { z } from "zod";
import { revalidatePath } from "next/cache";
import { redirect } from "next/navigation";
import postgres from "postgres";

const sql = postgres(process.env.POSTGRES_URL!, { ssl: "require" });

// Form validation
const FormSchema = z.object({
  id: z.string(),
  customerId: z.string(),
  amount: z.coerce.number(),
  status: z.enum(["pending", "paid"]), 
  date: z.string(),
});

const CreateInvoice = FormSchema.omit({ id: true, date: true });
const UpdateInvoice = FormSchema.omit({ id: true, date: true });

export async function createInvoice(formData: FormData) {
  const { customerId, amount, status } = CreateInvoice.parse({
    customerId: formData.get("customerId"),
    amount: formData.get("amount"),
    status: formData.get("status"),
  });
  const amountInCents = amount * 100;
  const date = new Date().toISOString().split("T")[0];

  try {
    await sql`
          INSERT INTO invoices (customer_id, amount, status, date)
          VALUES (${customerId}, ${amountInCents}, ${status}, ${date})
        `;
  } catch (error) {
    // We'll log the error to the console for now
    console.error(error);
  }

  revalidatePath("/dashboard/invoices");
  redirect("/dashboard/invoices");
}

export async function updateInvoice(id: string, formData: FormData) {
  const { customerId, amount, status } = UpdateInvoice.parse({
    customerId: formData.get("customerId"),
    amount: formData.get("amount"),
    status: formData.get("status"),
  });

  const amountInCents = amount * 100;

  try {
    await sql`
        UPDATE invoices
        SET customer_id = ${customerId}, amount = ${amountInCents}, status = ${status}
        WHERE id = ${id}
      `;
  } catch (error) {
    // We'll log the error to the console for now
    console.error(error);
  }

  revalidatePath("/dashboard/invoices");
  redirect("/dashboard/invoices");
}

export async function deleteInvoice(id: string) {
  throw new Error("Failed to Delete Invoice");

  await sql`DELETE FROM invoices WHERE id = ${id}`;
  revalidatePath("/dashboard/invoices");
}

```

#### Error Handling

Run `throw new Error('Failed to Delete Invoice');` to show error page. `notFound` can be used to display 404.

``` tsx {title="/dashboard/invoices/error.tsx"}
'use client';
 
import { useEffect } from 'react';
 
export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  useEffect(() => {
    // Optionally log the error to an error reporting service
    console.error(error);
  }, [error]);
 
  return (
    <main className="flex h-full flex-col items-center justify-center">
      <h2 className="text-center">Something went wrong!</h2>
      <button
        className="mt-4 rounded-md bg-blue-500 px-4 py-2 text-sm text-white transition-colors hover:bg-blue-400"
        onClick={
          // Attempt to recover by trying to re-render the invoices route
          () => reset()
        }
      >
        Try again
      </button>
    </main>
  );
}
```

#### Accessibility

Accessibility refers to designing and implementing web applications that everyone can use. You have sematic HTML, label tag, focus outline, ESLint, zod for form validation. Next.js have `useActionState` hook to perform custom action on form submit for form validation.

#### Authentication

`Authentication` is about making sure the user is who they say they are. `Authorization` decides what parts of the application are allowed to use. Next.js has middleware to handle authentication in multiple ways.

#### Metadata

Next.js have metadata utilities to boost SEO.