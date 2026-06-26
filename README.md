# 🧮 Claude Counter

> **Live token counting, cache tracking, and precise usage analytics for Claude.ai**  
> A lightweight browser extension that brings transparency to your Claude API consumption with real-time insights and accurate progress tracking.

---

## ✨ Features at a Glance

<table>
  <tr>
    <td width="50%">
      <h4>📊 Live Token Counter</h4>
      <p>Approximate token count for your current conversation with a mini progress bar against the 200k context limit. Know exactly how much of your context window you're using.</p>
    </td>
    <td width="50%">
      <h4>⏰ Cache Timer</h4>
      <p>Real-time countdown showing how long your conversation remains cached (cheaper to continue). Plan your work with cost-efficiency in mind.</p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h4>📈 Accurate Usage Bars</h4>
      <p>Session (5-hour) and weekly (7-day) usage from Claude's native API. More accurate than the rounded /usage page with exact progress bars and reset countdowns.</p>
    </td>
    <td width="50%">
      <h4>🔒 Privacy First</h4>
      <p>All data stays local—no external servers, no tracking, no ads. Fully open source and MIT licensed.</p>
    </td>
  </tr>
</table>

---

## 🚀 Installation

### Chrome / Edge / Chromium

1. **Download the extension**
   - Go to [Releases](../../releases) and download `claude-counter-0.4.2.zip`
   
2. **Enable Developer Mode**
   - Open `chrome://extensions` in your browser
   - Toggle **Developer mode** (top-right corner)

3. **Install**
   - Drag and drop the `claude-counter-0.4.2.zip` file onto the extensions page
   - Click **Add extension** when prompted
   - The extension icon will appear in your toolbar

### Firefox

1. **Download the extension**
   - Go to [Releases](../../releases) and download `claude-counter-0.4.2.xpi`

2. **Install**
   - Drag the `.xpi` file into any Firefox window
   - Click **Add** in the confirmation dialog
   - The extension is now active on claude.ai

### Userscript (Any Browser + Script Manager)

For browsers without native extension support or if you prefer a script-based approach:

