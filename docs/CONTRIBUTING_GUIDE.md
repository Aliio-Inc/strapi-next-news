# Contributing to Next News

First off, thank you for considering contributing to **Next News**! 🎉 Your involvement helps make this project better for everyone.

## Table of Contents

- [How Can I Contribute?](#how-can-i-contribute)
  - [Reporting Bugs](#reporting-bugs)
  - [Suggesting Enhancements](#suggesting-enhancements)
  - [Pull Requests](#pull-requests)
- [Code of Conduct](#code-of-conduct)
- [Style Guides](#style-guides)
  - [Git Commit Messages](#git-commit-messages)
  - [JavaScript Style Guide](#javascript-style-guide)
- [Branching Model](#branching-model)
- [Setting Up the Development Environment](#setting-up-the-development-environment)
- [Running Tests](#running-tests)
- [Additional Notes](#additional-notes)

## How Can I Contribute?

There are several ways you can contribute to **Next News**:

### Reporting Bugs

If you find a bug in the project, please follow these steps:

1. **Search Existing Issues**: Check if the bug has already been reported to avoid duplicates.
2. **Open a New Issue**: If the bug hasn't been reported, open a new issue and provide detailed information, including:
   - A clear and descriptive title.
   - A detailed description of the bug.
   - Steps to reproduce the bug.
   - Expected vs. actual behavior.
   - Screenshots or logs if applicable.

### Suggesting Enhancements

If you have an idea to improve **Next News**, please follow these steps:

1. **Search Existing Issues**: Check if the enhancement has already been suggested.
2. **Open a New Issue**: If not, open a new issue and include:
   - A clear and descriptive title.
   - A detailed description of the enhancement.
   - The benefits or use-cases of the enhancement.
   - Any additional context or screenshots if applicable.

### Pull Requests

We welcome pull requests (PRs) to help improve the project. Here's how you can contribute:

1. **Fork the Repository**: Click on the **Fork** button at the top right of the repository page.
2. **Clone Your Fork**:
   ```bash
   git clone https://github.com/your-username/strapi-next-news.git
   cd strapi-next-news
   ```
3. **Create a New Branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```
4. **Make Your Changes**: Implement your feature or fix the bug.
5. **Commit Your Changes**:
   ```bash
   git commit -m "feat: add your feature description"
   ```
6. **Push to Your Fork**:
   ```bash
   git push origin feature/your-feature-name
   ```
7. **Open a Pull Request**: Navigate to the original repository and click on **Compare & pull request**.

### Review Process

1. **Code Review**: Your PR will be reviewed by the maintainers. They may request changes or approve it.
2. **Address Feedback**: Make the necessary changes and push them to your branch.
3. **Merge**: Once approved, your PR will be merged into the main branch.

## Code of Conduct

Please read and follow our [Code of Conduct](./CODE_OF_CONDUCT.md) to ensure a welcoming and respectful environment for all contributors.

## Style Guides

### Git Commit Messages

Adhere to the following format for commit messages:

```
<type>: <subject>

<body>
```

**Types:**

- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation only changes
- `style`: Changes that do not affect the meaning of the code
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `test`: Adding missing tests or correcting existing tests
- `chore`: Changes to the build process or auxiliary tools

**Example:**

```
feat: add user authentication with JWT

Implemented JWT-based authentication to secure API endpoints. Users can now register and log in to access protected routes.
```

### JavaScript Style Guide

- **Indentation**: Use 2 spaces for indentation.
- **Quotes**: Use single quotes `'` for strings.
- **Semicolons**: Omit semicolons; rely on ASI (Automatic Semicolon Insertion).
- **Arrow Functions**: Use arrow functions for anonymous functions.
- **Destructuring**: Prefer destructuring assignment where applicable.
- **Modules**: Use ES6 modules (`import`/`export`) instead of CommonJS (`require`/`module.exports`).

## Branching Model

We follow the **GitFlow** branching model:

- **`main` Branch**: Contains the stable production-ready code.
- **`develop` Branch**: Integrates features and fixes before merging into `main`.
- **Feature Branches**: Named as `feature/feature-name` for new features.
- **Bugfix Branches**: Named as `bugfix/bug-name` for bug fixes.
- **Release Branches**: Named as `release/version-number` for preparing releases.
- **Hotfix Branches**: Named as `hotfix/issue-number` for urgent fixes on `main`.

## Setting Up the Development Environment

To set up the project locally for development:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Aliio-Inc/strapi-next-news.git
   cd strapi-next-news
   ```
2. **Install Dependencies**:
   ```bash
   npm install
   # or
   yarn install
   ```
3. **Configure Environment Variables**: Follow the [Installation Guide](./Installation.md) to set up `.env` files.
4. **Run the Development Server**:
   ```bash
   npm run dev
   # or
   yarn dev
   ```

## Running Tests

Ensure all tests pass before submitting a PR:

1. **Navigate to Backend Directory**:
   ```bash
   cd backend
   ```
2. **Run Tests**:
   ```bash
   npm test
   # or
   yarn test
   ```

## Additional Notes

- **Documentation**: Keep the documentation up-to-date with your changes. Update relevant markdown files as necessary.
- **Feedback**: We value your feedback! Feel free to share suggestions or improvements.
- **Stay Updated**: Regularly sync your fork with the upstream repository to stay updated with the latest changes.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

## Brief Explanation

- **Title and Introduction**: Clearly indicates that the document provides guidelines for contributing to the Next News project, expressing gratitude to potential contributors.

- **Table of Contents**: Organized list of sections to help contributors navigate the document easily.

- **How Can I Contribute?**:

  - **Reporting Bugs**: Instructions on how to report bugs, ensuring issues are well-documented and avoiding duplicates.
  - **Suggesting Enhancements**: Guidelines for proposing new features or improvements, emphasizing clear descriptions and benefits.
  - **Pull Requests**: Step-by-step instructions on how to create and submit pull requests, including branching and committing best practices.
  - **Review Process**: Outlines the code review process, encouraging constructive feedback and collaboration.

- **Code of Conduct**: Directs contributors to adhere to the project's Code of Conduct, fostering a respectful and inclusive environment.

- **Style Guides**:

  - **Git Commit Messages**: Provides a standardized format for commit messages to maintain clarity and consistency in the project history.
  - **JavaScript Style Guide**: Recommends coding standards for the frontend, including indentation, quotes, semicolon usage, and module syntax to ensure codebase uniformity.

- **Branching Model**: Describes the GitFlow branching strategy, explaining the purpose of different branches (e.g., `main`, `develop`, `feature/*`, `bugfix/*`, `release/*`, `hotfix/*`) to manage development workflows effectively.

- **Setting Up the Development Environment**: Guides new contributors through cloning the repository, installing dependencies, configuring environment variables, and running the development server, ensuring they can start contributing quickly.

- **Running Tests**: Emphasizes the importance of running tests before submitting contributions, providing commands to execute tests in the backend.

- **Additional Notes**: Encourages keeping documentation up-to-date, providing feedback, and staying synchronized with the upstream repository, promoting continuous improvement and collaboration.

- **Footer**: Includes essential project information, author details, website link, and contact information, offering contributors resources for further assistance and engagement.

Overall, the **CONTRIBUTING.md** file serves as a comprehensive guide for potential contributors, outlining the procedures, standards, and expectations for contributing to the Next News project. It aims to facilitate a smooth and productive collaboration process, ensuring that contributions align with the project's goals and maintain its quality.

---

**Project:** [Next News](https://github.com/Aliio-Inc/strapi-next-news)  
**Author:** Atiq Israk  
**Website:** [https://aliio.tech](https://aliio.tech)  
**Contact:** [atiqisrak@gmail.com](mailto:atiqisrak@gmail.com)

---

Feel free to customize this contributing guide to better fit the specific needs of your project. If you have any questions or need further assistance, don't hesitate to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out to the maintainers.
