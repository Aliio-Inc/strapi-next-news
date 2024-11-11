# Installation Guide for Next News

This guide provides step-by-step instructions to install and set up **Next News** on your local machine. Follow the steps below to get started with development or to run the project locally.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Clone the Repository](#clone-the-repository)
- [Install Dependencies](#install-dependencies)
  - [Frontend Dependencies](#frontend-dependencies)
  - [Backend Dependencies](#backend-dependencies)
- [Configure Environment Variables](#configure-environment-variables)
  - [Frontend Configuration](#frontend-configuration)
  - [Backend Configuration](#backend-configuration)
- [Set Up the Database](#set-up-the-database)
- [Initialize Strapi Backend](#initialize-strapi-backend)
- [Start the Next.js Frontend](#start-the-nextjs-frontend)
- [Verify the Installation](#verify-the-installation)
- [Troubleshooting](#troubleshooting)

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

- **Node.js** (v14 or later): [Download Node.js](https://nodejs.org/)
- **npm** or **Yarn**: Comes with Node.js, but you can install Yarn separately if preferred.
- **Git**: [Download Git](https://git-scm.com/downloads)
- **Database**: PostgreSQL or MongoDB, depending on your preference.
- **Strapi Account** _(optional for deployment)_: [Sign Up for Strapi](https://strapi.io/)

## Clone the Repository

Start by cloning the **Next News** repository to your local machine:

```bash
git clone https://github.com/Aliio-Inc/strapi-next-news.git
cd strapi-next-news
```

## Install Dependencies

**Next News** consists of two main parts: the **frontend** (built with Next.js) and the **backend** (powered by Strapi). Install dependencies for both.

### Frontend Dependencies

Navigate to the `frontend` directory and install the necessary packages:

```bash
cd frontend
npm install
# or
yarn install
```

### Backend Dependencies

Next, navigate to the `backend` directory and install the backend dependencies:

```bash
cd ../backend
npm install
# or
yarn install
```

## Configure Environment Variables

Environment variables are essential for configuring your application. Create `.env` files in both the `frontend` and `backend` directories based on the provided `.env.example` files.

### Frontend Configuration

1. Navigate to the `frontend` directory:

   ```bash
   cd ../frontend
   ```

2. Create a `.env` file:

   ```bash
   cp .env.example .env
   ```

3. Open the `.env` file in your preferred text editor and configure the variables:

   ```env
   NEXT_PUBLIC_API_URL=http://localhost:1337
   # Add other frontend-specific environment variables here
   ```

   **Note:** Replace `http://localhost:1337` with your Strapi backend URL if it's different.

### Backend Configuration

1. Navigate to the `backend` directory:

   ```bash
   cd ../backend
   ```

2. Create a `.env` file:

   ```bash
   cp .env.example .env
   ```

3. Open the `.env` file in your preferred text editor and configure the variables:

   ```env
   DATABASE_URL=postgres://user:password@localhost:5432/next_news
   # Add other backend-specific environment variables here
   ```

   **Note:** Replace `user`, `password`, and other placeholders with your actual database credentials.

## Set Up the Database

Ensure your chosen database (PostgreSQL or MongoDB) is installed and running. Create a new database for **Next News**.

### PostgreSQL Example

1. **Access PostgreSQL Prompt**:

   ```bash
   psql -U your_username
   ```

2. **Create a New Database**:

   ```sql
   CREATE DATABASE next_news;
   ```

3. **Exit the Prompt**:

   ```sql
   \q
   ```

### MongoDB Example

1. **Start MongoDB Service**:

   ```bash
   sudo service mongod start
   ```

2. **Create a New Database**:

   MongoDB will automatically create the database when you first store data in it.

## Initialize Strapi Backend

1. **Navigate to the Backend Directory**:

   ```bash
   cd backend
   ```

2. **Start the Strapi Development Server**:

   ```bash
   npm run develop
   # or
   yarn develop
   ```

   Strapi will be available at [http://localhost:1337](http://localhost:1337). Access the Strapi admin panel to manage content types, users, and settings.

   - **Admin Panel Setup**: On first run, you'll be prompted to create an admin user. Follow the on-screen instructions to set up your admin account.

## Start the Next.js Frontend

1. **Open a New Terminal Window** and navigate to the `frontend` directory:

   ```bash
   cd frontend
   ```

2. **Start the Next.js Development Server**:

   ```bash
   npm run dev
   # or
   yarn dev
   ```

   The Next.js application will be available at [http://localhost:3000](http://localhost:3000).

## Verify the Installation

1. **Access the Frontend**: Open your browser and navigate to [http://localhost:3000](http://localhost:3000). You should see the **Next News** homepage displaying the latest news articles.

2. **Access the Backend**: Navigate to [http://localhost:1337/admin](http://localhost:1337/admin) to access the Strapi admin panel. Log in with the admin credentials you created earlier.

3. **Create Content**:

   - **Define Content Types**: In the Strapi admin panel, define content types such as Articles, Categories, Authors, etc.
   - **Add Content**: Start adding news articles, categories, and other relevant content.

4. **Verify Data Flow**: Ensure that the content you create in Strapi is reflected on the frontend application.

## Troubleshooting

If you encounter any issues during the installation process, refer to the [Troubleshooting](./Troubleshooting.md) guide or open an issue on the [GitHub Issues](https://github.com/Aliio-Inc/strapi-next-news/issues) page.

### Common Issues

- **Backend Not Starting**:

  - Ensure the database is running and the `DATABASE_URL` in `backend/.env` is correct.
  - Check for missing dependencies and reinstall if necessary.

- **Frontend Not Connecting to Backend**:

  - Verify that `NEXT_PUBLIC_API_URL` in `frontend/.env` points to the correct Strapi backend URL.
  - Ensure the Strapi server is running.

- **CORS Errors**:
  - Configure CORS settings in Strapi to allow requests from your frontend URL.

## Additional Resources

- [Strapi Documentation](https://strapi.io/documentation/developer-docs/latest/getting-started/introduction.html)
- [Next.js Documentation](https://nextjs.org/docs)
- [Shadcn Documentation](https://shadcn.com/docs)

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Clearly states the purpose of the document and what the user will achieve by following it.
- **Prerequisites**: Lists all necessary tools and software required before installation.
- **Clone the Repository**: Provides commands to clone the project repository from GitHub.
- **Install Dependencies**: Guides users through installing necessary packages for both the frontend and backend.
- **Configure Environment Variables**: Instructions on setting up `.env` files for both frontend and backend, including placeholders for sensitive information.
- **Set Up the Database**: Details on setting up either PostgreSQL or MongoDB, depending on user preference.
- **Initialize Strapi Backend**: Steps to start the Strapi server and access the admin panel.
- **Start the Next.js Frontend**: Instructions to start the frontend development server.
- **Verify the Installation**: Steps to ensure that both frontend and backend are running correctly and communicating as expected.
- **Troubleshooting**: Common issues users might encounter during installation with brief solutions.
- **Additional Resources**: Links to official documentation for Strapi, Next.js, and Shadcn for further assistance.
- **Footer**: Includes project information and contact details for further assistance.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

Feel free to customize this installation guide to better fit the specific needs of your project. If you have any questions or need further assistance, don't hesitate to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out to the maintainers.
