# octave-api

![CI](https://img.shields.io/github/actions/workflow/status/layalelzeinti/octave-api/ci.yml?branch=main&label=CI) ![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-3178C6) ![License](https://img.shields.io/github/license/layalelzeinti/octave-api?color=blue) ![Version](https://img.shields.io/badge/version-1.6.2-green)

A minimal, tree-shakeable TypeScript client library with full type definitions. octave-api provides a Client class with HTTP method wrappers (get, post, put, delete), configurable retry with exponential backoff, typed ApiResponse and PaginatedResponse interfaces, and request/response interceptors. Built with tsup for CJS+ESM dual output.

## Features

- Client class with get/post/put/delete method wrappers
- Vitest test suite with mocked responses
- Works in both Node.js and browser environments
- Zero runtime dependencies -- uses native fetch
- Configurable base URL and API key
- Tree-shakeable and side-effect free for bundlers
- Automatic retry with exponential backoff (configurable maxRetries, default 3)

## Prerequisites

- Node.js 16 or higher
- TypeScript 5.0 or higher
- npm, yarn, or pnpm

## Installation

```bash
npm install octave-api
# or
yarn add octave-api
# or
pnpm add octave-api
```

## Usage

```typescript
import { Client } from 'octave-api';
import type { ApiResponse } from 'octave-api';

const client = new Client({
  apiKey: process.env.API_KEY!,
  baseUrl: 'https://api.example.com',
  maxRetries: 3,
});

// GET request with typed response
const data = await client.get<ApiResponse<{ id: string; name: string }>>('/items/1');
console.log(data.data.name);

// POST request
const created = await client.post('/items', { name: 'New Item', value: 42 });

// Automatic retry with exponential backoff on failure
// The client retries up to maxRetries times with 2^attempt * 1000ms delay
```

## Project Structure

```
octave-api/
├── src/
│   ├── client.ts
│   └── index.ts
├── tests/client.test.ts
├── package.json  tsconfig.json  tsup.config.ts
├── README.md  LICENSE  CHANGELOG.md  CONTRIBUTING.md  CODE_OF_CONDUCT.md
├── .github/
│   ├── workflows/ci.yml
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   └── PULL_REQUEST_TEMPLATE.md
└── .gitignore
```

## Running Tests

```bash
npm test
# watch mode
npm test -- --watch
```

## FAQ

**Is this production-ready?**
Yes, octave-api includes tests, CI/CD, and documentation. However, you should review the code and adapt it to your specific needs before deploying.

**Can I use this in my project?**
Yes, octave-api is licensed under the MIT. See the [LICENSE](LICENSE) file for details.

**How do I report a bug?**
Please [open an issue](https://github.com/layalelzeinti/octave-api/issues/new?template=bug_report.md) using the bug report template.

**How do I request a feature?**
Please [open an issue](https://github.com/layalelzeinti/octave-api/issues/new?template=feature_request.md) using the feature request template.

**How can I contribute?**
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

Quick start:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Make your changes and run tests (see [Running Tests](#running-tests) above)
4. Commit with a clear message: `git commit -am 'Add: my feature'`
5. Push to your fork: `git push origin feature/my-feature`
6. Open a Pull Request

Please ensure all tests pass before submitting a pull request.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for a list of changes and version history.

## License

This project is licensed under the MIT -- see the [LICENSE](LICENSE) file for details.

Copyright (c) 2026 nina smith.
