# Tmux Configuration Documentation

## Configuration File Locations

### Primary Configuration
- **Main config**: `/home/<username>/.tmux.conf`
  - **Impact**: This is the active configuration file that tmux reads on startup
  - **When to edit**: All tmux customizations should go here

### Backup/Alternative Locations
- **Dotfiles**: `/home/<username>/dotfiles/tmux/.tmux.conf`
  - **Impact**: Version-controlled dotfiles repository
  - **When to edit**: When syncing configurations across systems

## Key Bindings

### Prefix Key
- **Default**: `C-b` (Control + b)
- **Alternative**: `C-a` (commented out, uncomment to use)

### Session Management
| Key Binding | Action |
|------------|--------|
| `tmux new -s name` | Create new named session |
| `tmux ls` | List all sessions |
| `tmux attach -t name` | Attach to session |
| `C-b d` | Detach from session |
| `C-b s` | Switch sessions interactively |

### Window Management
| Key Binding | Action |
|------------|--------|
| `C-b c` | Create new window |
| `C-b n` | Next window |
| `C-b p` | Previous window |
| `C-b 0-9` | Switch to window number |
| `C-b w` | List windows interactively |
| `C-b ,` | Rename current window |
| `C-b &` | Kill current window |

### Pane Management
| Key Binding | Action |
|------------|--------|
| `C-b \|` | Split window vertically |
| `C-b -` | Split window horizontally |
| `C-b h` | Move to left pane |
| `C-b j` | Move to bottom pane |
| `C-b k` | Move to top pane |
| `C-b l` | Move to right pane |
| `C-b H` | Resize pane left |
| `C-b J` | Resize pane down |
| `C-b K` | Resize pane up |
| `C-b L` | Resize pane right |
| `C-b x` | Kill current pane |

### Copy Mode (Vi-style)
| Key Binding | Action |
|------------|--------|
| `C-b [` | Enter copy mode |
| `v` | Start selection |
| `C-v` | Rectangle selection |
| `y` | Copy selection |
| `q` | Exit copy mode |

### Configuration Management
| Key Binding | Action |
|------------|--------|
| `C-b r` | Reload configuration |

## Configuration Sections

### Basic Settings
```bash
# Prefix key configuration
set -g prefix C-b
unbind C-s

# Mouse support
set -g mouse on

# Window/pane indexing
set -g base-index 1
set -g pane-base-index 1
set-option -g renumber-windows on
```

### Terminal Settings
```bash
# Color support
set -g default-terminal "screen-256color"
set -ga terminal-overrides ",*256col*:Tc"

# Vi mode
set-window-option -g mode-keys vi

# Performance
set -s escape-time 0
set -g history-limit 10000
```

### Visual Styling
```bash
# Status bar position
set-option -g status-position bottom

# Pane borders
set -g pane-border-style 'fg=#313244'
set -g pane-active-border-style 'fg=#89b4fa'

# Window list formatting
set -g window-status-separator " "
set -g window-status-format " #I:#W "
set -g window-status-current-format " #I:#W "
set -g status-justify centre
```

### Activity Monitoring
```bash
set -g monitor-activity on
set -g visual-activity off
```

## Plugins

### Plugin Manager
- **TPM** (Tmux Plugin Manager): `tmux-plugins/tpm`
- **Installation**: `git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm`
- **Install plugins**: `C-b I`
- **Update plugins**: `C-b U`
- **Uninstall plugins**: `C-b alt+u`

### Installed Plugins

#### 1. Catppuccin Theme
- **Plugin**: `catppuccin/tmux`
- **Flavor**: Mocha
- **Status modules**: Directory and session
- **Configuration**:
  ```bash
  set -g @catppuccin_flavour 'mocha'
  set -g @catppuccin_status_modules_right "directory session"
  set -g @catppuccin_directory_text "#{pane_current_path}"
  ```

#### 2. Vim-Tmux Navigator
- **Plugin**: `christoomey/vim-tmux-navigator`
- **Purpose**: Seamless navigation between vim and tmux panes
- **Usage**: Same `h/j/k/l` keys work in both vim and tmux

## Troubleshooting

### Configuration Not Loading
```bash
# Reload configuration
tmux source-file ~/.tmux.conf

# Check if config file exists
ls -la ~/.tmux.conf

# Check for syntax errors
tmux -f ~/.tmux.conf new-session -d \; kill-session
```

### Plugin Issues
```bash
# Reinstall plugins
rm -rf ~/.tmux/plugins/
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
# Then press C-b I to install plugins
```

### Color Issues
```bash
# Check terminal color support
echo $TERM
# Should show "screen-256color" inside tmux

# Test true color support
curl -s https://raw.githubusercontent.com/JohnMorales/dotfiles/master/colors/24-bit-color.sh | bash
```

## Configuration Impact by Location

### `/home/<username>/.tmux.conf`
- **Primary config file**
- **Impact**: All tmux sessions
- **Reload**: `tmux source-file ~/.tmux.conf`

### `/home/<username>/dotfiles/tmux/.tmux.conf`
- **Version-controlled dotfiles**
- **Impact**: Backup/sync across systems
- **Usage**: Repository management

## Custom Features

### Enhanced Splitting
- Creates splits in current directory
- Intuitive `|` and `-` keys for vertical/horizontal splits

### Vim-style Navigation
- `h/j/k/l` for pane movement
- `H/J/K/L` for pane resizing
- Vi-mode copy/paste

### Better Defaults
- Windows/panes start at 1 (not 0)
- Mouse support enabled
- Faster escape sequences
- Larger scrollback buffer (10,000 lines)

### Visual Improvements
- Status bar at bottom (no gap with terminal)
- Centered window list
- Subtle pane borders
- Catppuccin theme integration
