# Next.js Setup Guide for Next News

This guide provides comprehensive instructions to set up **Next.js** for the **Next News** project. By following these steps, you'll configure a robust frontend that integrates seamlessly with Strapi and Shadcn, ensuring a high-performance, scalable, and maintainable application.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [1. Install Node.js and npm](#1-install-nodejs-and-npm)
  - [2. Create a New Next.js Project](#2-create-a-new-nextjs-project)
  - [3. Install Required Dependencies](#3-install-required-dependencies)
  - [4. Set Up Tailwind CSS](#4-set-up-tailwind-css)
  - [5. Install Shadcn UI Components](#5-install-shadcn-ui-components)
- [Configuration](#configuration)
  - [1. Configure Tailwind CSS](#1-configure-tailwind-css)
  - [2. Configure Shadcn](#2-configure-shadcn)
  - [3. Environment Variables](#3-environment-variables)
- [Integrating with Strapi](#integrating-with-strapi)
  - [1. API Integration](#1-api-integration)
  - [2. Fetching Data](#2-fetching-data)
- [Creating Pages and Components](#creating-pages-and-components)
  - [1. Pages Directory](#1-pages-directory)
  - [2. Components Directory](#2-components-directory)
- [State Management](#state-management)
  - [Using React Context API](#using-react-context-api)
  - [Optional: Integrate Redux or Zustand](#optional-integrate-redux-or-zustand)
- [Routing and Navigation](#routing-and-navigation)
  - [File-Based Routing](#file-based-routing)
  - [Dynamic Routes](#dynamic-routes)
  - [Navigation Bar](#navigation-bar)
- [Styling and Theming](#styling-and-theming)
  - [Using Tailwind CSS](#using-tailwind-css)
  - [Custom Themes with Shadcn](#custom-themes-with-shadcn)
- [Performance Optimization](#performance-optimization)
  - [Static Site Generation (SSG)](#static-site-generation-ssg)
  - [Server-Side Rendering (SSR)](#server-side-rendering-ssr)
  - [Incremental Static Regeneration (ISR)](#incremental-static-regeneration-isr)
  - [Image Optimization](#image-optimization)
- [Testing](#testing)
  - [Unit Testing with Jest](#unit-testing-with-jest)
  - [Integration Testing with React Testing Library](#integration-testing-with-react-testing-library)
  - [End-to-End Testing with Cypress](#end-to-end-testing-with-cypress)
- [Running the Development Server](#running-the-development-server)
- [Building for Production](#building-for-production)
- [Deployment Considerations](#deployment-considerations)
- [Troubleshooting](#troubleshooting)
- [Additional Resources](#additional-resources)
- [Footer](#footer)

## Prerequisites

Before setting up Next.js for **Next News**, ensure you have the following:

- **Node.js** (v14 or later)
- **npm** or **Yarn** (package manager)
- **Git** (optional, for version control)
- **Strapi Backend**: Ensure your Strapi backend is set up and running. Refer to the [Strapi Setup Guide](./Strapi_Setup.md) if needed.

## Installation

### 1. Install Node.js and npm

If you haven't installed Node.js and npm yet, download and install them from the [official Node.js website](https://nodejs.org/).

Verify the installation:

```bash
node -v
npm -v
```

### 2. Create a New Next.js Project

Navigate to your desired directory and create a new Next.js project using `create-next-app`.

```bash
# Using npm
npx create-next-app@latest next-news-frontend

# Using Yarn
yarn create next-app next-news-frontend
```

Follow the prompts to set up your project. For this guide, we'll assume the project name is `next-news-frontend`.

### 3. Install Required Dependencies

Navigate to your project directory and install necessary dependencies, including Shadcn and other UI libraries.

```bash
cd next-news-frontend

# Install Shadcn and its dependencies
npm install @shadcn/ui @radix-ui/react-icons @headlessui/react

# Install additional dependencies
npm install axios swr
```

**Note:** You can replace `npm` with `yarn` if you prefer using Yarn as your package manager.

### 4. Set Up Tailwind CSS

Tailwind CSS is essential for styling and works seamlessly with Shadcn.

1. **Install Tailwind CSS and its dependencies:**

   ```bash
   npm install -D tailwindcss postcss autoprefixer
   npx tailwindcss init -p
   ```

2. **Configure Tailwind to remove unused styles in production:**

   Update the `tailwind.config.js` file:

   ```javascript
   // tailwind.config.js
   module.exports = {
     content: [
       "./pages/**/*.{js,ts,jsx,tsx}",
       "./components/**/*.{js,ts,jsx,tsx}",
       "./app/**/*.{js,ts,jsx,tsx}", // Include if using the App directory
     ],
     theme: {
       extend: {},
     },
     plugins: [],
   };
   ```

3. **Add Tailwind directives to your CSS:**

   Create or update the `styles/globals.css` file:

   ```css
   /* styles/globals.css */
   @tailwind base;
   @tailwind components;
   @tailwind utilities;
   ```

4. **Import the CSS in your application:**

   Ensure that `globals.css` is imported in `pages/_app.js` or `pages/_app.tsx`:

   ```javascript
   // pages/_app.js or pages/_app.tsx
   import "../styles/globals.css";

   function MyApp({ Component, pageProps }) {
     return <Component {...pageProps} />;
   }

   export default MyApp;
   ```

### 5. Install Shadcn UI Components

Shadcn provides a collection of accessible and customizable UI components built with Radix UI and Tailwind CSS.

1. **Install Shadcn CLI (optional):**

   Shadcn offers a CLI tool to streamline component integration.

   ```bash
   npm install -g shadcn
   ```

2. **Initialize Shadcn in Your Project:**

   ```bash
   shadcn init
   ```

   Follow the prompts to select the components you wish to install.

3. **Manual Installation (if not using the CLI):**

   Alternatively, you can manually add Shadcn components by copying them into your `components` directory from the [Shadcn UI repository](https://github.com/shadcn/ui).

## Configuration

### 1. Configure Tailwind CSS

Ensure Tailwind CSS is correctly set up to work with Shadcn components.

```javascript
// tailwind.config.js
module.exports = {
  content: [
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",
    "./app/**/*.{js,ts,jsx,tsx}", // Include if using the App directory
  ],
  theme: {
    extend: {
      colors: {
        primary: "#1E40AF",
        secondary: "#9333EA",
      },
    },
  },
  plugins: [
    require("@tailwindcss/forms"), // Optional: For better form styling
    require("@tailwindcss/typography"), // Optional: For better typography
  ],
};
```

### 2. Configure Shadcn

Customize Shadcn components by modifying Tailwind configurations or overriding component styles.

```javascript
// Example: Extending theme in tailwind.config.js
module.exports = {
  // ...existing configuration
  theme: {
    extend: {
      colors: {
        primary: "#1E40AF",
        secondary: "#9333EA",
      },
    },
  },
  // ...existing configuration
};
```

### 3. Environment Variables

Create a `.env.local` file in the root of your Next.js project to manage environment variables.

```env
# .env.local

# API URL for Strapi backend
NEXT_PUBLIC_API_URL=https://your-strapi-backend-domain.com

# Site Metadata
NEXT_PUBLIC_SITE_TITLE=Next News
NEXT_PUBLIC_SITE_DESCRIPTION=A modern news portal built with Strapi and Next.js

# Add other frontend-specific environment variables as needed
```

**Security Note:** Ensure that sensitive information is not exposed via `NEXT_PUBLIC_*` variables. Only use `NEXT_PUBLIC_*` for variables that need to be accessible on the client side.

## Integrating with Strapi

### 1. API Integration

Use `axios` or `swr` to interact with the Strapi backend.

```bash
npm install axios swr
```

**Example: Creating an API Utility**

```javascript
// utils/api.js
import axios from "axios";

const api = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL || "http://localhost:1337",
});

export default api;
```

### 2. Fetching Data

Use `swr` for data fetching with caching and revalidation.

```javascript
// Example: Fetching Articles
import useSWR from "swr";
import api from "../utils/api";

const fetcher = (url) => api.get(url).then((res) => res.data);

export function useArticles() {
  const { data, error } = useSWR("/api/articles?populate=*", fetcher);

  return {
    articles: data?.data,
    isLoading: !error && !data,
    isError: error,
  };
}
```

**Example: Displaying Articles in a Page**

```javascript
// pages/index.js
import { useArticles } from "../hooks/useArticles";
import ArticleCard from "../components/ArticleCard";

export default function HomePage() {
  const { articles, isLoading, isError } = useArticles();

  if (isLoading) return <p>Loading...</p>;
  if (isError) return <p>Error loading articles.</p>;

  return (
    <div className="container mx-auto px-4">
      <h1 className="text-4xl font-bold my-8">Latest News</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        {articles.map((article) => (
          <ArticleCard key={article.id} article={article.attributes} />
        ))}
      </div>
    </div>
  );
}
```

## Creating Pages and Components

### 1. Pages Directory

Next.js uses the `pages` directory for routing. Each file corresponds to a route.

**Example: Creating an Article Page**

```javascript
// pages/articles/[id].js
import { useRouter } from "next/router";
import useSWR from "swr";
import api from "../../utils/api";

const fetcher = (url) => api.get(url).then((res) => res.data);

export default function ArticlePage() {
  const router = useRouter();
  const { id } = router.query;
  const { data, error } = useSWR(
    id ? `/api/articles/${id}?populate=*` : null,
    fetcher
  );

  if (error) return <p>Error loading article.</p>;
  if (!data) return <p>Loading...</p>;

  const article = data.data.attributes;

  return (
    <div className="container mx-auto px-4 py-8">
      <h1 className="text-3xl font-bold mb-4">{article.title}</h1>
      <p className="text-gray-700 mb-6">{article.content}</p>
      {/* Add more article details like author, category, images */}
    </div>
  );
}
```

### 2. Components Directory

Create reusable components to build your UI.

**Example: ArticleCard Component**

```javascript
// components/ArticleCard.js
import Link from "next/link";
import Image from "next/image";

export default function ArticleCard({ article }) {
  return (
    <div className="border rounded-lg overflow-hidden shadow-md">
      {article.featured_image && (
        <Image
          src={article.featured_image.data.attributes.url}
          alt={article.title}
          width={500}
          height={300}
          className="w-full h-48 object-cover"
        />
      )}
      <div className="p-4">
        <h2 className="text-xl font-semibold mb-2">{article.title}</h2>
        <p className="text-gray-600 mb-4">
          {article.content.substring(0, 100)}...
        </p>
        <Link href={`/articles/${article.id}`}>
          <a className="text-blue-500 hover:underline">Read More</a>
        </Link>
      </div>
    </div>
  );
}
```

## State Management

### Using React Context API

For managing global state like user authentication or theme settings, utilize React Context.

**Example: Creating a Theme Context**

```javascript
// context/ThemeContext.js
import { createContext, useState, useEffect } from "react";

export const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  useEffect(() => {
    // Check for saved theme in localStorage
    const savedTheme = localStorage.getItem("theme") || "light";
    setTheme(savedTheme);
    document.documentElement.classList.add(savedTheme);
  }, []);

  const toggleTheme = () => {
    const newTheme = theme === "light" ? "dark" : "light";
    document.documentElement.classList.remove(theme);
    document.documentElement.classList.add(newTheme);
    setTheme(newTheme);
    localStorage.setItem("theme", newTheme);
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

**Wrapping the Application with ThemeProvider**

```javascript
// pages/_app.js or pages/_app.tsx
import "../styles/globals.css";
import { ThemeProvider } from "../context/ThemeContext";

function MyApp({ Component, pageProps }) {
  return (
    <ThemeProvider>
      <Component {...pageProps} />
    </ThemeProvider>
  );
}

export default MyApp;
```

### Optional: Integrate Redux or Zustand

For more complex state management needs, consider integrating libraries like Redux or Zustand.

**Example: Setting Up Redux**

```bash
npm install redux react-redux @reduxjs/toolkit
```

**Configure Redux Store**

```javascript
// store/store.js
import { configureStore } from "@reduxjs/toolkit";
import userReducer from "./userSlice";

export const store = configureStore({
  reducer: {
    user: userReducer,
  },
});
```

**Provide the Store to the Application**

```javascript
// pages/_app.js or pages/_app.tsx
import "../styles/globals.css";
import { Provider } from "react-redux";
import { store } from "../store/store";

function MyApp({ Component, pageProps }) {
  return (
    <Provider store={store}>
      <Component {...pageProps} />
    </Provider>
  );
}

export default MyApp;
```

## Routing and Navigation

### File-Based Routing

Next.js uses a file-based routing system where each file in the `pages` directory corresponds to a route.

**Example: About Page**

```javascript
// pages/about.js
export default function About() {
  return (
    <div className="container mx-auto px-4 py-8">
      <h1 className="text-3xl font-bold">About Next News</h1>
      <p className="mt-4">
        Next News is a modern news portal built with Strapi and Next.js.
      </p>
    </div>
  );
}
```

### Dynamic Routes

Handle dynamic content like individual articles using dynamic routes.

**Example: Dynamic Article Route**

```javascript
// pages/articles/[id].js
import { useRouter } from "next/router";
import useSWR from "swr";
import api from "../../utils/api";
import ArticleCard from "../../components/ArticleCard";

const fetcher = (url) => api.get(url).then((res) => res.data);

export default function ArticlePage() {
  const router = useRouter();
  const { id } = router.query;
  const { data, error } = useSWR(
    id ? `/api/articles/${id}?populate=*` : null,
    fetcher
  );

  if (error) return <p>Error loading article.</p>;
  if (!data) return <p>Loading...</p>;

  const article = data.data.attributes;

  return (
    <div className="container mx-auto px-4 py-8">
      <h1 className="text-3xl font-bold mb-4">{article.title}</h1>
      <p className="text-gray-700 mb-6">{article.content}</p>
      {/* Additional article details */}
    </div>
  );
}
```

### Navigation Bar

Create a reusable navigation bar component for consistent navigation across pages.

**Example: Navbar Component**

```javascript
// components/Navbar.js
import Link from "next/link";
import { useContext } from "react";
import { ThemeContext } from "../context/ThemeContext";

export default function Navbar() {
  const { theme, toggleTheme } = useContext(ThemeContext);

  return (
    <nav className="bg-white dark:bg-gray-800 shadow">
      <div className="container mx-auto px-4 py-4 flex justify-between items-center">
        <Link href="/">
          <a className="text-xl font-bold text-gray-800 dark:text-white">
            Next News
          </a>
        </Link>
        <div className="flex items-center space-x-4">
          <Link href="/about">
            <a className="text-gray-800 dark:text-white">About</a>
          </Link>
          <button
            onClick={toggleTheme}
            className="text-gray-800 dark:text-white focus:outline-none"
          >
            {theme === "light" ? "🌙" : "☀️"}
          </button>
        </div>
      </div>
    </nav>
  );
}
```

**Include Navbar in Application**

```javascript
// pages/_app.js or pages/_app.tsx
import "../styles/globals.css";
import { ThemeProvider } from "../context/ThemeContext";
import Navbar from "../components/Navbar";

function MyApp({ Component, pageProps }) {
  return (
    <ThemeProvider>
      <Navbar />
      <Component {...pageProps} />
    </ThemeProvider>
  );
}

export default MyApp;
```

## Styling and Theming

### Using Tailwind CSS

Leverage Tailwind CSS utility classes to style your components efficiently.

**Example: Styling a Button**

```javascript
// components/Button.js
export default function Button({ children, onClick, variant = "primary" }) {
  const baseStyles = "px-4 py-2 rounded-md font-semibold focus:outline-none";
  const variantStyles =
    variant === "primary"
      ? "bg-blue-500 text-white hover:bg-blue-600"
      : "bg-gray-200 text-gray-800 hover:bg-gray-300";

  return (
    <button onClick={onClick} className={`${baseStyles} ${variantStyles}`}>
      {children}
    </button>
  );
}
```

### Custom Themes with Shadcn

Customize Shadcn components by modifying Tailwind CSS configurations or overriding component styles.

**Example: Customizing Button Colors**

```javascript
// tailwind.config.js
module.exports = {
  // ...existing configuration
  theme: {
    extend: {
      colors: {
        primary: "#1E40AF",
        secondary: "#9333EA",
      },
    },
  },
  // ...existing configuration
};
```

## Performance Optimization

### Static Site Generation (SSG)

Pre-render pages at build time for improved performance and SEO.

**Example: Using `getStaticProps`**

```javascript
// pages/index.js
import api from "../utils/api";
import ArticleCard from "../components/ArticleCard";

export async function getStaticProps() {
  const res = await api.get("/api/articles?populate=*");
  const articles = res.data.data;

  return {
    props: {
      articles,
    },
    revalidate: 60, // Revalidate every 60 seconds
  };
}

export default function HomePage({ articles }) {
  return (
    <div className="container mx-auto px-4">
      <h1 className="text-4xl font-bold my-8">Latest News</h1>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        {articles.map((article) => (
          <ArticleCard key={article.id} article={article.attributes} />
        ))}
      </div>
    </div>
  );
}
```

### Server-Side Rendering (SSR)

Render pages on each request for dynamic content.

**Example: Using `getServerSideProps`**

```javascript
// pages/articles/[id].js
import api from "../../utils/api";
import ArticleDetail from "../../components/ArticleDetail";

export async function getServerSideProps(context) {
  const { id } = context.params;
  const res = await api.get(`/api/articles/${id}?populate=*`);
  const article = res.data.data;

  return {
    props: {
      article,
    },
  };
}

export default function ArticlePage({ article }) {
  return <ArticleDetail article={article.attributes} />;
}
```

### Incremental Static Regeneration (ISR)

Update static pages after the site has been built without rebuilding the entire site.

**Example: Using `revalidate` in `getStaticProps`**

Refer to the SSG example above where `revalidate: 60` allows the page to be regenerated every 60 seconds.

### Image Optimization

Use Next.js's built-in Image component for automatic image optimization.

```javascript
// components/ArticleCard.js
import Image from "next/image";
import Link from "next/link";

export default function ArticleCard({ article }) {
  return (
    <div className="border rounded-lg overflow-hidden shadow-md">
      {article.featured_image && (
        <Image
          src={article.featured_image.data.attributes.url}
          alt={article.title}
          width={500}
          height={300}
          className="w-full h-48 object-cover"
        />
      )}
      <div className="p-4">
        <h2 className="text-xl font-semibold mb-2">{article.title}</h2>
        <p className="text-gray-600 mb-4">
          {article.content.substring(0, 100)}...
        </p>
        <Link href={`/articles/${article.id}`}>
          <a className="text-blue-500 hover:underline">Read More</a>
        </Link>
      </div>
    </div>
  );
}
```

**Note:** Ensure that the image domains are allowed in `next.config.js`.

```javascript
// next.config.js
module.exports = {
  images: {
    domains: ["your-strapi-backend-domain.com"],
  },
};
```

## Testing

### Unit Testing with Jest

Set up Jest for unit testing your components and utilities.

1. **Install Jest and Testing Libraries:**

   ```bash
   npm install --save-dev jest @testing-library/react @testing-library/jest-dom @testing-library/user-event babel-jest
   ```

2. **Configure Jest:**

   Create a `jest.config.js` file:

   ```javascript
   // jest.config.js
   module.exports = {
     testEnvironment: "jsdom",
     setupFilesAfterEnv: ["<rootDir>/jest.setup.js"],
     moduleNameMapper: {
       "\\.(css|less|scss|sass)$": "identity-obj-proxy",
     },
   };
   ```

3. **Set Up Testing Environment:**

   Create a `jest.setup.js` file:

   ```javascript
   // jest.setup.js
   import "@testing-library/jest-dom/extend-expect";
   ```

4. **Add Test Scripts:**

   Update `package.json`:

   ```json
   {
     "scripts": {
       "test": "jest",
       "test:watch": "jest --watch"
     }
   }
   ```

5. **Write Tests:**

   **Example: Testing the Button Component**

   ```javascript
   // components/__tests__/Button.test.js
   import { render, screen, fireEvent } from "@testing-library/react";
   import Button from "../Button";

   test("renders button with correct text", () => {
     render(<Button>Click Me</Button>);
     const buttonElement = screen.getByText(/Click Me/i);
     expect(buttonElement).toBeInTheDocument();
   });

   test("calls onClick handler when clicked", () => {
     const handleClick = jest.fn();
     render(<Button onClick={handleClick}>Click Me</Button>);
     const buttonElement = screen.getByText(/Click Me/i);
     fireEvent.click(buttonElement);
     expect(handleClick).toHaveBeenCalledTimes(1);
   });
   ```

### Integration Testing with React Testing Library

Test interactions between components and ensure they work together as expected.

**Example: Testing the Navbar Component**

```javascript
// components/__tests__/Navbar.test.js
import { render, screen } from "@testing-library/react";
import Navbar from "../Navbar";
import { ThemeProvider } from "../../context/ThemeContext";
import { Provider } from "react-redux";
import { store } from "../../store/store";

test("renders Navbar with site title", () => {
  render(
    <Provider store={store}>
      <ThemeProvider>
        <Navbar />
      </ThemeProvider>
    </Provider>
  );
  const titleElement = screen.getByText(/Next News/i);
  expect(titleElement).toBeInTheDocument();
});

test("renders navigation links", () => {
  render(
    <Provider store={store}>
      <ThemeProvider>
        <Navbar />
      </ThemeProvider>
    </Provider>
  );
  const aboutLink = screen.getByText(/About/i);
  expect(aboutLink).toBeInTheDocument();
});
```

### End-to-End Testing with Cypress

Automate user interactions and verify the entire application flow.

1. **Install Cypress:**

   ```bash
   npm install --save-dev cypress
   ```

2. **Initialize Cypress:**

   ```bash
   npx cypress open
   ```

3. **Write Tests:**

   **Example: Testing the Home Page**

   ```javascript
   // cypress/integration/home.spec.js
   describe("Home Page", () => {
     it("loads successfully", () => {
       cy.visit("/");
       cy.contains("Latest News").should("be.visible");
     });

     it("displays articles", () => {
       cy.visit("/");
       cy.get("div.grid").within(() => {
         cy.get("div.border").should("have.length.greaterThan", 0);
       });
     });

     it("navigates to an article page", () => {
       cy.visit("/");
       cy.get("a.text-blue-500").first().click();
       cy.url().should("include", "/articles/");
       cy.get("h1").should("be.visible");
     });
   });
   ```

4. **Run Cypress Tests:**

   ```bash
   npx cypress run
   ```

## Running the Development Server

Start the Next.js development server to begin working on your application.

```bash
npm run dev
# or
yarn dev
```

Navigate to `http://localhost:3000` in your browser to view the application.

## Building for Production

Prepare your application for deployment by creating an optimized production build.

```bash
npm run build
# or
yarn build
```

After building, start the production server:

```bash
npm start
# or
yarn start
```

## Deployment Considerations

For deploying **Next News**, refer to the [Deployment Guide](./Deployment_Guide.md) which provides detailed instructions on deploying both the frontend and backend to platforms like Vercel and Heroku.

## Troubleshooting

### Common Issues

- **Styles Not Applying:**

  - Ensure Tailwind CSS is correctly configured and imported.
  - Verify that Shadcn components are properly installed and imported.

- **API Calls Failing:**

  - Check if the Strapi backend is running and accessible.
  - Verify that `NEXT_PUBLIC_API_URL` is correctly set in `.env.local`.

- **Image Optimization Errors:**
  - Ensure image domains are allowed in `next.config.js`.
  - Verify that images are accessible and correctly referenced.

### Getting Help

If you encounter issues not covered in this guide:

- **Open an Issue:** Visit the [GitHub Issues](https://github.com/Aliio-Inc/strapi-next-news/issues) page to report the problem.
- **Next.js Documentation:** Refer to the [Next.js Documentation](https://nextjs.org/docs) for detailed guidance.
- **Shadcn Documentation:** Consult the [Shadcn UI Documentation](https://ui.shadcn.com/docs) for component-specific help.
- **Community Support:** Engage with the Next.js and Shadcn communities through forums and discussion boards.

## Additional Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Shadcn UI Documentation](https://ui.shadcn.com/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Strapi Documentation](https://strapi.io/documentation)
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [Axios Documentation](https://axios-http.com/docs/intro)
- [SWR Documentation](https://swr.vercel.app/)
- [Jest Documentation](https://jestjs.io/docs/getting-started)
- [Cypress Documentation](https://docs.cypress.io/guides/overview/why-cypress)

## Footer

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Clearly identifies the document as a setup guide for Next.js within the Next News project, outlining its purpose to configure a robust frontend that integrates with Strapi and Shadcn.

- **Table of Contents**: Provides an organized structure, allowing users to navigate easily through different sections such as installation, configuration, integration, testing, and troubleshooting.

- **Prerequisites**: Lists the essential tools and software required before starting the Next.js setup, ensuring users are adequately prepared.

- **Installation**:

  - **Install Node.js and npm**: Ensures users have the necessary runtime environment.
  - **Create a New Next.js Project**: Guides users through initializing a new Next.js application using `create-next-app`.
  - **Install Required Dependencies**: Details the installation of Shadcn and other essential libraries like `axios` and `swr` for API interactions and data fetching.
  - **Set Up Tailwind CSS**: Provides comprehensive steps to integrate Tailwind CSS, crucial for styling the application and working seamlessly with Shadcn.
  - **Install Shadcn UI Components**: Offers two methods for integrating Shadcn components—using the Shadcn CLI for streamlined installation or manually copying components from the repository.

- **Configuration**:

  - **Configure Tailwind CSS**: Explains how to extend Tailwind's theme and add plugins to support enhanced styling features.
  - **Configure Shadcn**: Guides on customizing Shadcn components by modifying Tailwind configurations.
  - **Environment Variables**: Emphasizes the importance of managing environment variables securely, providing an example `.env.local` file and highlighting security considerations.

- **Integrating with Strapi**:

  - **API Integration**: Demonstrates setting up API utilities using `axios` and `swr` for efficient data fetching from the Strapi backend.
  - **Fetching Data**: Provides examples of creating custom hooks to fetch and manage data, and how to display this data within components.

- **Creating Pages and Components**:

  - **Pages Directory**: Explains Next.js's file-based routing system with examples of creating static and dynamic pages.
  - **Components Directory**: Encourages building reusable components, providing examples like `ArticleCard` for displaying articles.

- **State Management**:

  - **Using React Context API**: Shows how to create and use a Theme Context for managing global state like theme settings.
  - **Optional: Integrate Redux or Zustand**: Suggests integrating more robust state management libraries for complex needs, with an example setup for Redux.

- **Routing and Navigation**:

  - **File-Based Routing**: Reiterates Next.js's routing mechanism with examples.
  - **Dynamic Routes**: Details handling dynamic content such as individual articles.
  - **Navigation Bar**: Guides on creating a reusable navigation bar component for consistent navigation across the application.

- **Styling and Theming**:

  - **Using Tailwind CSS**: Provides examples of styling components using Tailwind's utility classes.
  - **Custom Themes with Shadcn**: Explains how to customize Shadcn components by extending Tailwind's theme.

- **Performance Optimization**:

  - **Static Site Generation (SSG)**: Details using `getStaticProps` for pre-rendering pages at build time.
  - **Server-Side Rendering (SSR)**: Explains using `getServerSideProps` for rendering pages on each request.
  - **Incremental Static Regeneration (ISR)**: Discusses using ISR to update static pages without full rebuilds.
  - **Image Optimization**: Demonstrates using Next.js's Image component for automatic image optimization and configuring allowed image domains.

- **Testing**:

  - **Unit Testing with Jest**: Guides setting up Jest for unit testing components and utilities, with examples.
  - **Integration Testing with React Testing Library**: Shows how to test interactions between components.
  - **End-to-End Testing with Cypress**: Provides steps to set up Cypress for automated user flow testing.

- **Running the Development Server**: Provides commands to start the Next.js development server.

- **Building for Production**: Explains how to create an optimized production build and start the production server.

- **Deployment Considerations**: Directs users to the Deployment Guide for detailed instructions on deploying the frontend and backend.

- **Troubleshooting**:

  - **Common Issues**: Identifies frequent problems such as styling issues, API call failures, and image optimization errors, offering potential solutions.
  - **Getting Help**: Encourages users to seek assistance through GitHub Issues, official documentation, and community support channels.

- **Additional Resources**: Lists relevant documentation and resources for Next.js, Shadcn, Tailwind CSS, Strapi, and testing libraries to aid further learning and troubleshooting.

- **Footer**: Includes essential project information, author details, website link, and contact information, ensuring users have access to support and additional resources.

Overall, the **Nextjs_Setup.md** file serves as a comprehensive and detailed guide for setting up Next.js as the frontend framework for the Next News project. It covers all necessary steps from installation to customization, emphasizes best practices, and provides solutions to common issues. This ensures that developers can configure and maintain a high-quality, performant, and user-friendly frontend application.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

Feel free to customize this Next.js setup guide to better fit the specific needs of your project. If you have any questions or need further assistance, don't hesitate to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out to the maintainers.
