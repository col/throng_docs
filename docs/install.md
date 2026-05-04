# Install

## macOS (Homebrew)

Throng is distributed via a custom Homebrew tap.

### 1. Tap the repository

```bash
brew tap col/throng
```

This registers the `col/throng` tap so Homebrew knows where to find the
formula.

### 2. Install Throng

```bash
brew install col/throng/throng
```

### 3. Run first-time setup

```bash
throng setup
```

This prepares config, data directories, and any required local state.

### 4. Start the service

```bash
brew services start throng
```

`brew services` runs Throng in the background and re-launches it on login.
To stop it later, use `brew services stop throng`.

### 5. Verify it's running

Open <http://localhost:7654> — you should see the Throng app.

## Upgrading (Homebrew)

### 1. Update Homebrew

```bash
brew update
```

### 2. Upgrade Throng

```bash
brew upgrade col/throng/throng

# or

brew upgrade --restart-service col/throng/throng
```

### 3. Re-run Throng Setup (optional)

```bash
throng setup
```

### 4. Restart the Throng service

```bash
brew services restart throng
```