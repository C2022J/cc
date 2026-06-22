# Claude Code 2.1.88 Recovered

English | [简体中文](./README.zh-CN.md)

A reconstructed Claude Code 2.1.88 project generated from `cli.js.map`, reorganized into a standard npm-based repository that can install dependencies, build successfully, and launch the CLI entrypoint.

## Overview

This repository exists to turn reverse-sourcemap output into a practical development project that is easier to:

- install with npm
- build locally
- run from source
- continue repairing and extending

Verified working today:

- `npm install`
- `npm run build`
- `node dist/cli.js --help`
- `node dist/cli.js --version`

## Important Notes

This is not the official upstream source repository. It is a recovered and reconstructed project derived from sourcemap output.

Because reverse-sourcemap recovery is incomplete, the current build includes compatibility layers, generated shims, and stub modules to keep the project installable and buildable. In practice, that means:

- it is suitable for research, debugging, and iterative recovery work
- it is not guaranteed to behave exactly like the official published bundle
- some private integrations, native paths, or advanced features may still need manual restoration

## Requirements

- Node.js `>= 18`
- npm `>= 9`

Check your environment first:

```bash
node -v
npm -v
```

## Quick Start

```bash
npm install
npm run build
node dist/cli.js --help
```

## Installation

Install dependencies from the project root:

```bash
npm install
```

This uses [package.json](./package.json) and `package-lock.json` to resolve and install dependencies.

## Build

Build the project with:

```bash
npm run build
```

The build output is written to:

- `dist/cli.js`
- `dist/src/**`
- `dist/vendor/**`

The build pipeline is implemented in [scripts/build.mjs](./scripts/build.mjs). It currently handles:

- transpiling `src/` and `vendor/` into Node.js-compatible ESM output
- rewriting `bun:*` imports into npm/Node-compatible shims
- resolving `src/*` alias imports
- generating compatibility stubs for unresolved recovered modules
- injecting build-time constants required by CLI startup

## Run

Run the built CLI directly:

```bash
node dist/cli.js --help
```

Print the version:

```bash
node dist/cli.js --version
```

You can also run through npm:

```bash
npm start -- --help
```

## Install as a Local CLI

To install this project as a global command after building:

```bash
npm install -g .
```

Then run:

```bash
claude-recovered --help
```

For local development workflows, `npm link` is also supported:

```bash
npm link
```

## Common Commands

```bash
npm install
npm run build
npm run clean
npm start -- --help
node dist/cli.js --version
```

## Project Structure

```text
.
├── package.json
├── package-lock.json
├── scripts/
│   └── build.mjs
├── src/
├── vendor/
└── dist/
```

Notes:

- `src/`: recovered source files
- `vendor/`: local compatibility replacements for unavailable native or private modules
- `scripts/build.mjs`: custom npm build pipeline
- `dist/`: generated runtime output

## Known Limitations

- some original dependencies do not exist on npm and are currently replaced with local shims
- some modules could not be fully recovered from the sourcemap and are currently stubbed during build
- "starts successfully" does not mean "feature-complete parity with the official bundle"
- private services, private protocols, and native-platform paths may still require additional restoration work

## Troubleshooting

If you hit build or runtime issues, use this order:

1. Confirm that Node.js is at least version 18.
2. Remove old build output.
3. Reinstall dependencies.
4. Rebuild.
5. Validate the base CLI entrypoint.

Useful commands:

```bash
npm run clean
npm install
npm run build
node dist/cli.js --help
```

## Development Focus

If you want to continue improving this recovered project, the highest-value next steps are usually:

- fixing startup-time runtime errors
- replacing generated stubs with real implementations
- restoring missing private dependency behavior with compatible replacements
- validating high-value commands against the original bundle behavior

## License and Source Considerations

This repository contains code reconstructed from sourcemap-derived output. Before redistributing or publishing it, make sure you review the original project's license, copyright, and usage terms.
