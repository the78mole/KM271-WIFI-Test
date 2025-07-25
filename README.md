# KM271-WIFI Firmware

[![Build and Release](https://github.com/the78mole/KM271-WIFI-Test/actions/workflows/release.yaml/badge.svg)](https://github.com/the78mole/KM271-WIFI-Test/actions/workflows/release.yaml)
[![Latest Release](https://img.shields.io/github/v/release/the78mole/KM271-WIFI-Test?label=Release&color=success)](https://github.com/the78mole/KM271-WIFI-Test/releases/latest)
[![GitHub Downloads](https://img.shields.io/github/downloads/the78mole/KM271-WIFI-Test/total?label=Downloads&color=blue)](https://github.com/the78mole/KM271-WIFI-Test/releases)
[![PlatformIO CI](https://img.shields.io/badge/PlatformIO-CI-orange.svg)](https://platformio.org/)
[![ESP32](https://img.shields.io/badge/ESP32-Espressif-red.svg)](https://www.espressif.com/en/products/socs/esp32)
[![License](https://img.shields.io/github/license/the78mole/KM271-WIFI-Test?color=lightgrey)](LICENSE)
[![GitHub Issues](https://img.shields.io/github/issues/the78mole/KM271-WIFI-Test?color=yellow)](https://github.com/the78mole/KM271-WIFI-Test/issues)
[![GitHub Stars](https://img.shields.io/github/stars/the78mole/KM271-WIFI-Test?style=social)](https://github.com/the78mole/KM271-WIFI-Test/stargazers)

ESP32-based test firmware for the KM271-WIFI project - a WiFi interface for Buderus heating systems with KM271 communication module.

**🧪 This is a test program** that works standalone without requiring a Buderus heating system. It demonstrates basic ESP32 functionality with LED blinking and hardware revision detection.

**📋 Perfect ESP32 Template**: This project serves as an excellent template for your own ESP32 projects, featuring a complete CI/CD pipeline with automated building, testing, and releasing via GitHub Actions.

## 🚀 Features

- **🧪 Standalone Test Program**: Works without Buderus heating system - perfect for testing and development
- **📋 ESP32 Project Template**: Ready-to-use template with complete CI/CD pipeline for your own projects
- **ESP32-based**: Built on the robust ESP32 platform
- **Hardware Revision Support**: Configurable for different hardware revisions
- **PlatformIO**: Professional development environment
- **Automated CI/CD**: GitHub Actions workflow for building and releasing
- **Factory Images**: Complete flash images for new devices
- **Multi-Environment**: Support for different hardware configurations

## 📋 Hardware Requirements

### For Testing (Standalone)
- ESP32 Development Board (ESP32-WROOM-32 or compatible)
- USB cable for programming and power
- **LED connected to GPIO 2** (or modify `src/main.cpp` for your board's built-in LED)
- **No additional hardware required** - runs standalone for testing

> **💡 Note**: Most ESP32 development boards have a built-in LED on GPIO 2. If your board uses a different pin, check the board documentation or modify the `LED_PIN` definition in `src/main.cpp`.

### For Production Use
- ESP32 Development Board (ESP32-WROOM-32 or compatible)
- KM271-WIFI PCB (Hardware Revision 0.0.6 or compatible)
- Buderus heating system with KM271 communication module

## 🛠️ Development Setup

### Prerequisites

- [PlatformIO Core](https://platformio.org/install/cli) or [PlatformIO IDE](https://platformio.org/platformio-ide)
- Git
- Python 3.x (for esptool)

### Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/the78mole/KM271-WIFI-Test.git
   cd KM271-WIFI-Test
   ```

2. **Build the firmware:**
   ```bash
   # Build for all environments
   platformio run
   
   # Build for specific environment
   platformio run -e esp32dev
   ```

3. **Upload to device:**
   ```bash
   # Upload firmware
   platformio run -t upload
   
   # Upload and monitor serial output
   platformio run -t upload -t monitor
   ```

### Project Structure

```
KM271-WIFI-Test/
├── src/                    # Source code
│   └── main.cpp           # Main application
├── include/               # Header files
├── lib/                   # Private libraries
├── test/                  # Unit tests
├── .github/workflows/     # CI/CD workflows
├── platformio.ini         # PlatformIO configuration
└── README.md             # This file
```

## ⚙️ Configuration

### Hardware Revision

The firmware supports different hardware revisions through build flags in `platformio.ini`:

```ini
[env:esp32dev]
platform = espressif32
board = esp32dev
framework = arduino
build_flags = -DHW_REV=000006  ; Hardware Revision 0.0.6
```

### Adding New Hardware Revisions

To add support for a new hardware revision:

1. Add a new environment in `platformio.ini`:
   ```ini
   [env:esp32dev_rev007]
   platform = espressif32
   board = esp32dev
   framework = arduino
   build_flags = -DHW_REV=000007  ; Hardware Revision 0.0.7
   ```

2. The CI/CD workflow will automatically build binaries for all environments.

## 🏗️ Using as ESP32 Project Template

This project is designed to serve as a comprehensive template for ESP32 projects with PlatformIO. Here's what you get out of the box:

### 🎯 **Ready-to-Use CI/CD Pipeline**
- **GitHub Actions workflow** with automated building and releasing
- **Docker-based builds** ensuring consistent build environment
- **Multi-environment support** for different hardware configurations
- **Semantic versioning** with automatic version bumping
- **Factory image creation** with correct ESP32 flash offsets

### 🚀 **To Use as Template:**

1. **Fork or use as template** on GitHub
2. **Customize `platformio.ini`** for your hardware requirements
3. **Replace `src/main.cpp`** with your application code
4. **Update build flags** (e.g., `HW_REV`) as needed
5. **Push to main branch** → Automatic build and release! 🎉

### 💡 **What Works Out of the Box:**
- ✅ LED blinking test program (works on any ESP32 with LED on GPIO 2)
- ✅ Hardware revision detection and configuration
- ✅ Professional build pipeline with artifact creation
- ✅ Factory images for production deployment
- ✅ Release notes generation with flash instructions

### 🔧 **Easy Customization:**
```ini
# Add your own environments in platformio.ini
[env:my_custom_board]
platform = espressif32
board = esp32dev
framework = arduino
build_flags = -DMY_CUSTOM_FLAG=123
```

The CI/CD workflow will automatically detect and build all environments!

## 📦 Releases

### Automated Releases

The project uses GitHub Actions for automated building and releasing:

- **Triggers**: Push to `main` branch or manual workflow dispatch
- **Semantic Versioning**: Automatic version bumping based on commit messages
- **Multi-Environment**: Builds firmware for all configured environments
- **Factory Images**: Creates complete flash images with bootloader, partitions, and firmware

### Release Artifacts

Each release includes:

- **Firmware Binaries**: `KM271-WIFI-{env}-firmware-v{version}.bin`
- **Factory Images**: `KM271-WIFI-{env}-factory-v{version}.bin`
- **Debug Symbols**: `KM271-WIFI-{env}-firmware-v{version}.elf`

### Commit Message Convention

Use conventional commits for automatic version bumping:

- `feat: new feature` → Minor version bump
- `fix: bug fix` → Patch version bump
- `feat!: breaking change` → Major version bump
- `fix!: breaking fix` → Major version bump

## 🔧 Flashing Instructions

### For New Devices (Factory Image)

Use the factory image to flash a completely new device:

```bash
esptool --chip esp32 --port /dev/ttyUSB0 --baud 921600 \
  write_flash 0x0 KM271-WIFI-esp32dev-factory-v{version}.bin
```

### For Firmware Updates

For devices with existing bootloader and partitions:

```bash
esptool --chip esp32 --port /dev/ttyUSB0 --baud 921600 \
  write_flash 0x10000 KM271-WIFI-esp32dev-firmware-v{version}.bin
```

### Using PlatformIO

```bash
# Flash firmware via PlatformIO
platformio run -t upload

# Erase flash completely
platformio run -t erase

# Monitor serial output
platformio device monitor
```

## 🔍 Debugging

### Serial Monitor

Connect to the serial console to view debug output:

```bash
# Using PlatformIO
platformio device monitor

# Using minicom (Linux)
minicom -D /dev/ttyUSB0 -b 115200

# Using screen (macOS/Linux)
screen /dev/ttyUSB0 115200
```

### Hardware Revision Detection

The firmware automatically detects the hardware revision at runtime and configures the appropriate GPIO pins. Check the serial output for:

```
Hardware Revision: 0.0.6
LED Pin: 2
```

**GPIO Pin Assignments by Hardware Revision:**
- **HW_REV 000006**: LED on GPIO 2 (most ESP32 dev boards)
- **Other revisions**: Add your pin assignments in `src/main.cpp`

If the LED doesn't blink, check:
1. Your ESP32 board's built-in LED pin (commonly GPIO 2, but varies by manufacturer)
2. The hardware revision setting in `platformio.ini`
3. The pin assignment in `src/main.cpp`

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'feat: add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

### Development Guidelines

- Follow the existing code style
- Use meaningful commit messages (conventional commits)
- Test your changes on hardware if possible
- Update documentation as needed

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Related Projects

- [KM271-WIFI Hardware](https://github.com/the78mole/KM271-WIFI) - PCB design and hardware files
- [Buderus KM271](https://github.com/the78mole/buderus-km271) - Communication protocol documentation

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/the78mole/KM271-WIFI-Test/issues)
- **Discussions**: [GitHub Discussions](https://github.com/the78mole/KM271-WIFI-Test/discussions)

## 🏗️ CI/CD Status

The project uses a sophisticated CI/CD pipeline with:

- **Docker-based builds** using `ghcr.io/the78mole/platformio-docker:v1.0.0`
- **Multi-environment support** for different hardware revisions
- **Automatic factory image creation** with correct flash offsets
- **Semantic versioning** with automatic release creation
- **Comprehensive release notes** with flash instructions

---

**Made with ❤️ for the Buderus KM271 community**
