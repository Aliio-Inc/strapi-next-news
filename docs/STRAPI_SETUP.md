# Strapi Setup Guide for Next News

This guide provides step-by-step instructions to set up **Strapi** as the backend CMS for **Next News**. By following these steps, you'll be able to install Strapi, configure it with your preferred database, define content types, manage roles and permissions, and prepare the backend for development and production environments.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [1. Install Node.js and npm](#1-install-nodejs-and-npm)
  - [2. Install Strapi CLI](#2-install-strapi-cli)
  - [3. Create a New Strapi Project](#3-create-a-new-strapi-project)
- [Configuration](#configuration)
  - [1. Database Configuration](#1-database-configuration)
    - [PostgreSQL Setup](#postgresql-setup)
    - [MongoDB Setup](#mongodb-setup)
  - [2. Environment Variables](#2-environment-variables)
- [Defining Content Types](#defining-content-types)
  - [1. Article](#1-article)
  - [2. Category](#2-category)
  - [3. Author](#3-author)
- [Roles & Permissions](#roles--permissions)
  - [1. Default Roles](#1-default-roles)
  - [2. Creating Custom Roles](#2-creating-custom-roles)
- [Media Library Configuration](#media-library-configuration)
- [Extending Strapi](#extending-strapi)
  - [1. Installing Plugins](#1-installing-plugins)
  - [2. Custom Controllers and Routes](#2-custom-controllers-and-routes)
- [Running Strapi](#running-strapi)
  - [Development Mode](#development-mode)
  - [Production Mode](#production-mode)
- [Testing the Setup](#testing-the-setup)
- [Troubleshooting](#troubleshooting)
- [Additional Resources](#additional-resources)
- [Footer](#footer)

## Prerequisites

Before setting up Strapi for **Next News**, ensure you have the following:

- **Node.js** (v14 or later)
- **npm** (comes with Node.js) or **Yarn**
- **Git** (optional, for version control)
- **Database**: PostgreSQL or MongoDB installed and running

## Installation

### 1. Install Node.js and npm

If you haven't installed Node.js and npm yet, download and install them from the [official Node.js website](https://nodejs.org/).

Verify the installation:

```bash
node -v
npm -v
```

### 2. Install Strapi CLI

Install the Strapi Command Line Interface globally using npm or Yarn:

```bash
# Using npm
npm install -g create-strapi-app

# Using Yarn
yarn global add create-strapi-app
```

### 3. Create a New Strapi Project

Navigate to your desired directory and create a new Strapi project:

```bash
# Using npm
npx create-strapi-app@latest next-news-backend --quickstart

# Using Yarn
yarn create strapi-app next-news-backend --quickstart
```

**Note:** The `--quickstart` flag sets up Strapi with SQLite by default. To use PostgreSQL or MongoDB, omit the `--quickstart` flag and follow the prompts.

## Configuration

### 1. Database Configuration

Configure Strapi to use your preferred database (PostgreSQL or MongoDB).

#### PostgreSQL Setup

1. **Install PostgreSQL** if not already installed. Refer to the [official installation guide](https://www.postgresql.org/download/) for your operating system.

2. **Create a Database and User:**

   ```bash
   # Access PostgreSQL prompt
   psql -U postgres

   # Create a new database
   CREATE DATABASE next_news;

   # Create a new user with password
   CREATE USER next_user WITH PASSWORD 'securePassword';

   # Grant all privileges on the database to the user
   GRANT ALL PRIVILEGES ON DATABASE next_news TO next_user;

   # Exit the prompt
   \q
   ```

3. **Configure Strapi to Use PostgreSQL:**

   During project creation, select PostgreSQL as your database. If you used the `--quickstart` flag, you'll need to reconfigure.

   Update `config/database.js`:

   ```javascript
   // config/database.js
   module.exports = ({ env }) => ({
     connection: {
       client: "postgres",
       connection: {
         host: env("DATABASE_HOST", "127.0.0.1"),
         port: env.int("DATABASE_PORT", 5432),
         database: env("DATABASE_NAME", "next_news"),
         user: env("DATABASE_USERNAME", "next_user"),
         password: env("DATABASE_PASSWORD", "securePassword"),
         ssl: env.bool("DATABASE_SSL", false),
       },
       debug: false,
     },
   });
   ```

#### MongoDB Setup

1. **Install MongoDB** if not already installed. Refer to the [official installation guide](https://www.mongodb.com/docs/manual/installation/) for your operating system.

2. **Create a Database and User:**

   ```bash
   # Access MongoDB shell
   mongo

   # Switch to admin database
   use admin

   # Create a new user
   db.createUser({
     user: "next_user",
     pwd: "securePassword",
     roles: [{ role: "readWrite", db: "next_news" }]
   });

   # Exit the shell
   exit
   ```

3. **Configure Strapi to Use MongoDB:**

   During project creation, select MongoDB as your database. If you used the `--quickstart` flag, you'll need to reconfigure.

   Update `config/database.js`:

   ```javascript
   // config/database.js
   module.exports = ({ env }) => ({
     connection: {
       client: "mongo",
       connection: {
         uri: env(
           "DATABASE_URI",
           "mongodb://next_user:securePassword@localhost:27017/next_news"
         ),
         options: {
           ssl: env.bool("DATABASE_SSL", false),
         },
       },
       debug: false,
     },
   });
   ```

### 2. Environment Variables

Manage sensitive information using environment variables. Create a `.env` file in the root of your Strapi project.

```env
# .env
DATABASE_HOST=127.0.0.1
DATABASE_PORT=5432
DATABASE_NAME=next_news
DATABASE_USERNAME=next_user
DATABASE_PASSWORD=securePassword
DATABASE_SSL=false

ADMIN_JWT_SECRET=your_admin_jwt_secret
JWT_SECRET=your_jwt_secret

# Optional: Email configurations
EMAIL_PROVIDER=smtp
EMAIL_SMTP_HOST=smtp.example.com
EMAIL_SMTP_PORT=587
EMAIL_SMTP_USERNAME=your_username
EMAIL_SMTP_PASSWORD=your_password
```

**Security Note:** Never commit `.env` files to version control. Add `.env` to your `.gitignore`.

## Defining Content Types

Define the content structures that **Next News** will manage, such as Articles, Categories, and Authors.

### 1. Article

1. **Navigate to Content-Types Builder:**

   Open your browser and go to `http://localhost:1337/admin`. Log in with your admin credentials and navigate to **Content-Types Builder**.

2. **Create Article Collection Type:**

   - Click **"Create new collection type"**.
   - Name it **Article**.

3. **Add Fields:**

   - **Title**: Text (required)
   - **Content**: Rich Text (required)
   - **Published At**: Date (required)
   - **Author**: Relation (Many-to-One with Author)
   - **Category**: Relation (Many-to-One with Category)
   - **Featured Image**: Media (Single media)

4. **Save and Apply:**

   Click **"Save"** and allow Strapi to restart to apply changes.

### 2. Category

1. **Create Category Collection Type:**

   - In **Content-Types Builder**, click **"Create new collection type"**.
   - Name it **Category**.

2. **Add Fields:**

   - **Name**: Text (required)
   - **Description**: Rich Text
   - **Parent Category**: Relation (One-to-Many with Category) _(optional for nested categories)_

3. **Save and Apply:**

   Click **"Save"** and allow Strapi to restart.

### 3. Author

1. **Create Author Collection Type:**

   - In **Content-Types Builder**, click **"Create new collection type"**.
   - Name it **Author**.

2. **Add Fields:**

   - **Name**: Text (required)
   - **Bio**: Rich Text
   - **Profile Picture**: Media (Single media)
   - **Email**: Email (required, unique)
   - **Password**: Password (required) _(if authors can log in)_

3. **Save and Apply:**

   Click **"Save"** and allow Strapi to restart.

## Roles & Permissions

Configure user roles to control access to different parts of the API and admin panel.

### 1. Default Roles

Strapi provides three default roles:

- **Authenticated**: Users who are logged in.
- **Public**: Users who are not logged in.
- **Administrator**: Users with full access to Strapi's admin panel.

### 2. Creating Custom Roles

1. **Navigate to Roles & Permissions:**

   In the Strapi admin panel, go to **Settings** > **Users & Permissions Plugin** > **Roles**.

2. **Create a New Role:**

   - Click **"Add New Role"**.
   - Name it (e.g., **Editor**, **Contributor**).

3. **Set Permissions:**

   - Define what each role can do by selecting the appropriate permissions for each content type and action.
   - For example, an **Editor** might have permissions to create, read, update, and delete articles, whereas a **Contributor** might only have permissions to create and read.

4. **Save Changes:**

   Click **"Save"** to apply the new role.

## Media Library Configuration

Manage media assets like images and videos within Strapi.

1. **Access Media Library:**

   In the admin panel, navigate to **Media Library**.

2. **Upload Media:**

   - Click **"Upload"** to add new media files.
   - Organize media into folders as needed.

3. **Configure Providers:**

   For production environments, consider using cloud storage providers like AWS S3, Cloudinary, or others.

   - Install the provider plugin:

     ```bash
     npm install @strapi/provider-upload-aws-s3
     ```

   - Configure the provider in `config/plugins.js`:

     ```javascript
     // config/plugins.js
     module.exports = ({ env }) => ({
       upload: {
         provider: "aws-s3",
         providerOptions: {
           accessKeyId: env("AWS_ACCESS_KEY_ID"),
           secretAccessKey: env("AWS_ACCESS_SECRET"),
           region: env("AWS_REGION"),
           params: {
             Bucket: env("AWS_BUCKET"),
           },
         },
       },
     });
     ```

   - Update `.env` with AWS credentials:

     ```env
     AWS_ACCESS_KEY_ID=your_access_key_id
     AWS_ACCESS_SECRET=your_access_secret
     AWS_REGION=your_region
     AWS_BUCKET=your_bucket_name
     ```

## Extending Strapi

### 1. Installing Plugins

Enhance Strapi's functionality by installing plugins.

- **GraphQL Plugin:**

  ```bash
  npm install @strapi/plugin-graphql
  ```

  Configure the plugin in `config/plugins.js`:

  ```javascript
  // config/plugins.js
  module.exports = ({ env }) => ({
    graphql: {
      enabled: true,
      config: {
        endpoint: "/graphql",
        shadowCRUD: true,
        playgroundAlways: false,
        depthLimit: 7,
        amountLimit: 100,
      },
    },
  });
  ```

- **Email Plugin:**

  ```bash
  npm install @strapi/plugin-email
  ```

  Configure as per the [Email Plugin Documentation](https://docs.strapi.io/developer-docs/latest/plugins/email.html).

### 2. Custom Controllers and Routes

Customize API behavior by creating custom controllers and routes.

1. **Create a Custom Controller:**

   ```javascript
   // src/api/article/controllers/custom-article.js
   const { createCoreController } = require("@strapi/strapi").factories;

   module.exports = createCoreController(
     "api::article.article",
     ({ strapi }) => ({
       async customAction(ctx) {
         // Custom logic here
         ctx.send({ message: "This is a custom action!" });
       },
     })
   );
   ```

2. **Define a Custom Route:**

   ```javascript
   // src/api/article/routes/custom-article.js
   module.exports = {
     routes: [
       {
         method: "GET",
         path: "/articles/custom-action",
         handler: "custom-article.customAction",
         config: {
           policies: [],
         },
       },
     ],
   };
   ```

3. **Register the Custom Route:**

   Ensure the custom route is registered in the main routes file or use the Strapi CLI to automate.

## Running Strapi

### Development Mode

Start Strapi in development mode with hot-reloading:

```bash
# From the project root
npm run develop
# or
yarn develop
```

Strapi will be accessible at `http://localhost:1337/admin`.

### Production Mode

Build and start Strapi in production mode:

1. **Build the Admin Panel:**

   ```bash
   npm run build
   # or
   yarn build
   ```

2. **Start Strapi:**

   ```bash
   npm start
   # or
   yarn start
   ```

Ensure environment variables are correctly set in the production environment.

## Testing the Setup

1. **Access the Admin Panel:**

   Navigate to `http://localhost:1337/admin` and log in with your admin credentials.

2. **Create Sample Content:**

   - Add categories, authors, and articles to verify that content types are working correctly.
   - Upload media files to test the media library.

3. **API Testing:**

   Use tools like [Postman](https://www.postman.com/) or [Insomnia](https://insomnia.rest/) to test API endpoints.

   - **Example:** Fetch all articles via API.

     ```bash
     curl -X GET "http://localhost:1337/api/articles?populate=*"
     ```

## Troubleshooting

### Common Issues

- **Database Connection Errors:**

  - Ensure the database server is running.
  - Verify the `DATABASE_*` environment variables are correct.

- **Admin Panel Not Accessible:**

  - Check if Strapi is running without errors.
  - Verify that the server is listening on the correct port.

- **Media Upload Failures:**
  - Ensure the media provider is correctly configured.
  - Check file size limits and permissions.

### Getting Help

If you encounter issues not covered in this guide:

- **Open an Issue:** Visit the [GitHub Issues](https://github.com/Aliio-Inc/strapi-next-news/issues) page to report the problem.
- **Strapi Documentation:** Refer to the [Strapi Documentation](https://docs.strapi.io/developer-docs/latest/getting-started/introduction.html) for detailed guidance.
- **Community Support:** Engage with the Strapi community through forums and discussion boards.

## Additional Resources

- [Strapi Official Documentation](https://docs.strapi.io/)
- [Strapi GitHub Repository](https://github.com/strapi/strapi)
- [Strapi Plugins](https://docs.strapi.io/developer-docs/latest/plugins/introduction.html)
- [GraphQL Integration](https://docs.strapi.io/developer-docs/latest/plugins/graphql.html)
- [Email Plugin Documentation](https://docs.strapi.io/developer-docs/latest/plugins/email.html)
- [Strapi Tutorials](https://strapi.io/documentation/developer-docs/latest/getting-started/tutorials.html)

## Footer

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Clearly identifies the document as a setup guide for Strapi within the Next News project, outlining the purpose and scope.

- **Table of Contents**: Organized list of sections to facilitate easy navigation through different aspects of the Strapi setup process.

- **Prerequisites**: Lists essential tools and software required before starting the setup, ensuring that users are adequately prepared.

- **Installation**:

  - **Install Node.js and npm**: Ensures users have the necessary runtime environment.
  - **Install Strapi CLI**: Guides on installing the Strapi Command Line Interface for project creation.
  - **Create a New Strapi Project**: Provides commands to initialize a new Strapi project, with options for different database setups.

- **Configuration**:

  - **Database Configuration**: Detailed instructions for setting up either PostgreSQL or MongoDB, including creating databases and configuring connection settings in Strapi.
  - **Environment Variables**: Explains how to manage sensitive information using environment variables, with an example `.env` file and security notes.

- **Defining Content Types**:

  - **Article, Category, Author**: Step-by-step guide on creating and configuring essential content types within Strapi, including defining fields and setting up relationships.

- **Roles & Permissions**:

  - **Default Roles**: Overview of Strapi’s built-in roles.
  - **Creating Custom Roles**: Instructions for creating and configuring custom user roles to control access and permissions.

- **Media Library Configuration**: Guides on managing media assets within Strapi, including configuring cloud storage providers for production environments.

- **Extending Strapi**:

  - **Installing Plugins**: Instructions for adding plugins like GraphQL and Email to enhance Strapi’s functionality.
  - **Custom Controllers and Routes**: Demonstrates how to extend Strapi with custom logic, enabling tailored API behavior.

- **Running Strapi**:

  - **Development Mode**: Commands to start Strapi in development with hot-reloading.
  - **Production Mode**: Steps to build and run Strapi in a production environment, emphasizing the importance of environment variables.

- **Testing the Setup**: Provides methods to verify that Strapi is correctly set up by creating sample content and testing API endpoints using tools like Postman or cURL.

- **Troubleshooting**:

  - **Common Issues**: Identifies frequent problems such as database connection errors, inaccessible admin panels, and media upload failures, offering potential solutions.
  - **Getting Help**: Directs users to resources like GitHub Issues, Strapi Documentation, and community support channels for additional assistance.

- **Additional Resources**: Lists relevant documentation, repositories, and tutorials for further learning and reference, supporting users in deepening their understanding of Strapi.

- **Footer**: Provides essential project information, including links to the GitHub repository, author details, website, and contact information, ensuring users have access to support and additional resources.

Overall, the **Strapi_Setup.md** file serves as a comprehensive and detailed guide for setting up Strapi as the backend CMS for the Next News project. It covers all necessary steps from installation to customization, emphasizing best practices and providing solutions to common issues. This ensures that developers can set up and configure Strapi efficiently, enabling them to manage content effectively and maintain a robust backend infrastructure.
