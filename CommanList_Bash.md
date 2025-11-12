# Bash and Linux

## Command list

### Genral Commands

```bash

    #  To get current time
    date +"%I:%M %P"
    # 01:07 pm

    date +"%I:%M %p"
    # 01:07 PM

    date +"Week: %W - %U - %V | %A ( %d\%m\%Y | %H:%M:%S )"
    # Week: 45 - 45 - 46 | Wednesday ( 12\11\2025 | 09:18:13 )

# =================================================================
    # Get OS info
# =================================================================
    cat /etc/os-release

    # Output Result
    PRETTY_NAME="Ubuntu 24.04.3 LTS"
    NAME="Ubuntu"
    VERSION_ID="24.04"
    VERSION="24.04.3 LTS (Noble Numbat)"
    VERSION_CODENAME=noble
    ID=ubuntu
    ID_LIKE=debian
    HOME_URL="https://www.ubuntu.com/"
    SUPPORT_URL="https://help.ubuntu.com/"
    BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
    PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
    UBUNTU_CODENAME=noble
    LOGO=ubuntu-logo

    # Restart WSL from Windows PowerShell:
    wsl --shutdown

# =================================================================


# =================================================================
    # Check installed chromium dependencies
# =================================================================
    dpkg -l | grep -E "libasound|libatk|libcups|libdrm|libgbm|libgtk|libnss|libxss" | head -20

    # Output Result
    ii  libatk-bridge2.0-0t64:amd64          2.52.0-1build1                          amd64        AT-SPI 2 toolkit bridge - shared library
    ii  libatk1.0-0t64:amd64                 2.52.0-1build1                          amd64        ATK accessibility toolkit
    ii  libcups2t64:amd64                    2.4.7-1.2ubuntu7.4                      amd64        Common UNIX Printing System(tm) - Core library
    ii  libdrm-amdgpu1:amd64                 2.4.122-1~ubuntu0.24.04.1               amd64        Userspace interface to amdgpu-specific kernel DRM services -- runtime
    ii  libdrm-common                        2.4.122-1~ubuntu0.24.04.1               all          Userspace interface to kernel DRM services -- common files
    ii  libdrm-intel1:amd64                  2.4.122-1~ubuntu0.24.04.1               amd64        Userspace interface to intel-specific kernel DRM services -- runtime
    ii  libdrm-nouveau2:amd64                2.4.122-1~ubuntu0.24.04.1               amd64        Userspace interface to nouveau-specific kernel DRM services -- runtime
    ii  libdrm-radeon1:amd64                 2.4.122-1~ubuntu0.24.04.1               amd64        Userspace interface to radeon-specific kernel DRM services -- runtime
    ii  libdrm2:amd64                        2.4.122-1~ubuntu0.24.04.1               amd64        Userspace interface to kernel DRM services -- runtime
    ii  libgbm-dev:amd64                     25.0.7-0ubuntu0.24.04.2                 amd64        generic buffer management API -- development files
    ii  libgbm1:amd64                        25.0.7-0ubuntu0.24.04.2                 amd64        generic buffer management API -- runtime
    ii  libgtk-3-0t64:amd64                  3.24.41-4ubuntu1.3                      amd64        GTK graphical user interface library
    ii  libgtk-3-bin                         3.24.41-4ubuntu1.3                      amd64        programs for the GTK graphical user interface library
    ii  libgtk-3-common                      3.24.41-4ubuntu1.3                      all          common files for the GTK graphical user interface library
    ii  libnss-mdns:amd64                    0.15.1-4build1                          amd64        NSS module for Multicast DNS name resolution
    ii  libnss-systemd:amd64                 255.4-1ubuntu8.11                       amd64        nss module providing dynamic user and group name resolution
    ii  libnss3:amd64                        2:3.98-1build1                          amd64        Network Security Service libraries
    ii  libxss1:amd64                        1:1.2.3-1build3                         amd64        X11 Screen Saver extension library

# =================================================================

```

## Markdown PDF is not exporting pdf in WSL

Looking at this error, the issue is that the Puppeteer Chromium binary is missing required shared libraries in your WSL environment. This is a common problem when running headless Chrome in WSL. Let me check what's already installed and help you install the missing dependencies.

