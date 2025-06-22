# Insly AI Chat Widget

A customizable chat widget for embedding Insly AI assistants into any website. This widget provides a seamless way to integrate Insly's AI-powered support and sales assistance directly into your web applications.

Built with Solid.js for performance and flexibility, styled with Insly's brand colors and design system.

## Features

- 🎨 **Fully Customizable**: Extensive theming options for colors, fonts, and layout
- 📱 **Responsive Design**: Works seamlessly on desktop and mobile devices
- 🔒 **Secure Proxy Server**: Optional server to hide API keys and control access
- 💬 **Rich Chat Features**:
  - File uploads (images and documents)
  - Audio recording and speech-to-text
  - Streaming responses
  - Agent reasoning display
  - Source documents
  - Feedback system
  - Lead capture forms
  - Starter and follow-up prompts
- 🎯 **Two Integration Modes**:
  - Popup widget with floating button
  - Full-page chat interface

## Quick Start

### Option 1: Direct Integration

Add this to your HTML:

```html
<script type="module">
  import Chatbot from 'https://your-domain.com/web.js';

  Chatbot.init({
    chatflowid: 'chatflow_1',
    apiHost: 'https://ai.insly.ai',
    theme: {
      button: {
        backgroundColor: '#FF7D00',
        iconColor: 'white',
      },
      chatWindow: {
        title: 'Insly AI Assistant',
        welcomeMessage: 'Hello! How can I help you today?',
      },
    },
  });
</script>
```

### Option 2: Self-Hosted with Proxy Server

1. Clone the repository:

```bash
git clone https://github.com/insly/InslyAIChatWidget.git
cd InslyAIChatWidget
```

2. Install dependencies:

```bash
yarn install
```

3. Configure environment:

```bash
cp .env.example .env
```

Edit `.env`:

```env
API_HOST=https://ai.insly.ai
FLOWISE_API_KEY=your-api-key
chatflow_1=b1da4aa9-d66a-4f44-8ec5-4d157d061b1a,https://allowed-domain.com
chatflow_2=f0d7154c-285a-4d44-a917-b978d70e9500,https://allowed-domain.com
```

4. Start the proxy server:

```bash
yarn start
```

5. Embed in your website:

```html
<script type="module">
  import Chatbot from 'https://your-proxy-domain.com/web.js';

  Chatbot.init({
    chatflowid: 'chatflow_1',
    apiHost: 'https://your-proxy-domain.com',
  });
</script>
```

## Development

### Setup

```bash
# Install dependencies
yarn install

# Start development server
yarn dev

# Build for production
yarn build
```

### Project Structure

```
src/
├── features/          # Main chat implementations
│   ├── bubble/       # Popup widget
│   └── full/         # Full-page chat
├── components/       # Reusable UI components
│   ├── bubbles/     # Message bubbles
│   ├── buttons/     # Action buttons
│   ├── icons/       # SVG icons
│   └── inputs/      # Input components
├── assets/          # CSS and static assets
└── utils/           # Utility functions
```

## Customization

### Default Insly Theme

The widget comes pre-configured with Insly's brand colors and design system:

