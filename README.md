<h1 align="center">Moonfin for webOS</h1>
<h3 align="center">Enhanced Jellyfin client for LG Smart TVs</h3>

---

<p align="center">
  <img alt="Moonfin for webOS" src="frontend/assets/splash.png" />
</p>

[![License](https://img.shields.io/github/license/Moonfin-Client/webOS.svg)](https://github.com/Moonfin-Client/webOS)
[![Release](https://img.shields.io/github/release/Moonfin-Client/webOS.svg)](https://github.com/Moonfin-Client/webOS/releases)

<a href="https://www.buymeacoffee.com/moonfin" target="_blank"><img src="https://github.com/user-attachments/assets/fe26eaec-147f-496f-8e95-4ebe19f57131" alt="Buy Me A Coffee" ></a>

> **[← Back to main Moonfin project](https://github.com/Moonfin-Client)**

Moonfin for webOS is an enhanced fork of the official Jellyfin webOS client, optimized for the viewing experience on LG Smart TVs running webOS.

## Features & Enhancements

Moonfin for webOS builds on the solid foundation of Jellyfin with targeted improvements for TV viewing:

### Cross-Server Content Playback
- **Unified Library Support** - Seamless playback from multiple Jellyfin servers
- Seamless switching between servers for content playback
- Improved server selection logic

### Jellyseerr Integration (Beta)

Moonfin is the first webOS client with native Jellyseerr support.

- Browse trending, popular, and recommended movies/shows and filter content by Series/Movie Genres, Studio, Network, and keywords
- Request content in HD or 4K directly from your LG TV
- **NSFW Content Filtering** (optional) using Jellyseerr/TMDB metadata
- Smart season selection when requesting TV shows
- View all your pending, approved, and available requests
- Authenticate using your Jellyfin login (permanent local API key saved)
- Global search includes Jellyseerr results
- Rich backdrop images for a more cinematic discovery experience

### 🧭 Enhanced Navigation
- Quick access home button and search functionality
- Shuffle button for instant random movie/TV show discovery
- Genres menu to browse all media by genre in one place
- Dynamic library buttons automatically populate based on your Jellyfin libraries
- One-click navigation to any library or collection directly from the navbar
- Cleaner icon-based design for frequently used actions

### 🎵 Playback & Media Control
- **Theme Music Playback** - Background theme music support for TV shows and movies with volume control
- **Pre-Playback Track Selection** - Choose your preferred audio track and subtitle before playback starts (configurable in settings)
- **Next Episode Countdown** - Skip button shows countdown timer when next episode is available

### 📊 Improved Details Screen
- Metadata organized into clear sections: genres, directors, writers, studios, and runtime
- Taglines displayed above the description where available
- Cast photos appear as circles for a cleaner look
- Fits more useful information on screen without feeling cramped

### 🎨 UI Polish
- **Accent Color Customization** - Personalize the UI with your preferred accent color
- Item details show up right in the row, no need to open every title to see what it is
- Buttons look better when not focused (transparent instead of distracting)
- Better contrast makes text easier to read
- Transitions and animations feel responsive
- Consistent icons and visual elements throughout

---

## Installation

### Pre-built Releases
Download the latest IPK from the [Releases page](https://github.com/Moonfin-Client/webOS/releases).

**Supported Devices:**
- LG Smart TVs running webOS 3.0+
- LG webOS TVs (2016 and newer models)

### Jellyseerr Setup (Optional)
To enable media discovery and requesting:

1. Install and configure Jellyseerr on your network ([jellyseerr.dev](https://jellyseerr.dev))
2. In Moonfin, go to **Settings → Jellyseerr**
3. Enter your Jellyseerr server URL (e.g., `http://192.168.1.100:5055`)
4. Click **Connect with Jellyfin** and enter your Jellyfin password
5. Test the connection, then start discovering!

Your session is saved securely and will reconnect automatically.

### Sideloading Instructions
1. Enable Developer Mode on your LG TV
2. Install the webOS Dev Mode app from the LG Content Store
3. Use the ares-cli tools to install the IPK (see Building from Source section)

---

## Building from Source

### Prerequisites
- Node.js and npm
- webOS SDK (ares-cli tools)

There are three ways to create the required build environment:

- Full webOS SDK Installation
- Docker
- NPM ares-cli

### Full webOS SDK Installation

Install the webOS SDK from http://webostv.developer.lge.com/sdk/installation/

### Docker

A prebuilt docker image is available that includes the build and deployment dependencies, see [Docker Hub](https://ghcr.io/oddstr13/docker-tizen-webos-sdk).

### Managing the ares-tools via npm

This requires `npm`, the Node.js package manager.

Execute the following to install the required webOS toolkit for building & deployment:

```bash
npm install
```

Now you can package the app by running:

```bash
npm run package
```

### Building with Docker or webOS SDK

`dev.sh` is a wrapper around the Docker commands. If you have installed the SDK directly, just omit that part.

```bash
# Build the package via Docker
./dev.sh ares-package --no-minify services frontend

# Build the package with natively installed webOS SDK
ares-package --no-minify services frontend
```

---

## Development

### Developer Notes
- Uses npm for dependency management
- webOS SDK or Docker recommended for development
- Code style follows upstream Jellyfin conventions
- UI changes should be tested on actual LG TV devices when possible

### Testing on TV

Testing on a TV requires [registering a LG developer account](https://webostv.developer.lge.com/develop/app-test/preparing-account/) and [setting up the devmode app](https://webostv.developer.lge.com/develop/app-test/using-devmode-app/).

Once you have installed the devmode app on your target TV and logged in with your LG developer account, you need to turn on the `Dev Mode Status` and `Key Server`.
**Make sure** to take a note of the passphrase.

```bash
# Add your TV. The defaults are fine, but I recommend naming it `tv`.
./dev.sh ares-setup-device --search

# This command sets up the SSH key for the device `tv` (Key Server must be running)
./dev.sh ares-novacom --device tv --getkey

# Run this command to verify that things are working.
./dev.sh ares-device-info -d tv

# This command installs the app. Remember to build it first.
./dev.sh ares-install -d tv org.moonfin.webos_*.ipk

# Launch the app and the web developer console.
./dev.sh ares-inspect -d tv org.moonfin.webos

# Or just launch the app.
./dev.sh ares-launch -d tv org.moonfin.webos
```

---

## Contributing

We welcome contributions to Moonfin for webOS!

### Guidelines
1. **Check existing issues** - See if your idea/bug is already reported
2. **Discuss major changes** - Open an issue first for significant features
3. **Follow code style** - Match the existing codebase conventions
4. **Test on TV devices** - Verify changes work on actual LG TV hardware
5. **Consider upstream** - Features that benefit all users should go to Jellyfin first!

### Pull Request Process
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes with clear commit messages
4. Test thoroughly on LG TV devices
5. Submit a pull request with a detailed description

---

## Support & Community

- **Issues** - [GitHub Issues](https://github.com/Moonfin-Client/webOS/issues) for bugs and feature requests
- **Discussions** - [GitHub Discussions](https://github.com/Moonfin-Client/webOS/discussions) for questions and ideas
- **Upstream Jellyfin** - [jellyfin.org](https://jellyfin.org) for server-related questions

---

## Credits

Moonfin for webOS is built upon the excellent work of:

- **[Jellyfin Project](https://jellyfin.org)** - The foundation and upstream codebase
- **Jellyfin webOS Contributors** - All the developers who built the original client
- **Moonfin Contributors** - Everyone who has contributed to this fork

---

## License

This project inherits the MPL 2.0 license from the upstream Jellyfin webOS project. Some parts incorporate content licensed under the Apache 2.0 license. All images are taken from and licensed under the same license as https://github.com/jellyfin/jellyfin-ux. See the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <strong>Moonfin for webOS</strong> is an independent fork and is not affiliated with the Jellyfin project.<br>
  <a href="https://github.com/Moonfin-Client">← Back to main Moonfin project</a>
</p>
