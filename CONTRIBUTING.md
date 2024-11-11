# Contributing to Next News

First off, thank you for considering contributing to **Next News**! 🎉 Your efforts are greatly appreciated and help make this project better for everyone.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
  - [Reporting Bugs](#reporting-bugs)
  - [Suggesting Enhancements](#suggesting-enhancements)
  - [Pull Requests](#pull-requests)
- [Style Guide](#style-guide)
- [Development Setup](#development-setup)
- [Commit Guidelines](#commit-guidelines)
- [License](#license)

## Code of Conduct

Please read and follow our [Code of Conduct](./CODE_OF_CONDUCT.md) to ensure a welcoming and respectful environment for all contributors.

## How to Contribute

### Reporting Bugs

If you find a bug in **Next News**, please follow these steps:

1. **Search Existing Issues**: Look through the [open issues](https://github.com/Aliio-Inc/strapi-next-news/issues) to see if the bug has already been reported.
2. **Create a New Issue**: If the bug hasn't been reported, click on the "New issue" button.
3. **Provide Detailed Information**:
   - **Title**: A clear and descriptive title.
   - **Description**: Detailed information about the bug.
   - **Steps to Reproduce**: Step-by-step instructions to reproduce the issue.
   - **Expected Behavior**: What you expected to happen.
   - **Actual Behavior**: What actually happened.
   - **Screenshots**: If applicable, add screenshots to help explain the issue.
   - **Environment**: Information about your setup (e.g., OS, browser, versions).

### Suggesting Enhancements

We welcome suggestions for new features or improvements! To propose an enhancement:

1. **Search Existing Issues**: Check if the enhancement has already been suggested.
2. **Create a New Issue**: Click on "New issue" and select the "Feature request" template.
3. **Provide Detailed Information**:
   - **Title**: A clear and descriptive title.
   - **Description**: Detailed explanation of the enhancement.
   - **Benefits**: Explain why this enhancement would be valuable.
   - **Possible Implementation**: Any ideas on how to implement it.

### Pull Requests

Contributions through pull requests are highly encouraged! Here's how to submit one:

1. **Fork the Repository**: Click the "Fork" button at the top-right corner of the repository page.
2. **Clone Your Fork**:
   ```bash
   git clone https://github.com/your-username/strapi-next-news.git
   ```
3. **Create a New Branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```
4. **Make Your Changes**: Implement your feature or bug fix.
5. **Commit Your Changes**:
   ```bash
   git commit -m "Add feature: your feature description"
   ```
6. **Push to Your Fork**:
   ```bash
   git push origin feature/your-feature-name
   ```
7. **Open a Pull Request**: Navigate to the original repository and click "Compare & pull request". Provide a clear description of your changes.

**Please ensure your pull request adheres to the [Style Guide](#style-guide) and includes necessary tests if applicable.**

## Style Guide

To maintain consistency and quality, please follow these guidelines:

- **Code Formatting**: Use [Prettier](https://prettier.io/) for code formatting. Ensure your code passes linting checks.
- **Naming Conventions**: Use meaningful and descriptive names for variables, functions, and components.
- **Documentation**: Document your code where necessary, especially for complex logic.
- **Commit Messages**: Follow the [Commit Guidelines](#commit-guidelines) for clear and descriptive commit messages.

## Development Setup

To set up a local development environment, follow these steps:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/Aliio-Inc/strapi-next-news.git
   cd strapi-next-news
   ```
2. **Install Dependencies**:
   - **Frontend**:
     ```bash
     cd frontend
     npm install
     # or
     yarn install
     ```
   - **Backend**:
     ```bash
     cd ../backend
     npm install
     # or
     yarn install
     ```
3. **Configure Environment Variables**:
   - Create `.env` files in both `frontend` and `backend` directories based on `.env.example`.
4. **Run the Application**:
   - **Backend**:
     ```bash
     cd backend
     npm run develop
     # or
     yarn develop
     ```
   - **Frontend**:
     ```bash
     cd frontend
     npm run dev
     # or
     yarn dev
     ```

## Commit Guidelines

Please follow these guidelines to ensure your commits are clear and helpful:

- **Use the Imperative Mood**: e.g., "Add feature" instead of "Added feature".
- **Be Descriptive**: Clearly describe what changes the commit includes.
- **Reference Issues**: If your commit relates to an issue, include its number (e.g., `Fixes #123`).

**Example Commit Message**:

```
Add user authentication feature

- Implement JWT-based authentication
- Add login and registration forms
- Update API endpoints to handle auth
```

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](./LICENSE.md).

---

Thank you for your interest in contributing to **Next News**! If you have any questions or need assistance, feel free to [open an issue](https://github.com/Aliio-Inc/strapi-next-news/issues) or reach out to the maintainers.
