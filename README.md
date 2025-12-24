# Lighthouse Plugin Example

This is an example for how to make a Lighthouse plugin with custom audits. This plugin demonstrates how to extend Lighthouse with custom audits that check for specific elements on web pages.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Plugin Structure](#plugin-structure)
- [Features](#features)
- [Development Guide](#development-guide)
- [Contributing](#contributing)
- [License](#license)
- [Additional Resources](#additional-resources)

## Installation

First, ensure you have Node.js 18.16 or higher installed. Then install the plugin along with Lighthouse:

```bash
npm install -D lighthouse lighthouse-plugin-example
```

## Usage

### Running with CLI

To run Lighthouse with this plugin from the command line:

```bash
lighthouse https://example.com --plugins=lighthouse-plugin-example --only-categories=lighthouse-plugin-example --view
```

Or use the npm script provided in this repository:

```bash
npm run run-plugin https://example.com
```

### Configuration Options

- `--plugins=lighthouse-plugin-example`: Loads the plugin
- `--only-categories=lighthouse-plugin-example`: Only runs audits from this plugin
- `--view`: Opens the results in your browser automatically

## Plugin Structure

The plugin consists of the following key files:

```
lighthouse-plugin-example/
├── audits/
│   └── has-cat-images.js    # Custom audit implementation
├── plugin.js                 # Main plugin configuration
└── package.json             # Plugin metadata and dependencies
```

### Key Components

- **`plugin.js`**: Defines the plugin configuration, including which audits to run and how to display results
- **`audits/has-cat-images.js`**: A sample audit that checks if a page contains cat images
- **`package.json`**: Declares the plugin entry point and dependencies

## Features

### Custom Audits

This plugin includes the following custom audit:

#### Cat Images Audit (`has-cat-images-id`)

- **Purpose**: Checks if the page contains at least one cat image
- **Pass Criteria**: The page has one or more images with "cat" in the URL
- **Impact**: Demonstrates how to access and analyze image artifacts in Lighthouse
- **Score**: 100 if cat images are found, 0 otherwise

This audit showcases:
- How to access Lighthouse artifacts (`ImageElements`)
- How to filter and analyze page elements
- How to return meaningful audit results

## Development Guide

### Local Development

1. Clone this repository
2. Install dependencies:
   ```bash
   npm install
   ```

### Creating Your Own Audits

To create a new audit:

1. Create a new file in the `audits/` directory
2. Extend the `Audit` class from Lighthouse
3. Define the `meta` object with audit metadata
4. Implement the `audit()` method with your custom logic
5. Register the audit in `plugin.js`

Example audit structure:

```javascript
import {Audit} from 'lighthouse';

class MyCustomAudit extends Audit {
  static get meta() {
    return {
      id: 'my-audit-id',
      title: 'My Audit Title',
      failureTitle: 'My Audit Failure Message',
      description: 'Description of what this audit checks',
      requiredArtifacts: ['ArtifactName'],
    };
  }

  static audit(artifacts) {
    // Your audit logic here
    return {
      score: 1, // 0 to 1
      numericValue: 0, // Optional numeric result
    };
  }
}

export default MyCustomAudit;
```

### Testing Your Plugin

Test your plugin by running it against various websites:

```bash
npm run run-plugin https://example.com
```

## Contributing

We welcome contributions! Please see our [CONTRIBUTING](./CONTRIBUTING) guide for details on:

- Code of Conduct
- Contributor License Agreement
- How to submit pull requests
- Code review process

## License

This project is licensed under the Apache License 2.0. See the [LICENSE](./LICENSE) file for details.

## Additional Resources

- [Lighthouse Plugin Handbook](https://github.com/GoogleChrome/lighthouse/blob/main/docs/plugins.md) - Complete guide to creating Lighthouse plugins
- [Lighthouse Documentation](https://github.com/GoogleChrome/lighthouse) - Main Lighthouse repository
- [Available Artifacts](https://github.com/GoogleChrome/lighthouse/blob/main/docs/plugins.md#plugin-audits) - List of artifacts you can use in audits
- [Audit Best Practices](https://github.com/GoogleChrome/lighthouse/blob/main/docs/recipes/custom-audit) - Guidelines for writing quality audits
