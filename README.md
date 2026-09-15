# 🌐 Puter - Platform for Unified Technology, Execution, and Resources

[![License](https://img.shields.io/badge/License-AGPL3.0-blue.svg)](LICENSE)
[![Node.js](https://img.shields.io/badge/Node.js-v14%2B-green.svg)](https://nodejs.org/)
[![JavaScript](https://img.shields.io/badge/JavaScript-75.7%25-yellow.svg)]()
[![Docker](https://img.shields.io/badge/Docker-Supported-blue.svg)]()

> **A modern, web-based operating system that brings traditional OS power and flexibility into your browser.**

Puter is a feature-rich, cloud-first web platform designed to provide a unified interface for managing files, running applications, and accessing online resources—all from any device, anywhere. Built with modern web technologies, Puter delivers a desktop-like experience in the browser with zero installation required.

---

## 🚀 Quick Start

### Try It Live
Access the live demo: [https://bit.ly/4mssb9b](https://bit.ly/4mssb9b)

### Installation (5 minutes)

```bash
# Clone the repository
git clone https://github.com/ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources.git
cd Platform-for-Unified-Technology-Execution-and-Resources

# Install dependencies
npm install --workspaces

# Start development server
npm run start=gui

# Access in browser
# http://localhost:3000
```

For detailed installation instructions, see [INSTALL.md](INSTALL.md)

---

## ✨ Key Features

- **📁 File Management** - Browse, create, edit, and manage files with an intuitive file explorer
- **🎨 Desktop Environment** - Familiar desktop-like interface with windows, taskbar, and system tray
- **🔧 Extensible Architecture** - Modular system with support for custom applications and plugins
- **☁️ Cloud-Ready** - Self-hosted or cloud deployment with persistent storage
- **🔐 Secure** - Built-in security features and access controls
- **⚡ Fast & Responsive** - Optimized performance with modern web technologies
- **🌍 Cross-Platform** - Works on any device with a modern web browser
- **🔌 Plugin System** - Extend functionality through mods and custom packages

---

## 📋 System Requirements

### Minimum
- **OS**: Windows, macOS, Linux, or any Unix-like system
- **Node.js**: v14.0.0 or higher
- **npm**: v6.0.0 or higher
- **RAM**: 512MB minimum
- **Disk Space**: 1GB minimum
- **Browser**: Modern browser (Chrome, Firefox, Safari, Edge)

### Recommended
- **OS**: Linux (Ubuntu 20.04+) or macOS 11+
- **Node.js**: v18.0.0 or higher
- **npm**: v8.0.0 or higher
- **RAM**: 2GB or more
- **Disk Space**: 2GB or more
- **CPU**: Multi-core processor

---

## 📁 Project Structure

```
Platform-for-Unified-Technology-Execution-and-Resources/
├── src/                          # Source code
│   ├── gui/                      # Frontend GUI (JavaScript/HTML/CSS)
│   ├── backend/                  # Backend services
│   ├── phoenix/                  # Core engine
│   └── ...
├── mods/                         # Custom modules and extensions
│   └── kdmod/                    # Kernel development module
├── mod_packages/                 # Packaged mods for distribution
├── experiments/                  # Experimental features
│   └── js-parse-and-output/     # JavaScript parsing utilities
├── test/                         # Test suites
├── volatile/                     # Runtime data storage
│   └── Contains all saved Puter data (unless using /etc and /var)
├── tools/                        # Build and automation scripts
├── badges/                       # Badge assets
├── awesome/                      # Community resources and links
├── package.json                  # Project dependencies
├── index.html                    # Entry point
├── API.md                        # API documentation
├── INSTALL.md                    # Installation guide
├── SECURITY.md                   # Security guidelines
├── LICENSE                       # AGPL-3.0 License
└── TRADEMARK.md                  # Trademark information
```

### Key Directories Explained

| Directory | Purpose |
|-----------|---------|
| **src/** | All source code including frontend, backend, and core systems |
| **mods/** | Developer modules for extending Puter functionality |
| **mod_packages/** | Pre-packaged, distributable extensions |
| **experiments/** | Research and experimental features |
| **test/** | Unit and integration tests |
| **volatile/** | Persistent storage for application data |
| **tools/** | Build scripts and utilities |

---

## 🛠️ Technology Stack

### Frontend (75.7%)
- **JavaScript** - Core application logic
- **HTML** - Markup and structure
- **Webpack** - Module bundling and optimization
- **Modern Browser APIs** - WebGL, WebSockets, File APIs

### Backend
- **Node.js** - Server runtime
- **Express.js** - HTTP server framework
- **Redis** - Data caching (ioredis)
- **PostgreSQL/MySQL** - Database (via drivers)

### DevOps (7.5%)
- **Docker** - Container virtualization
- **Docker Compose** - Multi-container orchestration

### Build Tools
- **ESLint** - Code quality and style
- **Mocha** - Testing framework
- **Webpack CLI** - Build automation
- **Nodemon** - Development auto-reload

### Additional Tools (4.2%)
- **C++/C** - Performance-critical components
- **Shell Scripts** - Automation

---

## 📦 Installation Methods

### 1. Development (npm)
```bash
npm install --workspaces
npm run start=gui
```

### 2. Production (Self-Hosted)
```bash
npm install --workspaces
npm run build
npm start
```

### 3. Docker
```bash
docker build -t puter:latest .
docker run -d -p 3000:3000 puter:latest
```

### 4. Docker Compose
```bash
docker-compose up -d
```

For comprehensive instructions, see [INSTALL.md](INSTALL.md)

---

## 📖 Documentation

| Document | Purpose |
|----------|---------|
| [INSTALL.md](INSTALL.md) | Complete installation guide for all platforms |
| [API.md](API.md) | API endpoints and integration guide |
| [SECURITY.md](SECURITY.md) | Security features and best practices |
| [TRADEMARK.md](TRADEMARK.md) | Trademark and branding guidelines |

---

## 🚀 Available Commands

| Command | Description |
|---------|-------------|
| `npm install` | Install root and workspace dependencies |
| `npm run start=gui` | Start development server with hot-reload |
| `npm start` | Start production self-hosted server |
| `npm run build` | Build GUI for production |
| `npm test` | Run all test suites |
| `npm run check-translations` | Verify translation files |

---

## 🎯 Project Goals

- ✅ Create a powerful, open-source web OS
- ✅ Eliminate installation barriers (works in any modern browser)
- ✅ Provide professional-grade file and resource management
- ✅ Enable seamless app execution and plugin development
- ✅ Maintain security and privacy standards
- ✅ Support self-hosted and cloud deployments
- ✅ Build an active, contributing community

---

## 🤝 Contributing

We welcome contributions! Please see our contribution guidelines for:
- Reporting bugs
- Submitting feature requests
- Making code contributions
- Creating extensions and mods

Visit our [GitHub Issues](https://github.com/ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources/issues) to get started.

---

## 📜 License

This project is licensed under the **AGPL-3.0** License. See [LICENSE](LICENSE) file for details.

- **AGPL-3.0**: Copyleft license requiring derivative works to be open-source
- Personal and commercial use permitted
- Contributions welcome from the community
- See [TRADEMARK.md](TRADEMARK.md) for trademark information

---

## 🔐 Security

Security is our priority. Please refer to [SECURITY.md](SECURITY.md) for:
- Security features and architecture
- Best practices for deployment
- Vulnerability reporting procedures
- Data privacy and protection

---

## 🌟 Roadmap & Vision

### Short Term (v2.5+)
- Enhanced performance optimizations
- Expanded plugin ecosystem
- Improved mobile responsiveness
- Additional built-in applications

### Long Term
- Full-featured office suite
- Advanced collaboration tools
- AI-powered features
- Enhanced multimedia support
- Enterprise-grade features

---

## 💬 Community & Support

- **GitHub Issues**: [Report bugs & request features](https://github.com/ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources/issues)
- **GitHub Discussions**: [Join community conversations](https://github.com/ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources/discussions)
- **Documentation**: [Full docs and guides](https://puter.com/docs)
- **Live Demo**: [Try it online](https://bit.ly/4mssb9b)

---

## 📊 Project Statistics

| Metric | Value |
|--------|-------|
| **Primary Language** | JavaScript (75.7%) |
| **License** | AGPL-3.0 |
| **Node.js Version** | v14.0.0+ |
| **Repository Size** | ~563 KB |
| **Latest Version** | 2.5.1 |
| **Status** | Active Development |

---

## 🎓 Learning Resources

- **Official Website**: [puter.com](https://puter.com)
- **API Documentation**: [API.md](API.md)
- **Installation Guide**: [INSTALL.md](INSTALL.md)
- **Development Setup**: See Quick Start above
- **Code Examples**: [examples/](examples/) directory

---

## 🐛 Troubleshooting

### Common Issues

**Port 3000 already in use?**
```bash
PORT=3001 npm start
```

**Module not found?**
```bash
npm cache clean --force
npm install --workspaces
```

**High memory usage?**
```bash
NODE_OPTIONS="--max-old-space-size=2048" npm start
```

For more troubleshooting, see [INSTALL.md#troubleshooting](INSTALL.md#troubleshooting)

---

## ✅ Development Workflow

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** changes (`git commit -m 'Add AmazingFeature'`)
4. **Push** to branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

---

## 📝 Version History

- **v2.5.1** - Latest release with performance improvements
- **v2.5.0** - Enhanced UI and new features
- **v2.4.x** - Stability and bug fixes
- **v2.0.x** - Major redesign

---

## 🙏 Acknowledgments

- Thanks to all contributors and community members
- Special thanks to [Puter Technologies Inc.](https://puter.com)
- Powered by the open-source community

---

## 📧 Contact

For inquiries or support:
- **GitHub**: [@ImSuvodeep](https://github.com/ImSuvodeep)
- **Project**: [Platform for Unified Technology, Execution, and Resources](https://github.com/ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources)
- **Website**: [puter.com](https://puter.com)

---

<div align="center">

**Made with ❤️ by the Puter Community**

[⬆ back to top](#-puter---platform-for-unified-technology-execution-and-resources)

</div>
