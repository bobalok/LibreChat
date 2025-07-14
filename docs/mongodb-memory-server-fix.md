# MongoDB Memory Server Installation Fix

If you encounter errors during npm installation related to `mongodb-memory-server`, use this solution:

## Problem
The error occurs when `mongodb-memory-server` tries to download MongoDB binaries but fails during the file rename operation:

```
Error: ENOENT: no such file or directory, rename '/path/to/mongodb-macos-arm64-7.0.14.tgz.downloading' -> '/path/to/mongodb-macos-arm64-7.0.14.tgz'
```

## Solution

### Method 1: Disable Post-Install (Recommended)
Set the environment variable to skip binary downloads:

```bash
export MONGOMS_DISABLE_POSTINSTALL=1
npm install
```

### Method 2: Use System MongoDB
If you have MongoDB installed globally:

```bash
export MONGOMS_SYSTEM_BINARY=/usr/local/bin/mongod
npm install
```

### Method 3: Clear Cache and Retry
```bash
npm cache clean --force
rm -rf node_modules/.cache/mongodb-memory-server
npm install
```

## Permanent Fix
Add to your shell profile (`.zshrc`, `.bashrc`, etc.):

```bash
export MONGOMS_DISABLE_POSTINSTALL=1
```

This prevents the issue from occurring in future installations.

## Note
This package is only used for testing and doesn't affect production functionality.
