# Deployment Guide for Next News

Deploying **Next News** to a production environment involves setting up both the frontend and backend applications, configuring environment variables, and ensuring security and scalability. This guide provides step-by-step instructions to help you deploy Next News efficiently.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Frontend Deployment](#frontend-deployment)
  - [Deploying to Vercel](#deploying-to-vercel)
  - [Environment Variables](#environment-variables)
  - [Custom Domain Setup](#custom-domain-setup)
- [Backend Deployment](#backend-deployment)
  - [Deploying to Heroku](#deploying-to-heroku)
  - [Environment Variables](#environment-variables-1)
  - [Database Setup](#database-setup)
  - [Custom Domain and SSL](#custom-domain-and-ssl)
- [CI/CD Pipeline](#cicd-pipeline)
  - [Setting Up GitHub Actions](#setting-up-github-actions)
- [Security Considerations](#security-considerations)
  - [HTTPS Enforcement](#https-enforcement)
  - [Environment Variables Management](#environment-variables-management)
  - [Access Controls](#access-controls)
- [Scalability and Performance](#scalability-and-performance)
  - [Scaling Backend Services](#scaling-backend-services)
  - [Optimizing Frontend Performance](#optimizing-frontend-performance)
- [Monitoring and Logging](#monitoring-and-logging)
  - [Monitoring Tools](#monitoring-tools)
  - [Logging Setup](#logging-setup)
- [Troubleshooting Deployment Issues](#troubleshooting-deployment-issues)
- [Additional Resources](#additional-resources)

## Prerequisites

Before deploying **Next News**, ensure you have the following:

- **GitHub Repository**: Ensure your project is pushed to GitHub.
- **Vercel Account**: [Sign Up for Vercel](https://vercel.com/signup)
- **Heroku Account**: [Sign Up for Heroku](https://signup.heroku.com/)
- **Database Service**: PostgreSQL (e.g., Heroku Postgres) or MongoDB (e.g., MongoDB Atlas)
- **Custom Domain** _(optional)_: If you wish to use a custom domain.

## Frontend Deployment

### Deploying to Vercel

Vercel is the recommended platform for deploying Next.js applications due to its seamless integration and optimized performance.

1. **Sign In to Vercel**:

   - Go to [Vercel](https://vercel.com/) and sign in using your GitHub account.

2. **Import Project**:

   - Click on **"New Project"**.
   - Select your **Next News** repository from GitHub.
   - Click **"Import"**.

3. **Configure Project Settings**:

   - **Framework Preset**: Vercel should automatically detect **Next.js**.
   - **Build & Output Settings**: Ensure the build command is `npm run build` or `yarn build` and the output directory is `.next`.

4. **Set Environment Variables**:

   - Navigate to the **"Environment Variables"** section.
   - Add the necessary environment variables as outlined in the [Environment Variables](#environment-variables) section below.

5. **Deploy**:
   - Click **"Deploy"**.
   - Vercel will build and deploy your application. Once completed, you’ll receive a live URL.

### Environment Variables

Proper configuration of environment variables is crucial for the frontend to communicate with the backend.

1. **Navigate to Project Settings**:

   - In Vercel, go to your **Next News** project.
   - Click on **"Settings"** > **"Environment Variables"**.

2. **Add Variables**:

   - **NEXT_PUBLIC_API_URL**: `https://your-backend-domain.com`
   - **NEXT_PUBLIC_SITE_TITLE**: `Next News`
   - **NEXT_PUBLIC_SITE_DESCRIPTION**: `A modern news portal built with Strapi and Next.js`
   - Add any other frontend-specific environment variables as needed.

3. **Save Changes**:
   - After adding all necessary variables, save the changes. Vercel will trigger a new deployment with the updated configurations.

### Custom Domain Setup

1. **Add Custom Domain**:

   - In Vercel, navigate to **"Domains"** under your project settings.
   - Click **"Add"** and enter your custom domain (e.g., `www.yourdomain.com`).

2. **Configure DNS**:

   - Update your domain’s DNS settings to point to Vercel. Vercel provides specific DNS records to add.

3. **Verify Domain**:
   - Once DNS changes propagate, Vercel will verify and activate your custom domain.

## Backend Deployment

### Deploying to Heroku

Heroku is a reliable platform for deploying Strapi applications with support for various add-ons.

1. **Sign In to Heroku**:

   - Go to [Heroku](https://www.heroku.com/) and sign in or create an account.

2. **Create a New App**:

   - Click on **"New"** > **"Create new app"**.
   - Enter a unique app name (e.g., `next-news-backend`) and select your region.
   - Click **"Create app"**.

3. **Connect to GitHub**:

   - In your Heroku app dashboard, navigate to the **"Deploy"** tab.
   - Under **"Deployment method"**, select **"GitHub"**.
   - Connect to your GitHub account and select the **Next News** repository.
   - Enable automatic deploys if desired.

4. **Provision a Database**:

   - Navigate to the **"Resources"** tab.
   - Under **"Add-ons"**, search for **Heroku Postgres** or **MongoDB Atlas**.
   - Select the desired plan and add it to your app.

5. **Set Environment Variables**:

   - Go to the **"Settings"** tab and click **"Reveal Config Vars"**.
   - Add the necessary environment variables as outlined in the [Environment Variables](#environment-variables) section below.

6. **Deploy**:
   - Trigger a manual deploy or wait for automatic deploys to complete.
   - Once deployed, your Strapi backend will be live at `https://your-backend-app.herokuapp.com`.

### Environment Variables

Configuring environment variables ensures that your backend operates correctly in production.

1. **Navigate to App Settings**:

   - In Heroku, go to your **Next News Backend** app.
   - Click on **"Settings"** > **"Reveal Config Vars"**.

2. **Add Variables**:

   - **DATABASE_URL**: Provided by your database add-on (Heroku Postgres or MongoDB Atlas).
   - **ADMIN_JWT_SECRET**: A secure, random string for admin authentication.
   - **JWT_SECRET**: A secure, random string for user authentication.
   - **EMAIL_PROVIDER**, **EMAIL_SMTP_HOST**, **EMAIL_SMTP_PORT**, **EMAIL_SMTP_USERNAME**, **EMAIL_SMTP_PASSWORD**: If using email functionalities.
   - Add any other backend-specific environment variables as needed.

3. **Save Changes**:
   - Heroku will automatically restart your app with the new configurations.

### Database Setup

Depending on your chosen database, follow the respective setup instructions.

#### PostgreSQL (Heroku Postgres)

1. **Provision Add-on**:

   - In Heroku, navigate to **"Resources"** > **"Add-ons"**.
   - Search for **Heroku Postgres** and add it.

2. **Access Database Credentials**:

   - Heroku automatically sets the `DATABASE_URL` environment variable with the connection string.

3. **Run Migrations**:
   - If applicable, run any necessary database migrations to set up your schema.

#### MongoDB (MongoDB Atlas)

1. **Set Up MongoDB Atlas**:

   - Sign up at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) and create a new cluster.

2. **Whitelist IP Addresses**:

   - In MongoDB Atlas, navigate to **"Network Access"** and whitelist your Heroku app’s IP addresses or allow access from anywhere (not recommended for production).

3. **Create a Database User**:

   - Set up a database user with appropriate permissions.

4. **Retrieve Connection String**:
   - Obtain the MongoDB connection string and set it as the `DATABASE_URL` in Heroku config vars.

### Custom Domain and SSL

1. **Add Custom Domain**:

   - In Heroku, go to your app’s **"Settings"**.
   - Under **"Domains and certificates"**, click **"Add domain"** and enter your custom domain.

2. **Configure DNS**:

   - Update your domain’s DNS settings to point to Heroku’s provided DNS target.

3. **Enable SSL**:
   - Heroku provides free SSL certificates for custom domains.
   - Ensure SSL is enabled to secure your backend.

## CI/CD Pipeline

Automating testing and deployment ensures that your application remains reliable and up-to-date.

### Setting Up GitHub Actions

1. **Create Workflow File**:

   - In your GitHub repository, navigate to `.github/workflows/`.
   - Create a new file, e.g., `deploy.yml`.

2. **Define Workflow**:

   - Configure the workflow to run on push events to the `main` branch.
   - Include jobs for building and deploying both frontend and backend.

3. **Sample Workflow Configuration**:

   ```yaml
   name: CI/CD Pipeline

   on:
     push:
       branches:
         - main

   jobs:
     build-frontend:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v2
         - name: Install Dependencies
           run: |
             cd frontend
             npm install
         - name: Build
           run: |
             cd frontend
             npm run build
         - name: Deploy to Vercel
           uses: amondnet/vercel-action@v20
           with:
             vercel-token: ${{ secrets.VERCEL_TOKEN }}
             vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
             vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
             working-directory: ./frontend
             alias: your-production-domain.com

     build-backend:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v2
         - name: Install Dependencies
           run: |
             cd backend
             npm install
         - name: Run Tests
           run: |
             cd backend
             npm test
         - name: Deploy to Heroku
           uses: akshnz/heroku-deploy@v3.12.12
           with:
             heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
             heroku_app_name: "next-news-backend"
             heroku_email: "atiqisrak@gmail.com"
   ```

4. **Configure Secrets**:

   - In GitHub, navigate to **"Settings"** > **"Secrets"**.
   - Add the following secrets:
     - `VERCEL_TOKEN`: Your Vercel API token.
     - `VERCEL_ORG_ID`: Your Vercel organization ID.
     - `VERCEL_PROJECT_ID`: Your Vercel project ID.
     - `HEROKU_API_KEY`: Your Heroku API key.

5. **Commit Workflow**:
   - Commit and push the `deploy.yml` file to trigger the workflow.

## Security Considerations

### HTTPS Enforcement

Ensure all communications between the frontend, backend, and users are encrypted.

- **Vercel and Heroku** automatically provide SSL certificates for deployed applications.
- **Custom Domains**: Verify that SSL is correctly configured for custom domains to prevent mixed content issues.

### Environment Variables Management

- **Never Commit `.env` Files**: Keep environment variables out of version control to protect sensitive information.
- **Use Secrets Management**: Utilize platform-specific secrets management features (e.g., Vercel Secrets, Heroku Config Vars) to securely store environment variables.

### Access Controls

- **Role-Based Permissions**: Configure user roles in Strapi to restrict access to sensitive operations.
- **API Security**: Protect API endpoints using authentication and authorization mechanisms to prevent unauthorized access.

## Scalability and Performance

### Scaling Backend Services

- **Heroku Dynos**: Scale your backend by increasing the number of dynos based on traffic.
- **Database Scaling**: Upgrade your database plan to handle increased data and query loads.

### Optimizing Frontend Performance

- **Static Generation**: Utilize Next.js’s static generation features to serve pre-rendered pages for faster load times.
- **Image Optimization**: Use Next.js’s built-in Image component to optimize images automatically.
- **Code Splitting**: Leverage dynamic imports to split code and reduce initial load times.

## Monitoring and Logging

### Monitoring Tools

- **Heroku Metrics**: Use Heroku’s built-in monitoring to track app performance, memory usage, and response times.
- **Vercel Analytics**: Monitor frontend performance metrics through Vercel’s analytics dashboard.
- **External Tools**: Integrate with tools like New Relic or Datadog for advanced monitoring capabilities.

### Logging Setup

- **Heroku Logs**: Access logs via the Heroku dashboard or using the Heroku CLI (`heroku logs --tail`).
- **Strapi Logging**: Configure Strapi to use centralized logging services for better log management.
- **Error Tracking**: Implement tools like Sentry to capture and monitor application errors in real-time.

## Troubleshooting Deployment Issues

### Common Issues

- **Deployment Failures**:

  - **Frontend**: Check build logs in Vercel for errors related to dependencies or build scripts.
  - **Backend**: Review Heroku logs for issues related to environment variables or database connections.

- **Environment Variable Misconfigurations**:

  - Ensure all required environment variables are set correctly in Vercel and Heroku.
  - Verify that the frontend’s `NEXT_PUBLIC_API_URL` points to the correct backend URL.

- **Database Connection Issues**:

  - Confirm that the database service is running and accessible.
  - Check the `DATABASE_URL` for correct credentials and connection details.

- **CORS Errors**:
  - Ensure that the backend’s CORS settings include the frontend’s domain.
  - Update the `backend/config/middlewares.js` or `backend/config/server.js` accordingly.

### Getting Help

If you encounter issues not covered in this guide:

- **Open an Issue**: Visit the [GitHub Issues](https://github.com/Aliio-Inc/strapi-next-news/issues) page to report the problem.
- **Community Support**: Engage with the open-source community or seek help from platform-specific support channels (e.g., Vercel Support, Heroku Support).

## Additional Resources

- [Vercel Documentation](https://vercel.com/docs)
- [Heroku Documentation](https://devcenter.heroku.com/)
- [Strapi Deployment Guides](https://strapi.io/documentation/developer-docs/latest/setup-deployment-guides/index.html)
- [Next.js Deployment Documentation](https://nextjs.org/docs/deployment)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Sentry Documentation](https://docs.sentry.io/)

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Clearly states the purpose of the document, outlining the steps required to deploy Next News to production environments.

- **Prerequisites**: Lists essential tools and accounts needed before starting the deployment process, ensuring users are prepared.

- **Frontend Deployment**:

  - **Deploying to Vercel**: Provides a step-by-step guide to deploy the Next.js frontend using Vercel, including connecting to GitHub, configuring project settings, and deploying.
  - **Environment Variables**: Explains how to set up necessary environment variables in Vercel to ensure proper communication between frontend and backend.
  - **Custom Domain Setup**: Guides users on adding a custom domain to their Vercel deployment for a professional appearance.

- **Backend Deployment**:

  - **Deploying to Heroku**: Details the process of deploying the Strapi backend to Heroku, including creating a new app, connecting to GitHub, provisioning a database, and deploying.
  - **Environment Variables**: Covers setting up essential environment variables in Heroku to secure and configure the backend application.
  - **Database Setup**: Provides instructions for setting up PostgreSQL or MongoDB, depending on user preference, ensuring the backend can store and manage data effectively.
  - **Custom Domain and SSL**: Explains how to add a custom domain to the Heroku backend and enable SSL for secure communications.

- **CI/CD Pipeline**:

  - **Setting Up GitHub Actions**: Introduces automating the build and deployment process using GitHub Actions, enhancing workflow efficiency and reliability.

- **Security Considerations**:

  - **HTTPS Enforcement**: Emphasizes the importance of serving applications over HTTPS to protect data in transit.
  - **Environment Variables Management**: Highlights best practices for managing sensitive information through environment variables and secrets management.
  - **Access Controls**: Discusses configuring user roles and API security to prevent unauthorized access.

- **Scalability and Performance**:

  - **Scaling Backend Services**: Advises on scaling backend resources using Heroku dynos and upgrading databases as needed.
  - **Optimizing Frontend Performance**: Offers tips for enhancing frontend performance through static generation, image optimization, and code splitting.

- **Monitoring and Logging**:

  - **Monitoring Tools**: Suggests tools like Heroku Metrics, Vercel Analytics, New Relic, and Datadog for tracking application performance and health.
  - **Logging Setup**: Recommends setting up centralized logging and error tracking with tools like Sentry to monitor and debug issues effectively.

- **Troubleshooting Deployment Issues**:

  - **Common Issues**: Identifies frequent deployment problems and provides potential solutions to help users resolve them quickly.
  - **Getting Help**: Encourages users to seek assistance by opening GitHub issues or utilizing support channels if they encounter unresolved problems.

- **Additional Resources**: Provides links to official documentation and resources for Vercel, Heroku, Strapi, Next.js, GitHub Actions, and Sentry, enabling users to delve deeper into specific topics as needed.

- **Footer**: Includes project information, author details, website link, and contact information for further support and inquiries.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

Feel free to customize this deployment guide to better fit the specific needs of your project. If you have any questions or need further assistance, don't hesitate to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out to the maintainers.
