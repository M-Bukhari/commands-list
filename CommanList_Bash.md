# Bash and Linux

## Command list

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
