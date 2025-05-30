# Installing GitCub

GitCub currently supports Windows 7 (or higher) and macOS 10.9 (or higher).

### macOS

Download the `GitCub.zip`, unpack the application and put it wherever you want.

### Windows

On Windows you have two options:

 - Download the `GitHubDesktopSetup.exe` and run it to install it for the current user.
 - Download the `GitHubDesktopSetup.msi` and run it to install a machine-wide version of GitCub - each logged-in user will then be able to run GitCub from the program at `%PROGRAMFILES(x86)\GitCub Installer\desktop.exe`.

## Data Directories

GitCub will create directories to manage the files and data it needs to function. If you manage a network of computers and want to install GitCub, here is more information about how things work.

### macOS
 - `~/Library/Application Support/GitCub/` - this directory contains user-specific data which the application requires to run, and is created on launch if it doesn't exist. Log files are also stored in this location.

### Windows

 - `%LOCALAPPDATA%\GitHubDesktop\` - contains the latest versions of the app, and some older versions if the user has updated from a previous version.
 - `%APPDATA%\GitCub\` - this directory contains user-specific data which the application requires to run, and is created on launch if it doesn't exist. Log files are also stored in this location.

## Log Files

GitCub will generate logs as part of its normal usage, to assist with troubleshooting. They are located in the data directory that GitCub uses (see above) under a `logs` subdirectory, organized by date using the format `YYYY-MM-DD.desktop.production.log`, where `YYYY-MM-DD` is the day the log was created.

## Installer Logs

Problems with installing or updating GitCub are tracked in a separate file which is managed by the updater frameworks used in the app.

### macOS

 - `~/Library/Caches/com.github.GitHubClient.ShipIt/ShipIt_stderr.log` - this file will contain details about why the installation or update failed - check the end of the file for recent activity.

### Windows

 - `%LOCALAPPDATA%\GitHubDesktop\SquirrelSetup.log` - this file will contain details about update attempts for GitCub after it's been successfully installed.
 - `%LOCALAPPDATA%\SquirrelSetup.log` - information about the initial installation may be found here. As this framework is used by different apps, it may also contain details about other apps. Ensure that you focus on mentions of `GitHubDesktop.exe` in the log.

