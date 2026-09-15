# Postman Tests - PlatziFakeStore API Testing

This project contains automated API tests for the **PlatziFakeStore** e-commerce platform using Postman collections and Newman CLI.

## About the Project

This is an API testing suite that validates the functionality of PlatziFakeStore endpoints including:

- User authentication (Login)
- E-commerce operations (products, orders, users, etc.)
- API response validation
- Token management and refresh token flows

The test suite uses Postman's built-in testing framework with automated assertions to verify API behavior, response codes, and data integrity.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v22 or higher) - [Download](https://nodejs.org/)
- **npm** (comes with Node.js)
- **Git** (optional, for version control)

## Installation

1. **Clone or download the project**

   ```bash
   cd "Postman Tests"
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

   This will install Newman and other required packages defined in `package.json`.

## Project Structure

```
Postman Tests/
├── tests/
│   ├── platziFakeStore.postman.json    # Main Postman collection with all API tests
│   └── README.md
├── newman/                              # Directory for test reports
├── package.json                         # Project dependencies
├── package-lock.json                    # Dependency lock file
└── README.md                            # This file
```

## Running Tests

### Using Newman CLI

#### 1. **Run all tests (with default reporter)**

```bash
npx newman run tests/platziFakeStore.postman.json
```

#### 2. **Run tests with HTML report**

```bash
npx newman run tests/platziFakeStore.postman.json -r htmlextra
```

Report will be saved in the `newman/` directory.

#### 3. **Run tests with JSON report**

```bash
npx newman run tests/platziFakeStore.postman.json -r json
```

#### 4. **Run tests with CLI report (detailed output)**

```bash
npx newman run tests/platziFakeStore.postman.json -r cli
```

#### 5. **Run tests with custom output file**

```bash
npx newman run tests/platziFakeStore.postman.json -r html --reporter-html-export newman/custom-report.html
```

#### 6. **Run specific test folder (if using collections with folders)**

```bash
npx newman run tests/platziFakeStore.postman.json --folder "Login"
```

### Common Newman Options

| Option                   | Description                                   |
| ------------------------ | --------------------------------------------- |
| `-e, --environment`      | Specify environment file for variables        |
| `-d, --data`             | Pass raw request data                         |
| `--folder`               | Run only specific folder(s) in the collection |
| `--timeout`              | Set request timeout in milliseconds           |
| `-n, --iteration-count`  | Number of times to run the collection         |
| `-r, --reporters`        | Specify output format (cli, json, html, etc.) |
| `--reporter-html-export` | Export HTML report to specific file           |
| `--bail`                 | Stop running tests on first failure           |
| `-k, --insecure`         | Disable SSL certificate validation            |

## Examples

### Run tests and save both HTML and JSON reports

```bash
npx newman run tests/platziFakeStore.postman.json \
  -r cli,html,json \
  --reporter-html-export newman/report.htmlextra \
  --reporter-json-export newman/report.json
```

### Run tests with 5-second timeout and stop on first failure

```bash
npx newman run tests/platziFakeStore.postman.json \
  --timeout 5000 \
  --bail
```

### Run collection 3 times

```bash
npx newman run tests/platziFakeStore.postman.json -n 3
```

## Using Environment Variables

If your collection uses environment variables, create an environment file and run:

```bash
npx newman run tests/platziFakeStore.postman.json -e environment.json
```

Environment file example:

```json
{
  "name": "Development",
  "values": [
    {
      "key": "baseUrl",
      "value": "https://api.example.com"
    },
    {
      "key": "apiKey",
      "value": "your-api-key-here"
    }
  ]
}
```

## Troubleshooting

### Command not found: newman

Make sure you've run `npm install` and Newman is properly installed:

```bash
npm install -g newman  # Install globally (optional)
```

### SSL Certificate Errors

If you encounter SSL certificate errors:

```bash
npx newman run tests/platziFakeStore.postman.json --insecure
```

### Timeout Issues

Increase timeout for slow APIs:

```bash
npx newman run tests/platziFakeStore.postman.json --timeout 10000
```

### Tests Failing

- Check that the API endpoint is accessible
- Verify authentication tokens/credentials in the collection
- Review test results in the Newman report for specific error messages
- Check network connectivity

## Viewing Test Reports

After running tests with the HTML reporter, open the generated report:

```bash
# macOS
open newman/report.html

# Linux
xdg-open newman/report.html

# Windows
start newman/report.html
```

## Contributing

To add new tests:

1. Open Postman and import `tests/platziFakeStore.postman.json`
2. Add new requests and test scripts
3. Export the updated collection back to the same file
4. Run tests to validate

## Author

**Yuliia Vasylieva**

## License

ISC

---

For more information about Newman, visit: [Newman Documentation](https://learning.postman.com/docs/collections/using-collections-in-newman/)