```bash

    #  Install Chromium dependencies for Ubuntu

    sudo apt-get update && sudo apt-get install -y \
        libasound2 \
        libatk-bridge2.0-0 \
        libatk1.0-0 \
        libcups2 \
        libdbus-1-3 \
        libdrm2 \
        libgbm1 \
        libgtk-3-0 \
        libnspr4 \
        libnss3 \
        libxcomposite1 \
        libxdamage1 \
        libxfixes3 \
        libxkbcommon0 \
        libxrandr2 \
        xdg-utils \
        fonts-liberation \
        libu2f-udev \
        libvulkan1


    sudo apt-get update && sudo apt-get install -y \
        libasound2t64 \
        libasound2-data \
        ca-certificates \
        fonts-liberation \
        libappindicator3-1 \
        libnss3 \
        lsb-release \
        xdg-utils \
        wget \
        libgbm1 \
        libxshmfence1
```

### Why this fixes the issue:

The error libasound.so.2: cannot open shared object file means the Chromium binary bundled with the markdown-pdf extension is missing the ALSA sound library and likely other dependencies. On Windows, these libraries come pre-installed, but in WSL (Linux environment), you need to install them manually. The command above installs all the shared libraries that Chromium needs to run in a headless environment, including:
libasound2 - The missing ALSA sound library
Graphics libraries (libgbm1, libdrm2, libvulkan1)
GTK and accessibility libraries (libgtk-3-0, libatk\*)
X11 libraries for rendering (libxcomposite1, libxdamage1, libxfixes3, libxrandr2)
NSS libraries for network security (libnss3)
Fonts and utilities
After running this command, the markdown-pdf extension should work correctly in WSL.

## Searching for something

```bash
    Search for terms acceptance in blade files
    grep -r "termsAcceptance\|terms_acceptance\|terms-acceptance" "d:\01 Apps\Development\Web\abam-invest-hub\resources" 2>/dev/null

    Output Result :
    # d:\01 Apps\Development\Web\abam-invest-hub\resources/views/investor/qualification.blade.php:          <label for="termsAcceptance" class="terms-label danger-text"
    # d:\01 Apps\Development\Web\abam-invest-hub\resources/views/investor/qualification.blade.php:          <select id="termsAcceptance" name="termsAcceptance" required>



    Search for terms styling in CSS
    grep -n "danger-text\|terms-label" "d:\01 Apps\Development\Web\abam-invest-hub\public\css\forms.css" 2>/dev/null

    Output Result :
    # 410:.terms-label {



    Search for danger and terms styling
    grep -n "danger\|terms" "d:\01 Apps\Development\Web\abam-invest-hub\public\css\components.css" 2>/dev/null | head -20

    Output Result :
    # 463:  .alert-danger {
    # 464:    background: linear-gradient(45deg, var(--danger-color), #e74c3c);
    # 890:  .badge-danger {
    # 991:  .btn-outline-danger {
    # 996:  .btn-outline-danger:hover {
    # 1002: .border-danger {

    Output Result :
#     D:\01 Apps\Development\Web\abam-invest-hub\01_local-files\TempBackup\qualification-views-backup-20250928_134704\qualification-component.blade.php
#     D:\01 Apps\Development\Web\abam-invest-hub\01_local-files\TempBackup\qualification-views-backup-20250928_134704\qualification.old.blade.php
#     D:\01 Apps\Development\Web\abam-invest-hub\01_local-files\TempBackup\qualification-views-backup-20250928_134704\qualification.blade.php
#     D:\01 Apps\Development\Web\abam-invest-hub\01_local-files\TempBackup\251030\qualification_new.blade.php
#     D:\01 Apps\Development\Web\abam-invest-hub\resources\views\project\qualification.blade.php
#     D:\01 Apps\Development\Web\abam-invest-hub\resources\views\investor\qualification.blade.php
```

```bash

    #  To get current time
    date +"%I:%M %P"
    # 01:07 pm

    date +"%I:%M %p"
    # 01:07 PM

```

## Stagind Servers Inquiries and Details

### Check the UPload File Size

