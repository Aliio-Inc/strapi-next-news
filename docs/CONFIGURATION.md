# Configuration Guide for Next News

This guide provides detailed instructions on configuring **Next News** to suit your development and production environments. It covers both frontend and backend configurations, environment variables, and other essential settings.

## Table of Contents

- [Environment Variables](#environment-variables)
  - [Frontend Environment Variables](#frontend-environment-variables)
  - [Backend Environment Variables](#backend-environment-variables)
- [Strapi Configuration](#strapi-configuration)
  - [Content Types](#content-types)
  - [Plugins](#plugins)
  - [Roles & Permissions](#roles--permissions)
  - [CORS Settings](#cors-settings)
- [Next.js Configuration](#nextjs-configuration)
  - [Pages and Routing](#pages-and-routing)
  - [API Routes](#api-routes)
  - [Styling with Shadcn](#styling-with-shadcn)
  - [Internationalization](#internationalization)
- [Database Configuration](#database-configuration)
- [Advanced Configurations](#advanced-configurations)
  - [Custom Middleware](#custom-middleware)
  - [Logging](#logging)
- [Security Best Practices](#security-best-practices)
- [Environment-Specific Settings](#environment-specific-settings)
- [Troubleshooting Configuration Issues](#troubleshooting-configuration-issues)

## Environment Variables

Proper configuration using environment variables ensures that sensitive information is not hard-coded into the application and allows for flexibility across different environments (development, staging, production).

### Frontend Environment Variables

Located in `frontend/.env`, these variables configure the frontend application.

```env
# API endpoint for Strapi backend
NEXT_PUBLIC_API_URL=http://localhost:1337

# Other frontend-specific environment variables
NEXT_PUBLIC_SITE_TITLE=Next News
NEXT_PUBLIC_SITE_DESCRIPTION=A modern news portal built with Strapi and Next.js
```

**Description of Variables:**

- `NEXT_PUBLIC_API_URL`: The base URL for the Strapi backend API. Ensure this points to the correct backend server.
- `NEXT_PUBLIC_SITE_TITLE`: The title of your news portal.
- `NEXT_PUBLIC_SITE_DESCRIPTION`: A brief description of your site for SEO purposes.

### Backend Environment Variables

Located in `backend/.env`, these variables configure the backend Strapi application.

```env
# Database configuration
DATABASE_URL=postgres://user:password@localhost:5432/next_news

# Strapi Admin credentials
ADMIN_JWT_SECRET=your_admin_jwt_secret
JWT_SECRET=your_jwt_secret

# Email settings (optional)
EMAIL_PROVIDER=smtp
EMAIL_SMTP_HOST=smtp.example.com
EMAIL_SMTP_PORT=587
EMAIL_SMTP_USERNAME=your_username
EMAIL_SMTP_PASSWORD=your_password
```

**Description of Variables:**

- `DATABASE_URL`: Connection string for your PostgreSQL or MongoDB database.
- `ADMIN_JWT_SECRET`: Secret key for admin authentication tokens.
- `JWT_SECRET`: Secret key for user authentication tokens.
- Email settings: Configure if you plan to use email functionalities like user registration confirmation.

## Strapi Configuration

### Content Types

Define the content structures that **Next News** will manage. Common content types include:

- **Article**: Fields like title, content, author, category, published date, etc.
- **Category**: Name and description.
- **Author**: Name, bio, profile picture, etc.

**Steps to Create Content Types:**

1. Navigate to the Strapi admin panel at [http://localhost:1337/admin](http://localhost:1337/admin).
2. Go to **Content-Types Builder**.
3. Create a new content type and add the necessary fields.

### Plugins

Strapi offers various plugins to extend functionality. Consider configuring the following:

- **Users & Permissions**: Manage user roles and access levels.
- **Email**: Set up email providers for notifications and user communications.
- **Media**: Manage and serve media assets like images and videos.

**Installing Plugins:**

```bash
# Example: Installing the email plugin
cd backend
npm install @strapi/plugin-email
# or
yarn add @strapi/plugin-email
```

After installation, enable and configure the plugin via the Strapi admin panel.

### Roles & Permissions

Configure roles to control access to different parts of the API and admin panel.

**Steps:**

1. In the Strapi admin panel, go to **Settings > Users & Permissions > Roles**.
2. Edit existing roles or create new ones as needed.
3. Assign permissions to content types and API endpoints based on role requirements.

### CORS Settings

Ensure that the frontend can communicate with the backend by configuring Cross-Origin Resource Sharing (CORS).

**Configuration File:**

Located in `backend/config/middlewares.js` or `backend/config/server.js` depending on Strapi version.

```javascript
module.exports = ({ env }) => ({
  // ...
  settings: {
    cors: {
      enabled: true,
      origin: ["http://localhost:3000", "https://your-production-domain.com"],
    },
  },
});
```

**Explanation:**

- `origin`: List of allowed origins. Update this with your frontend's URL.

## Next.js Configuration

### Pages and Routing

Customize the routing structure by modifying the files in the `frontend/pages` directory.

**Dynamic Routes:**

Use dynamic routing to handle pages like individual articles or categories.

```javascript
// Example: pages/articles/[slug].js
import { useRouter } from "next/router";

const Article = () => {
  const router = useRouter();
  const { slug } = router.query;

  // Fetch and display article based on slug
};

export default Article;
```

### API Routes

Next.js allows creating API routes within the `pages/api` directory for server-side operations.

**Example:**

```javascript
// pages/api/subscribe.js
export default function handler(req, res) {
  if (req.method === "POST") {
    // Handle subscription logic
    res.status(200).json({ message: "Subscribed successfully!" });
  } else {
    res.status(405).json({ message: "Method Not Allowed" });
  }
}
```

### Styling with Shadcn

Shadcn provides pre-built UI components. Customize the styling as needed.

**Configuration:**

1. Install Shadcn:

   ```bash
   cd frontend
   npm install @shadcn/ui
   # or
   yarn add @shadcn/ui
   ```

2. Import and use components in your React components.

   ```javascript
   import { Button } from "@shadcn/ui";

   const HomePage = () => <Button variant="primary">Click Me</Button>;

   export default HomePage;
   ```

### Internationalization

If you plan to support multiple languages, configure Next.js internationalization.

**Configuration:**

Edit `next.config.js`:

```javascript
module.exports = {
  i18n: {
    locales: ["en", "es", "fr"],
    defaultLocale: "en",
  },
  // Other Next.js configurations
};
```

**Usage:**

Use `next-translate` or similar libraries to manage translations.

## Database Configuration

Depending on your choice between PostgreSQL and MongoDB, ensure the database is correctly set up and the connection string in `backend/.env` is accurate.

**PostgreSQL:**

- Ensure the database is running.
- Verify the `DATABASE_URL` includes the correct username, password, host, port, and database name.

**MongoDB:**

- Ensure the MongoDB service is running.
- Verify the `DATABASE_URL` includes the correct username, password, host, port, and database name.

## Advanced Configurations

### Custom Middleware

Add custom middleware for tasks like logging, request validation, or authentication.

**Example:**

Create a new middleware in `backend/middlewares/logger.js`:

```javascript
module.exports = (config, { strapi }) => {
  return async (ctx, next) => {
    console.log(`${ctx.method} ${ctx.url}`);
    await next();
  };
};
```

Register the middleware in `backend/config/middlewares.js`:

```javascript
module.exports = [
  // Existing middlewares
  "strapi::cors",
  "strapi::security",
  // Add custom middleware
  {
    name: "logger",
    config: {},
  },
];
```

### Logging

Configure logging to monitor application behavior.

**Configuration File:**

Located in `backend/config/logger.js`:

```javascript
module.exports = ({ env }) => ({
  level: env("LOG_LEVEL", "info"),
  // Other logging options
});
```

## Security Best Practices

- **Environment Variables**: Never commit `.env` files to version control.
- **Update Dependencies**: Regularly update dependencies to patch known vulnerabilities.
- **Use HTTPS**: Ensure all communications are over HTTPS in production.
- **Access Controls**: Properly configure user roles and permissions in Strapi.

## Environment-Specific Settings

Configure settings that differ between development, staging, and production environments.

**Example:**

Create separate configuration files for each environment in `backend/config/env/production/server.js` and `backend/config/env/development/server.js`.

```javascript
// backend/config/env/production/server.js
module.exports = ({ env }) => ({
  host: env("HOST", "0.0.0.0"),
  port: env.int("PORT", 1337),
  url: env("PRODUCTION_URL", "https://your-production-domain.com"),
  // Other production-specific settings
});
```

## Troubleshooting Configuration Issues

If you encounter issues related to configuration:

- **Check Environment Variables**: Ensure all required variables are set and correctly formatted.
- **Review Logs**: Look at Strapi and Next.js logs for error messages.
- **Validate Configuration Files**: Ensure no syntax errors exist in configuration files.
- **Consult Documentation**: Refer to [Strapi Documentation](https://strapi.io/documentation) and [Next.js Documentation](https://nextjs.org/docs) for detailed configuration options.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Clearly states the purpose of the document and what the user will achieve by following it.
- **Table of Contents**: Helps users navigate through the various sections of the configuration guide.

- **Environment Variables**: Details the necessary environment variables for both frontend and backend, including descriptions and examples to ensure proper setup.

- **Strapi Configuration**: Provides instructions on setting up content types, plugins, roles & permissions, and CORS settings within Strapi to tailor the backend to your project's needs.

- **Next.js Configuration**: Covers customization of pages and routing, creation of API routes, styling with Shadcn, and setting up internationalization for multilingual support.

- **Database Configuration**: Guides users through configuring their chosen database (PostgreSQL or MongoDB) to ensure seamless backend operations.

- **Advanced Configurations**: Introduces more sophisticated setups like custom middleware and logging to enhance application functionality and monitoring.

- **Security Best Practices**: Offers essential tips to maintain the security and integrity of the application, emphasizing the importance of environment variables, dependency management, HTTPS, and access controls.

- **Environment-Specific Settings**: Explains how to handle different configurations for various environments (development, staging, production) to maintain consistency and reliability.

- **Troubleshooting Configuration Issues**: Provides solutions to common configuration-related problems, ensuring users can resolve issues efficiently.

- **Footer**: Includes project information, author details, website link, and contact information for further assistance.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

Feel free to customize this configuration guide to better fit the specific needs of your project. If you have any questions or need further assistance, don't hesitate to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out to the maintainers.
