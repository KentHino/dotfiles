# ssh/conf.d directory structure

## Contents

- `repo` - Repository-related SSH configurations (e.g., GitHub, GitLab)
- `hosts/` - Host-specific configurations (managed as a Git submodule)

## Submodule Setup

The `hosts` directory is managed as a separate Git submodule for privacy and flexibility.

### Adding the submodule:

```bash
# From the dotfiles root directory
git submodule add <your-private-repo-url> ssh/conf.d/hosts
git commit -m "Add SSH hosts as submodule"
```

### Cloning with submodules:

```bash
git clone --recurse-submodules <dotfiles-repo-url>
```

Or if already cloned:

```bash
git submodule update --init --recursive
```

### Updating the submodule:

```bash
cd ssh/conf.d/hosts
git pull origin main
cd ../../..
git add ssh/conf.d/hosts
git commit -m "Update SSH hosts submodule"
```