```bash
[u779519913@us-phx-web1104 invest-hub]$ cat .env | grep -E "UPLOAD_MAX_SIZE|POST_MAX_SIZE"
UPLOAD_MAX_SIZE=32M
POST_MAX_SIZE=64M

[u779519913@us-phx-web1104 invest-hub]$ ps aux | grep nginx
u779519+ 2817754  0.0  0.0 221944  1180 pts/4    S+   12:18   0:00 grep --color=auto nginx

[u779519913@us-phx-web1104 invest-hub]$ php -i | grep -i "upload_max_filesize"

upload_max_filesize => 256M => 256M
[u779519913@us-phx-web1104 invest-hub]$ php -i | grep -i "post_max_size"

post_max_size => 256M => 256M
[u779519913@us-phx-web1104 invest-hub]$ php -i | grep -i "max_file_uploads"

max_file_uploads => 20 => 20
[u779519913@us-phx-web1104 invest-hub]$ cat /etc/nginx/nginx.conf | grep client_max_body_size
cat: /etc/nginx/nginx.conf: No such file or directory

```

## Selecting Multiple Occurrences in Visual Studio Code

Visual Studio Code (VS Code) provides powerful multi-cursor editing features to select and edit multiple occurrences of text efficiently. This is often called "multi-select" or "multiple cursors." Below are the main methods, with keyboard shortcuts (default on Windows/Linux; macOS uses Cmd instead of Ctrl

1. Select All Occurrences of the Currently Selected Text

Shortcut: Ctrl+Shift+L (macOS: Cmd+Shift+L)
How it works:

First, select or place your cursor on a word/phrase.
Press the shortcut to add a cursor (and selection) at every occurrence in the file.
Type to edit all instances simultaneously.

Tip: This is ideal for renaming variables or updating repeated strings.

2. Add Next Occurrence (One by One)

Shortcut: Ctrl+D (macOS: Cmd+D)
How it works:

Select or cursor on a word.
Press Ctrl+D repeatedly to add cursors to the next matching occurrence each time.
Stop when you've selected the desired ones, then edit.

Undo last addition: Ctrl+U (macOS: Cmd+U)
Tip: Great for selective edits without selecting everything at once.

3. Select All via Find Widget

Steps:

Select a word or open the Find widget with Ctrl+F (macOS: Cmd+F).
In the Find widget, press Alt+Enter (macOS: Option+Enter) to select all matches in the file.

How it works: Adds cursors to every match of the search term.
Tip: Useful if you want to preview matches first.

4. Add Cursors with Mouse (Column or Multi-Select Mode)

Hold Alt (macOS: Option) and click/drag to place multiple cursors anywhere.
For columns: Enable Column Selection Mode via the status bar or menu (Selection > Column Selection Mode). Then, drag with Shift+Alt (macOS: Shift+Option).
Customize modifier: In settings (Ctrl+,), search for editor.multiCursorModifier and set to ctrlCmd or alt.

Additional Tips

Menu access: Go to Selection > Add Cursor Above/Below or Switch to Ctrl+Click for Multi-Cursor.
Extensions: For regex-based multi-select, try "Find and Transform" or built-in regex support in Find (enable with the regex icon).
These features work across languages and file types, making VS Code feel like Sublime Text for multi-edits.

If these don't match your setup (e.g., due to keybinding conflicts), check your Keyboard Shortcuts (Ctrl+K Ctrl+S) or reset to defaults. For more, see the official docs on basic editing.

## Removing NVM to install it again

### Step 1: Remove the Old NVM Configuration

```bash

    # Open the file in nano editor
    nano ~/.bash_profile

    Use Ctrl + _ (underscore) to go to a specific line

    Type 127 and press Enter

    # NVM configuration
    export NVM_DIR="/Users/m.bukhari/Library/Application Support/Herd/config/nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

    Position your cursor on line 127
    Press Ctrl + K four times (once for each line) to delete all 4 lines


    # Remove lines 127-130 from .bash_profile
    sed -i '127,130d' ~/.bash_profile && source ~/.bash_profile
```

### Step 4: Save and Exit

    Press Ctrl + X
    Press Y to confirm
    Press Enter to save

### Step 5: Reload Your Shell

```bash
    # Reload Your Shell
    source ~/.bash_profile

    # Verify NVM_DIR is Cleared
    echo $NVM_DIR

    # Install NVM Fresh
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash


    # Verify installed tools
    node --version && npm --version && nvm --version && npx --version


    # Install latest LTS
    nvm install --lts

    # Verify
    node --version
    npm --version
```
