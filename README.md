# find_flutter_builds

A lightweight Bash CLI tool for macOS and Linux that recursively discovers and cleans Flutter/Dart project `build` directories to recover disk space.

## Features

- **Project-Aware**: Finds `build/` directories only if a valid `pubspec.yaml` exists in the same root.
- **Size Calculation**: Formats folder sizes accurately (KB, MB, GB).
- **Automation Ready**: Outputs raw paths by default, making it easy to pipe into other CLI workflows.
- **Safe Cleanup**: Executes official `flutter clean` commands inside target project directories.

## Installation

1. Download or clone the script:
    ```bash
    curl -O https://raw.githubusercontent.com/your-username/find_flutter_builds/main/find_flutter_builds
    ```
2. Make it executable:
    ```bash
    chmod +x find_flutter_builds
    ```

3. Move it to a directory in your PATH (e.g. `/usr/local/bin` or `~/.local/bin`):

   # Option A: System-wide installation
   ```bash
   sudo mv find_flutter_builds /usr/local/bin/
   ```

   # Option B: User-level installation (recommended on macOS)
   ```bash
   mkdir -p ~/.local/bin
   mv find_flutter_builds ~/.local/bin/
   ```

4. (If command is not found) Ensure the directory is in your PATH. 
   For zsh (default shell on macOS), run:

   ```bash
   echo 'export PATH="$HOME/.local/bin:/usr/local/bin:$PATH"' >> ~/.zshrc
   source ~/.zshrc
   ```

## Usage
```bash
find_flutter_builds [-s] [-d] [path]
```

### Options

- (none): Outputs plain paths to build directories (ideal for piping).
- -s: Displays each directory's size alongside its path and shows total size summary.
- -d: Executes flutter clean on discovered projects and outputs total freed space.

### Examples

1. List build directories in current directory:
   ./find_flutter_builds

   Output:
   ./my_app/build
   ./packages/custom_widget/build

2. Inspect build directory sizes in a specific workspace:
   ./find_flutter_builds -s ~/Projects

   Output:
   /Users/user/Projects/my_app/build (1.20 GB)
   /Users/user/Projects/packages/custom_widget/build (240.50 MB)
   ----------------------------------------
   SUMMARY:
   Total build size: 1.43 GB

3. Clean all projects in a directory:
   ./find_flutter_builds -d ~/Projects

   Output:
   /Users/user/Projects/my_app/build
     └─ Cleaning (flutter clean)...
   /Users/user/Projects/packages/custom_widget/build
     └─ Cleaning (flutter clean)...
   ----------------------------------------
   SUMMARY:
   Total space freed: 1.43 GB

4. Combine size estimation and cleanup:
   ./find_flutter_builds -sd ~/Projects

## License

MIT