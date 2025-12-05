# Citron CI Workflows

This directory contains GitHub Actions workflows for building Citron emulator across multiple platforms.

## Workflows

### 🪟 Windows Build (`build-windows.yml`)
- **Trigger**: Manual dispatch only
- **Platform**: Windows x64
- **Build System**: CMake + Visual Studio 2022
- **Output**: ZIP archive with Qt6 GUI
- **Release Tag**: `nightly-windows`

### 🐧 Linux Build (`build-linux.yml`)
- **Trigger**: Manual dispatch only
- **Platform**: Linux x86_64 (CachyOS container)
- **Build System**: CMake + Ninja
- **Output**: AppImage (portable) + tar.gz (binaries)
- **Release Tag**: `nightly-linux`

### 📱 Android Build (`build-android.yml`)
- **Trigger**: Manual dispatch only
- **Platform**: Android ARM64-v8a
- **Build System**: Gradle + Android NDK 26.1.10909125
- **Output**: APK (unsigned or signed if secrets configured)
- **Release Tag**: `nightly-android`

## Configuration

### Required Secrets (Optional)
- `ANDROID_KEYSTORE_B64`: Base64-encoded Android keystore for APK signing
- `ANDROID_KEY_ALIAS`: Keystore key alias
- `ANDROID_KEYSTORE_PASS`: Keystore password

### Version Tracking
Each workflow maintains a separate version file:
- `LATEST_VERSION_WINDOWS`
- `LATEST_VERSION_LINUX`
- `LATEST_VERSION_ANDROID`

These files track the last successfully built commit hash from the upstream Citron repository.

## Upstream Source
All builds pull from: `https://git.citron-emu.org/Citron/Emulator.git`
Branch: `fix/audio-biquad-filter-metroid-prime-4`

## Build Process

1. **Version Check**: Compare upstream commit hash with last built version
2. **Build**: Compile Citron for the target platform
3. **Package**: Create distribution packages
4. **Release**: Create/update nightly release with artifacts

## Manual Trigger

You can manually trigger any workflow:
1. Go to the "Actions" tab
2. Select the desired workflow
3. Click "Run workflow"
4. Choose the branch and click "Run workflow"

## Artifacts Retention

- Workflow artifacts: 90 days
- Release artifacts: Permanent (until manually deleted)
- Each nightly release is overwritten with the latest build
