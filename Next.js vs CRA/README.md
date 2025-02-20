# Next.js Compared to CRA

## Basics

### Routes

`.js` files inside of pages directory are routes (ex: `pages/about.js` will show as `/about`). `index.js` goes to `/`.

### Rendering

- Static Site Generation (**SSG**) : Pages are pre-rendered at build time. Use `getStaticProps` to fetch data before building.

- Server-Side Rendering (**SSR**): Pages are rendered on each request. Use `getServerSideProps` to fetch data on every request.

- Client-Side Rendering (**CSR**): You can still use CSR with hooks like `useEffect` for fetching data after the page loads.

- Incremental Static Regeneration (**ISR**): Allows you to update static pages after the site is built without needing a full rebuild.

### APIs

You can create API routes directly inside the `pages/api` directory. For example, `pages/api/hello.js` will be accessible at `/api/hello`.

### Static Assets

Static assets should be placed in the `public` folder as well, but Next.js optimizes image handling. You can use the `next/image` component for automatic image optimization.

### CSS and Styling

You can use the same methods, but Next.js also offers built-in support for CSS modules and global CSS. You can import `.css` files directly in your components. If you’re using **styled-components**, you’ll need to configure the server-side rendering support for it.

### Dev and Build

You run `npm run dev` for development, `npm run build` for production, and `npm run start` to serve the production build.

### Environment Variables

You can also use `.env.local`, `.env.development`, and `.env.production` for environment variables. In Next.js, you can expose variables to the client by prefixing them with `NEXT_PUBLIC_`.

### Typescript (optional)

TypeScript is natively supported. You just need to install TypeScript and its dependencies, and Next.js will automatically detect and configure it.

### Deployment

Next.js works seamlessly with **Vercel** (created by the Next.js team) for deployment. It also supports static export, so you can host on platforms like **Netlify** or **AWS**.

## Examples

### Page

```javascript
// pages/index.js
export default function HomePage() {
  return <h1>Welcome to the homepage</h1>;
}
```

#### Fetching data for static generation

```javascript
// pages/posts.js
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();

  return {
    props: { posts },
  };
}

export default function PostsPage({ posts }) {
  return (
    <div>
      <h1>Posts</h1>
      <ul>
        {posts.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```

### API Route

```javascript
// pages/api/hello.js
export default function handler(req, res) {
  res.status(200).json({ message: 'Hello, world!' });
}
```