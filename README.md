# TFVM - Terraform Version Manager for Windows
### A NodeJS-based CLI tool to manage terraform versions on windows without needing admin access (that actually works)


## Setup

### Step 1: Installation
In order to use tfvm-windows, you must be able to run powershell scripts. To enable powershell scripts to run on your machine, **run the following command in a powershell window:**
  ```shell
  Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
  ```

Next, install tfvm. You will need to have node installed.
  ```shell
  npm i -g tfvm-windows
  ```
> If you frequently change versions of node and you wish to use tfvm in other node versions, you will need to re-install tfvm in this way for each version.
>
> Fortunately, any installed terraform versions and your selected terraform version will be maintained for each node version that you switch to, as they are stored on your system and not in node's files.

### Step 2: Delete existing terraform setup
tfvm will auto-create directories and an environment variable for terraform setup. This will conflict with anything you already have.
1. If you already have terraform set up on your computer, delete your entry for your terraform directory in your PATH environment variables.
2. You could leave your terraform.exe file(s), but you might as well delete them. tfvm will download its own files.

### Step 3: Run tfvm for the first time
1. Open up any command line (command prompt, Powershell, Git Bash, etc).
2. Run any tfvm command. If you know what version you want to use first, you can run `tfvm install <that version>` and then `tfvm use <that version>`.
   If you don't have a version in mind, you could run something like `tfvm list` or `tfvm install latest`. 
> You should see some lines appear saying that tfvm has automatically added a directory pointing to its terraform installation folder to your Path. This means it is working correctly
3. Restart your terminal(s). In order to start using terraform now, you'll have to open up a new terminal so that your Path can be refreshed and your CLI can actually find terraform.
   Any terminals (including those built into IDEs) that were open before you installed tfvm will have to be restarted to use the versions of terraform that tfvm install.
   This may require you to also restart your IDE.
4. in your new terminal, run `terraform --version` to verify that you are using the version of terraform that you installed with tfvm.

## Usage
run `tfvm` in any command line that has admin privileges (e.g. 'Run as Administrator), followed by one of these commands:
- `install` or `i`: installs terraform version and sets up folder inside your tfvm folder.
  - Ex: `tfvm install 1.0.3` or `tfvm install latest`
- `list` or `ls`: lists all versions of terraform you have saved in your tfvm folder.
  - Ex: `tfvm list`
- `uninstall`: Deletes terraform executable and folder inside your tfvm folder.
  - Ex: `tfvm uninstall 1.0.3`
- `use` or `u`: sets specified terraform version to being the actively used version.
  - Ex: `tfvm use 1.0.3`
  - If you attempt to use a version that you haven't installed, you will be prompted to install it.
- `current`: displays the terraform version you are using.
  - Ex: `tfvm current`
- `tfvm config`: allows the user to change tfvm settings (currently the only setting is 'disableErrors', a boolean)
  - Ex: `tfvm config disableErrors=true`
- `help`: prints usage information. Run `tfvm help <command>` to see information about the other tfvm commands.

## FAQ
**Q:** Why use this app instead of one of the other terrform version managers you can find?

**A:** It is the simplest to use for Windows. Most don't support windows, and those that do are unintuitive. This one is simple and works, especially for beginners to terraform.

**Q:** I'm getting this error when running tfvm in powershell: `File C:\Program Files\nodejs\tfvm.ps1 cannot be loaded because running scripts is disabled on this system.`

**A:** Most custom CLI apps will throw this error in Powershell. Run this command to update your powershell execution policy:
  ```shell
  Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
  ```

**Q:** What terraform versions are supported?

**A:** tfvm will install and use any major version that is available in the [Hashicorp Terraform Releases archive](https://releases.hashicorp.com/terraform/). At this time, tfvm will not allow you to select alpha, beta, or rc releases (though this is planned for a future update).
