# WordPress Database Prefix Changer

A powerful, safe, and automated Bash script to change the WordPress database table prefix. This tool handles the entire process: backing up the database, renaming tables, updating internal references (usermeta/options), and modifying `wp-config.php`.

## 🚀 Features

- **Auto-Discovery**: Automatically detects database credentials and the current prefix from wp-config.php.
- **Safety First**: Creates a full database backup (`.sql dump`) before applying any changes.
- **Deep Cleaning**: Not only renames tables but also updates critical rows in `_usermeta` and `_options` tables to prevent permission issues.
- **Config Update**: Automatically updates the `$table_prefix` variable in your `wp-config.php` file.
- **Self-Update**: Checks for the latest version of the script remotely.

## 📋 Prerequisites

To run this script, your environment must have:
- Linux/Unix OS (Ubuntu, Debian, CentOS, etc.)
- `bash` (shell)
- `mysql` and `mysqldump` (client tools)
- `grep`, `awk`
- `curl` or `wget` (for update checks)
- `Root/Sudo` access is recommended if file permissions are restricted, though not strictly required if the user owns the files.

## 📥 Installation

You can download the script directly to your WordPress root directory:

```bash
wget https://raw.githubusercontent.com/percioandrade/wpchangeprefix/refs/heads/main/wp-change-prefix.sh
chmod +x wpchange_prefix.sh
```

## ⚙️ Usage

**1. Navigate to your WordPress root directory (where wp-config.php is located).**

**2. Run the script:**

```bash
./wpchange_prefix.sh
```

**3. Follow the interactive prompts:**

- The script will verify credentials.
- It will show the current detected prefix.
- It will ask for the NEW prefix (alphanumeric only).
- Confirm the operation.

## Command Line Options

```bash
Flag             Description
-s, --skip       Skip Backup: Runs the script without creating a database dump (Not recommended).
-n, --noversion  No Version Check: Skips the remote check for script updates.
-h, --help       Displays the help menu.
```

**Example**

# Run without checking for updates and skipping backup

```bash
./wpchange_prefix.sh --skip --noversion
```

🛠️ How it Works

- **Validation**: Checks if `wp-config.php` exists and parses DB credentials.
- **Connection**: Tests connection to the MySQL server.
- **Detection**: Scans `information_schema` to find the active prefix (looking for `_usermeta` or `_options`).
- **Backup**: Runs `mysqldump` to save the current state.
- **Renaming**: Iterates through all tables matching the old prefix and renames them to the new prefix.
- **Data Patching**: Runs SQL updates to fix prefix references inside `usermeta` (keys like `wp_capabilities`) and options (keys `like wp_user_roles`).
- **Finalize**: Updates the PHP variable in the config file.

## ⚠️ Disclaimer

> [!WARNING]
> This software is provided "as is". Always make sure to test in a development environment first. The author is not responsible for any misuse, legal consequences, or data impact caused by this tool.

## 📚 Detailed Tutorial

For a complete, step-by-step guide on how to import generated files into Thunderbird and troubleshoot common migration issues, check out my full article:

👉 [**Create modal popups in WHMCS**](https://perciocastelo.com.br/blog/change-wordpress-database-prefix.html)

## License 📄

This project is licensed under the **GNU General Public License v3.0**. See the [LICENSE](LICENSE) file for more details.