1. **Install a Script Manager**
   - [Tampermonkey](https://www.tampermonkey.net/) (Chrome, Firefox, Edge, Opera, Safari)
   - [Greasemonkey](https://www.greasespot.net/) (Firefox)
   - [Violentmonkey](https://violentmonkey.github.io/) (Chrome, Firefox, Edge, Opera, Safari)

2. **Add the Script**
   - Click [here](./userscript/claude-counter.user.js) to open the userscript
   - Your script manager will detect it
   - Click **Install** and confirm

---

## 💡 How It Works

The extension operates silently in the background, providing real-time insights:

- **API Interception**: Intercepts Claude's API responses to extract conversation data and usage information
- **Smart Tokenization**: Uses a vendored tokenizer (`o200k_base`) for accurate token counting
- **Live Accuracy**: Leverages Claude's `/usage` endpoint plus real-time SSE `message_limit` data to provide exact, unrounded utilization fractions—making progress bars more accurate than the rounded percentages on the native /usage page
- **DOM Injection**: Watches for page changes and injects UI elements as you navigate claude.ai
- **Zero Network Overhead**: Makes requests only to claude.ai—no external servers

---

## 🎨 Visual Preview

![Claude Counter Interface](./claude-counter-my-own/screenshot.png)

The extension displays three key metrics right on the claude.ai interface:
- **Token Progress Bar**: Shows current context usage
- **Cache Status**: Displays cache expiration countdown
- **Usage Analytics**: Session and weekly usage bars with reset timers

---

## 🔐 Privacy & Security

✅ **Completely Private**
- All processing happens locally in your browser
- No data is sent to external servers
- No tracking, analytics, or third-party integrations

✅ **Minimal Permissions**
- Reads your `lastActiveOrg` cookie to query Claude's `/usage` endpoint
- Makes requests only to `claude.ai`
- No access to browsing history or personal files

✅ **Open Source & Auditable**
- Source code available for security review
- MIT License—free for personal and commercial use

---

## 📦 What's Included

```
claude-counter-my-own/
├── manifest.json              # Extension configuration (Manifest v3)
├── src/
│   ├── content/              # Content scripts that run on claude.ai
│   │   ├── main.js           # Entry point and orchestration
│   │   ├── ui.js             # UI rendering and injection
│   │   ├── tokens.js         # Token counting logic
│   │   ├── bridge-client.js  # Communication with injected scripts
│   │   └── constants.js      # Configuration and constants
│   ├── injected/             # Scripts injected into the page context
│   │   └── bridge.js         # Bridge for API access
│   ├── vendor/               # Third-party dependencies
│   │   └── o200k_base.js     # GPT tokenizer
│   └── styles.css            # UI styling
├── icons/                     # Extension icons (16, 32, 48, 96, 128, 256px)
├── README.md                  # This file
└── LICENSE                    # MIT License
```

---

## 🛠️ Usage Tips

### Maximize Accuracy
- Keep the extension enabled for the most accurate token counting
- Use it to monitor cache status and plan longer conversations during cache windows
- Track your weekly usage to stay within your quota

### Cost Optimization
- Use the cache timer to determine when to continue vs. start a new conversation
- Session-based tracking helps you understand peak usage times
- Compare the exact usage bars with Claude's native /usage page to spot discrepancies

### Troubleshooting
- **Extension not showing**: Refresh the claude.ai page after installation
- **Inaccurate tokens**: Token counting is approximate; exact counts depend on Claude's tokenizer version
- **Missing data**: Ensure cookies are enabled for claude.ai

---

## 📊 Technical Details

### Architecture

The extension uses a secure three-layer architecture:

1. **Content Script** (`src/content/*.js`)
   - Runs in the page context
   - Intercepts API responses
   - Injects UI elements

2. **Injected Script** (`src/injected/bridge.js`)
   - Runs in the main page context with full API access
   - Bridges data between the page and extension scripts

3. **UI Layer** (`src/styles.css`)
   - Minimal, responsive styling
   - Seamless integration with Claude's interface

### Token Counting

- Uses the `o200k_base` tokenizer (same as Claude's native implementation)
- Tokenizes message content in real-time
- Provides approximate counts; exact counts are available in Claude's API

### Data Sources

- **Tokens**: Message content from conversation API responses
- **Cache Status**: Server response headers and SSE message data
- **Usage**: Claude's `/usage` endpoint (requires authentication)

---

## 📝 Credits

- **Token Counting**: [gpt-tokenizer](https://github.com/niieani/gpt-tokenizer) by niieani (MIT License)
- **Inspiration**: [Claude Usage Tracker](https://github.com/lugia19/Claude-Usage-Extension) by lugia19
- **Icons**: Custom design for modern, minimalist aesthetic

---

## 📄 License

This project is licensed under the **MIT License**—see the [LICENSE](./LICENSE) file for details.

```
MIT License - You are free to use, modify, and distribute this software
for any purpose, personal or commercial. See LICENSE file for full terms.
```

---

## 🚦 Getting Started Checklist

- [ ] Download the extension from [Releases](../../releases)
- [ ] Install for your browser (Chrome, Firefox, or via Userscript)
- [ ] Visit [claude.ai](https://claude.ai)
- [ ] Look for the Claude Counter widget in the interface
- [ ] Enable "Developer mode" in your browser (Chrome/Edge) if needed
- [ ] Start tracking your tokens, cache status, and usage!

---

## 🐛 Issues & Feedback

Found a bug or have a feature request? 
- Open an [Issue](../../issues) with detailed information
- Include your browser and Claude Counter version
- Describe the expected vs. actual behavior

---

## 🤝 Contributing

We welcome contributions! To get started:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/your-feature`)
3. **Commit** your changes (`git commit -am 'Add feature'`)
4. **Push** to the branch (`git push origin feature/your-feature`)
5. **Submit** a pull request with a clear description

---

## 📞 Support

- **Questions?** Check the [Issues](../../issues) for existing Q&A
- **Privacy concerns?** Review the [Privacy & Security](#-privacy--security) section
- **Feature suggestions?** [Create an issue](../../issues/new) with the `enhancement` label

---

<div align="center">

**Made with ❤️ for the Claude community**

[⭐ Star this repo](../../stargazers) if you find it useful!

</div>
