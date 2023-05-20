# EcoNuker
Guilded Bot: EcoNuker. This repository is private and reserved for developers only.

# Setup
If you're not using pm2, you can safely ignore the monitor.
- Download this repository as a zip, and unzip it.
- Install the required libraries using `pip install -r requirements.txt` or your pip command (eg. `pip3`)
    - If you're on Windows, cairosvg will require extra setup. Run `pip install pipwin`, then run `pipwin install cairocffi`
    - Chess may encounter issues when installing `uplink-python`. Read https://pypi.org/project/uplink-python/ (Option 2) for more info.
        - This will require GO. Install it on your platform.
            - There may be issues on Windows. If you're getting the `loadinternal: cannot find runtime\cgo` error, run this command: `go env -w CGO_ENABLED=1`
            - There may be issues on Windows. If you're getting the `cgo: C compiler "gcc" not found: exec: "gcc": executable file not found in %PATH%` error, install https://jmeubank.github.io/tdm-gcc/. Make sure to check "Add to Path" at the bottom of the list of items!
            - Once you have built `libuplinkc.so`, check the error message again. There should be a path where the `uplink-python` library is installed; this is normally located at (Windows) `%localappdata%\Programs\Python\Python310\Lib\site-packages\uplink_python`, (Linux) `/usr/local/lib/python3.10/dist-packages/uplink_python`
                - Navigate to the directory, and drop `libuplinkc.so` into it. Verify the uplink works by running the bot again.
- The API requires a Memcached server. Follow the accepted answer here if you're on windows: https://stackoverflow.com/questions/59476616/install-memcached-on-windows
    - On Linux, install memcached `sudo apt-get install memcached` (Debian flavors) or `sudo yum install memcached` (CentOS)
    - Start the server on port 11211.
    - If you're on Ubuntu, make sure to add Uncomplicated Firewall exceptions: `ufw allow 11211`
- Make sure your bot has all the required permissions. For testing, we recommend all permissions.
- Setup your config file! There will be a readme.md in the /configs/ folder to tell you what variable is what. **The backup database has a max connection limit of 5, and will be slower.**
- Run your bot. You can start it in debug mode or normal by running `python guildedbot.py` or `python guildedbot.py debug`

# Notes
To restore the backup DB, you might use the `db_restore` command. This command can cause a lot of issues. The correct format is:
`pg_restore -h hosturl -p 5432 -U username -d databasename < dumpfile.dump`

**Do not merge the *beta* branch into *main*. The *beta* branch uses seperate configs. Instead, create a pull request after creating a new temporary branch, and upload any changed files. If the configs were updated, update the config files TAKEN FROM *main* MANUALLY, adding/removing whatever needs to be changed.**
- Alternative: If there's too many changed files and you can't bother, download the `configs/` and `debugconfigs/` content, create a seperate branch based off of the Beta branch, and merge that temporary branch into Main. After that, replace the configs with the normal EcoNuker configs. *Even when using the alternative, keep the Beta branch. Create a temporary branch to merge Main with.*