- **Primary Color**: Orange (#FF7D00)
- **Text Color**: Black (#121212)
- **Background**: White (#FFFFFF)
- **Bot Messages**: Light gray background (#F3F4F6)
- **Typography**: Inter font family
- **Border Radius**: 8px for modern appearance

### Theme Options

```javascript
Chatbot.init({
  chatflowid: 'chatflow_1',
  apiHost: 'https://ai.insly.ai',
  theme: {
    button: {
      backgroundColor: '#FF7D00',
      iconColor: 'white',
      size: 'medium', // 'small', 'medium', 'large', or number in pixels
      bottom: 20,
      right: 20,
      dragAndDrop: true,
    },
    chatWindow: {
      showTitle: true,
      title: 'Insly AI Assistant',
      titleAvatarSrc: 'https://example.com/avatar.png',
      titleTextColor: '#121212',
      titleBackgroundColor: '#FFFFFF',
      welcomeMessage: 'Hello! How can I help you today?',
      backgroundColor: '#FFFFFF',
      height: 700,
      width: 400,
      fontSize: 14,
      poweredByTextColor: '#666666',
      botMessage: {
        backgroundColor: '#F3F4F6',
        textColor: '#121212',
        showAvatar: true,
        avatarSrc: 'https://example.com/bot-avatar.png',
      },
      userMessage: {
        backgroundColor: '#FF7D00',
        textColor: '#FFFFFF',
        showAvatar: true,
        avatarSrc: 'https://example.com/user-avatar.png',
      },
      textInput: {
        placeholder: 'Type your message...',
        backgroundColor: '#FFFFFF',
        textColor: '#121212',
        sendButtonColor: '#FF7D00',
        maxChars: 1000,
        autoFocus: true,
        sendMessageSound: true,
      },
      feedback: {
        color: '#FF7D00',
      },
      footer: {
        showFooter: true,
        textColor: '#666666',
        text: 'Powered by',
        company: 'Insly',
        companyLink: 'https://insly.com',
      },
      dateTimeToggle: {
        date: true,
        time: true,
      },
    },
  },
});
```

### Custom CSS

You can add custom CSS through the theme:

```javascript
theme: {
  customCSS: `
    * {
      font-family: 'Inter', sans-serif !important;
    }
    
    [part="bot"] {
      border-radius: 8px !important;
    }
    
    button:hover {
      opacity: 0.9 !important;
    }
  `;
}
```

## Proxy Server Configuration

The proxy server provides enhanced security and access control:

### Environment Variables

```env
# Required
API_HOST=https://ai.insly.ai
FLOWISE_API_KEY=your-api-key-here

# Chatflow mappings (name=chatflowId,allowedDomain)
chatflow_1=b1da4aa9-d66a-4f44-8ec5-4d157d061b1a,https://insly.com
chatflow_2=f0d7154c-285a-4d44-a917-b978d70e9500,https://app.insly.com
```

### Features

- **Domain Whitelisting**: Restrict access to specific domains
- **API Key Protection**: Keep your Flowise API key secure
- **CORS Handling**: Proper cross-origin configuration
- **Request Validation**: Ensure only valid requests reach your AI backend

## Advanced Features

### File Uploads

Enable file uploads in your chatflow configuration:

```javascript
// Image uploads
uploadsConfig: {
  imgUploadSizeAndTypes: [
    { fileTypes: ['image/png', 'image/jpeg'], maxUploadSize: 5 }
  ],
  isImageUploadAllowed: true
}

// Document uploads
uploadsConfig: {
  fileUploadSizeAndTypes: [
    { fileTypes: ['application/pdf', 'text/plain'], maxUploadSize: 10 }
  ],
  isRAGFileUploadAllowed: true
}
```

### Lead Capture

Configure lead capture forms:

```javascript
leadsConfig: {
  status: true,
  title: 'Let us know how to contact you',
  name: true,
  email: true,
  phone: true,
  successMessage: 'Thank you! We\'ll be in touch soon.'
}
```

### Agent Reasoning

Display agent reasoning for AI workflows:

```javascript
theme: {
  chatWindow: {
    showAgentMessages: true;
  }
}
```

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

- Documentation: [https://docs.insly.com/ai-chat](https://docs.insly.com/ai-chat)
- Issues: [GitHub Issues](https://github.com/insly/InslyAIChatWidget/issues)
- Support: [support@insly.com](mailto:support@insly.com)

## Acknowledgments

Built with:

- [Solid.js](https://www.solidjs.com/) - Reactive UI framework
- [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS
- [Rollup](https://rollupjs.org/) - Module bundler
- [TypeScript](https://www.typescriptlang.org/) - Type safety
