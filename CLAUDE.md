# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

FlowiseChatEmbed is a JavaScript library for embedding Flowise chatbots into websites. It provides two main integration modes: a popup chat widget and a full-page chat interface.

## Key Technologies

- **UI Framework**: Solid.js (reactive, similar to React but with fine-grained reactivity)
- **Build Tool**: Rollup with TypeScript
- **Styling**: Tailwind CSS with PostCSS
- **Package Manager**: Yarn (v1.22.22)

## Development Commands

```bash
# Essential commands
yarn install         # Install dependencies
yarn dev            # Start dev server at http://localhost:5678 with hot reload
yarn build          # Build production files (dist/web.js and dist/web.umd.js)

# Code quality
yarn lint           # Run ESLint
yarn lint-fix       # Auto-fix ESLint issues
yarn format         # Format with Prettier
yarn format:check   # Check formatting

# Proxy server (optional)
yarn start          # Start proxy server at http://localhost:3001
```

## Architecture & Code Structure

### Component Organization

- `/src/features/` - Main chat implementations
  - `bubble/` - Popup chat widget with floating button
  - `full/` - Full-page chat implementation
  - `popup/` - Popup and disclaimer functionality
- `/src/components/` - Reusable UI components organized by type
- `/src/utils/` - Utility functions
- `/server.js` - Optional proxy server for enhanced security

### Key Patterns

- **Web Components**: Exports as custom elements (`<flowise-chatbot>`, `<flowise-fullchatbot>`)
- **State Management**: Uses Solid.js signals and effects (no external state library)
- **Path Aliases**: `@/*` maps to `src/*` directory
- **Theming**: Extensive customization through theme props passed to init()

### Build Output

- `dist/web.js` - ES module build
- `dist/web.umd.js` - UMD build for broader compatibility

## Development Workflow

1. **Local Development**: Run `yarn dev` and modify `public/index.html` with your chatflow details for testing
2. **Hot Reload**: Changes to source files automatically reload at http://localhost:5678
3. **Building**: Use `yarn build` to create distribution files
4. **Integration**: Embed via CDN or self-host the built files

## Important Implementation Notes

### Solid.js Specifics

- Components use function syntax, not classes
- Use `createSignal`, `createEffect`, `Show`, `For` from solid-js
- Props are accessed directly (not destructured) to maintain reactivity
- No virtual DOM - updates are fine-grained

### Tailwind CSS

- Utility classes are used extensively
- Custom colors and themes are applied via inline styles
- PostCSS processes Tailwind directives during build

### Event Streaming

- Uses `@microsoft/fetch-event-source` for SSE support
- Handles streaming responses from Flowise API
- Implements retry logic for connection failures

### File Uploads

- Client-side uses standard file input with base64 encoding
- Server-side (proxy) uses Multer for multipart handling
- Supports images and documents based on Flowise configuration

## Testing Approach

No automated tests are currently implemented. Testing is done manually by:

1. Running `yarn dev`
2. Updating `public/index.html` with test configurations
3. Verifying functionality in the browser

## Proxy Server Configuration

When using the proxy server for enhanced security:

1. Copy `.env.example` to `.env`
2. Configure `API_HOST`, `FLOWISE_API_KEY`, and agent mappings
3. Agent format: `agentName=chatflowId,allowedDomain`

The proxy server provides domain-based access control and hides API keys from the client.
