# Installation Guide

Comprehensive guide for installing and setting up Puter on various systems.

## Table of Contents

- [System Requirements](#system-requirements)
- [Installation Methods](#installation-methods)
  - [From Source](#from-source)
  - [Docker](#docker)
  - [Self-Hosted](#self-hosted)
- [Troubleshooting](#troubleshooting)
- [Post-Installation](#post-installation)

## System Requirements

### Minimum Requirements
- **OS**: Windows, macOS, Linux, or any Unix-like system
- **Node.js**: v14.0.0 or higher
- **npm**: v6.0.0 or higher
- **RAM**: 512MB minimum
- **Disk Space**: 1GB minimum
- **Browser**: Modern browser (Chrome, Firefox, Safari, Edge)

### Recommended Requirements
- **OS**: Linux (Ubuntu 20.04+) or macOS 11+
- **Node.js**: v18.0.0 or higher
- **npm**: v8.0.0 or higher
- **RAM**: 2GB or more
- **Disk Space**: 2GB or more
- **CPU**: Multi-core processor

### Optional Dependencies
- **Docker**: v20.10+ (for containerized deployment)
- **Docker Compose**: v1.29+ (for orchestration)
- **Git**: v2.30+ (for version control)
- **Make**: For build automation

## Installation Methods

### From Source

#### Step 1: Clone Repository

```bash
# Using HTTPS
git clone https://github.com/ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources.git

# Using SSH
git clone git@github.com:ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources.git

# Navigate to directory
cd Platform-for-Unified-Technology-Execution-and-Resources
```

#### Step 2: Check Node.js Version

```bash
# Verify Node.js installation
node --version

# Should output: v14.0.0 or higher

# Verify npm installation
npm --version

# Should output: v6.0.0 or higher
```

#### Step 3: Install Dependencies

```bash
# Install root dependencies
npm install

# Install workspace dependencies
npm install --workspaces
```

#### Step 4: Build (Optional)

```bash
# Build GUI for production
npm run build
```

#### Step 5: Start Application

```bash
# Development mode with auto-reload
npm run start=gui

# Production mode with self-hosted setup
npm start
```

#### Step 6: Access Application

Open your browser and navigate to:
```
http://localhost:3000
```

### Docker

#### Step 1: Prerequisites

Ensure Docker is installed:

```bash
# Check Docker version
docker --version

# Should output: Docker version 20.10.0 or higher
```

#### Step 2: Build Docker Image

```bash
# Navigate to repository
cd Platform-for-Unified-Technology-Execution-and-Resources

# Build image
docker build -t puter:latest .

# Verify image creation
docker images | grep puter
```

#### Step 3: Run Container

```bash
# Basic run
docker run -d -p 3000:3000 --name puter-instance puter:latest

# With volume mount for persistence
docker run -d \
  -p 3000:3000 \
  -v puter-data:/app/volatile \
  --name puter-instance \
  puter:latest

# With environment variables
docker run -d \
  -p 3000:3000 \
  -e NODE_ENV=production \
  -e LOG_LEVEL=info \
  --name puter-instance \
  puter:latest
```

#### Step 4: Verify Container

```bash
# Check container status
docker ps | grep puter

# View logs
docker logs puter-instance

# Access application
# Open http://localhost:3000 in browser
```

#### Step 5: Additional Docker Commands

```bash
# Stop container
docker stop puter-instance

# Restart container
docker restart puter-instance

# Remove container
docker rm puter-instance

# Access container shell
docker exec -it puter-instance /bin/bash

# View real-time logs
docker logs -f puter-instance
```

### Docker Compose

#### Step 1: Create docker-compose.yml

```yaml
version: '3.8'

services:
  puter:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: puter-app
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - LOG_LEVEL=info
    volumes:
      - puter-data:/app/volatile
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000"]
      interval: 30s
      timeout: 10s
      retries: 3

volumes:
  puter-data:
    driver: local
```

#### Step 2: Deploy with Docker Compose

```bash
# Start services
docker-compose up -d

# View logs
docker-compose logs -f puter

# Stop services
docker-compose down

# Remove data
docker-compose down -v
```

### Self-Hosted

#### Step 1: Prepare Server

```bash
# Update system
sudo apt-get update && sudo apt-get upgrade -y

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify installation
node --version
npm --version
```

#### Step 2: Create Application Directory

```bash
# Create directory
sudo mkdir -p /opt/puter
cd /opt/puter

# Clone repository
sudo git clone https://github.com/ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources.git .

# Change ownership
sudo chown -R $USER:$USER /opt/puter
```

#### Step 3: Install Dependencies

```bash
cd /opt/puter
npm install --workspaces
npm run build
```

#### Step 4: Create Systemd Service

Create `/etc/systemd/system/puter.service`:

```ini
[Unit]
Description=Puter - Web-based Operating System
After=network.target

[Service]
Type=simple
User=puter
WorkingDirectory=/opt/puter
Environment="NODE_ENV=production"
ExecStart=/usr/bin/node /opt/puter/tools/run-selfhosted.js
Restart=always
RestartSec=10
StandardOutput=append:/var/log/puter/app.log
StandardError=append:/var/log/puter/error.log

[Install]
WantedBy=multi-user.target
```

#### Step 5: Enable and Start Service

```bash
# Create puter user
sudo useradd -m -s /bin/bash puter

# Create log directory
sudo mkdir -p /var/log/puter
sudo chown puter:puter /var/log/puter

# Reload systemd
sudo systemctl daemon-reload

# Enable service
sudo systemctl enable puter

# Start service
sudo systemctl start puter

# Check status
sudo systemctl status puter
```

#### Step 6: Configure Reverse Proxy (Nginx)

Create `/etc/nginx/sites-available/puter`:

```nginx
server {
    listen 80;
    server_name your-domain.com;
    
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Enable the site:

```bash
# Create symlink
sudo ln -s /etc/nginx/sites-available/puter /etc/nginx/sites-enabled/

# Test configuration
sudo nginx -t

# Reload nginx
sudo systemctl reload nginx
```

## Troubleshooting

### Port Already in Use

```bash
# Find process using port 3000
lsof -i :3000

# Kill process
kill -9 <PID>

# Or use different port
PORT=3001 npm start
```

### Permission Denied Error

```bash
# Fix directory permissions
chmod -R 755 Platform-for-Unified-Technology-Execution-and-Resources
chmod -R 755 volatile/

# Or run with sudo (not recommended)
sudo npm start
```

### Module Not Found Error

```bash
# Clean install
rm -rf node_modules package-lock.json
npm cache clean --force
npm install
```

### High Memory Usage

```bash
# Increase Node.js heap size
NODE_OPTIONS="--max-old-space-size=2048" npm start
```

### Docker Build Fails

```bash
# Clean Docker cache
docker system prune -a

# Rebuild
docker build --no-cache -t puter:latest .
```

## Post-Installation

### Initial Setup

1. **Access Application**
   - Open http://localhost:3000
   - Create admin account
   - Configure settings

2. **Update Configuration**
   - Edit configuration files
   - Set up storage
   - Configure security

3. **Verify Installation**
   ```bash
   # Run tests
   npm test
   
   # Check system health
   curl http://localhost:3000/health
   ```

### Maintenance

```bash
# Update dependencies
npm update

# Check for security vulnerabilities
npm audit

# Fix vulnerabilities
npm audit fix

# View logs
tail -f /var/log/puter/app.log
```

### Backup

```bash
# Backup volatile directory
tar -czf puter-backup-$(date +%Y%m%d).tar.gz volatile/

# Backup entire installation
tar -czf puter-full-backup-$(date +%Y%m%d).tar.gz .
```

## Next Steps

- Read [README.md](README.md) for project overview
- Check [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines
- Review [API documentation](docs/API.md)
- Explore [examples](examples/)

## Support

- 📖 [Documentation](https://puter.com/docs)
- 🐛 [Report Issues](https://github.com/ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources/issues)
- 💬 [Discussions](https://github.com/ImSuvodeep/Platform-for-Unified-Technology-Execution-and-Resources/discussions)

---

**Happy Installing! 🎉**
