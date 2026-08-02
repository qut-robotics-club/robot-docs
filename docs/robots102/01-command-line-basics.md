# Command Line Basics

## Introduction
This lesson establishes essential terminal/command-line skills needed before moving into version control systems like Git. These commands are fundamental for navigating any project environment effectively [1].

---

## 1. What is a Terminal/Command-Line Interface?

A **terminal** (or CLI) provides text-based access to your operating system without a graphical interface. It's essential because:
- Many development tools operate primarily via command-line
- Version control systems like Git interact with the terminal [1]
- Scripts and automation run from here

### Installation Requirements Before Starting

| Operating System           | Terminal Type                                        | How to Access                                                                                      | Setup Notes                                                                                                                                                            |
| -------------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Windows**                | Command Prompt (`cmd`), PowerShell, Windows Terminal | Press `Win + R`, type `cmd.exe`; or use Start Menu → "Terminal"                                    | Use Git Bash for consistency with Unix-style commands [1]                                                                                                              |
| **macOS**                  | zsh (default in bash/zsh shells)                     | Applications folder → Terminal app; press `Cmd + Space` then type `terminal.app`                   | Comes pre-installed on all Macs. Install Homebrew if needed via: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"` [1] |
| **Linux** (Ubuntu, Fedora) | bash or zsh depending on distro                      | Press `Ctrl + Alt + T`; type `gnome-terminal`, `xfce4-terminal` etc. to get specific one if needed | Pre-installed; may need to install Git later for version control [1]                                                                                                   |

---

## 2. Basic Navigation Commands (Linux/Mac)

### Changing Directories
```bash
# Go back up a directory level
cd ..  

# Navigate into subdirectories - note: no spaces around > or / unless it's part of the name!
cd Documents/Work_Projects/final_report
# or with single-quoted paths for safety (if path contains special characters):
cd 'Projects/new_project/'
```

### Showing Current Location and Contents
```bash
pwd          # Print Working Directory: shows your full current location. Use -P to get absolute physical path, use ~ to see relative from home folder [1]  
ls           # List directory contents without options (basic usage)
ll           # ls with long format (more detail than basic listing; some systems show file type/permissions). Alternative for Mac: `stat filename` or `open -g .` shows extended info in Finder via GUI. For terminal, use `-lh` flag to see human-readable sizes [1]  
cd ~        # Go home folder
```

### Viewing Files and Directories with Detail (useful before Git work)
| Command         | Purpose                                                                                           | Example Output Info |
| --------------- | ------------------------------------------------------------------------------------------------- | ------------------- |
| `ls -l` / `-lh` | Long format; human-readable sizes. On Mac use instead: stat command in terminal or GUI Finder [1] |
```bash
-rw-r--r--   4 alice    users    docfiles     Feb 25 09:37 README.md

# Permissions breakdown (Mac alternative): 
stat -f "%Su" filename        # Shows owner name on Mac via stat command in terminal instead of ls -l showing detailed permission bits [1]
``` | File permissions, size, date/time, user/owner |
| `ls -a` or `la` | List all items including `.hidden_files` (dot-prefixed). Files not normally shown are hidden on Linux/Mac but visible via Git if added to repo later. Use with caution in production environments [1]  
```bash
# This will show dotfiles and also help see what needs .gitignore attention:
ls -lah

# On Mac alternative using stat command shows file properties like size/owner/date for each item separately (not batch listing) unless looped over filenames [1] |
| `tree` or similar recursive directory tools | Visualizes folder structure hierarchically. Git tracks files at multiple levels in subdirectories, so you should be able to navigate nested directories easily beforehand via these navigation skills taught here [1]|  
```bash
# install tree if not present (Mac: brew install tree; Linux apt/brew): 
sudo apt-get install git  # Install both tree and git together since Git depends on it! Also installs other dependencies needed for version control. On Mac, use homebrew to get these tools quickly via `brew` command [1]  
tree -L 2 /home/project

# Shows directory structure; useful before initializing a repo or checking what will be committed. Files like .git are created here when you run git init on any folder in your current working dir (cwd) for project version control tracking, which is where this lesson comes right into play after understanding these commands [1]|
``` | Hierarchical directory tree view; shows depth up to specified level (-L 2 means show 2 levels deep). Git tracks files at all depths within the repository structure you've navigated using `cd` and folder navigation skills from here, so knowing how folders work with `-a` flag revealing hidden dotfiles (including `.git`, which is invisible until created) helps when preparing to initialize version control tracking [1]|
| Use: `ls /home/user/project/`. If `/project` exists as a valid file path on your machine or network filesystem, navigate into it via cd command. This demonstrates understanding of absolute vs relative paths and directory hierarchy needed for Git work later [1] |

---

## 3. Creating Files and Directories (Prerequisites Before Version Control)

### Making New Content
```bash
# Linux/Mac: Create empty file + content in one step using touch or echo with redirection operator > to append/overwrite text into new .txt, etc.: 
touch sample_file.txt         # Creates empty file named 'sample_file' in current directory; useful before adding files to Git repo. Note that you may need mkdir command first if target folder doesn't exist yet [1]  
mkdir my_subfolder            # Create a brand new subdirectory with name "my_subfolder" (or any desired path); will fail if parent paths don't exist, so use cd .. as needed before running this from higher levels. For nested folders: mkdir -p /new/path/structure  creates all intermediate directories [1]  
cat sample_file.txt > README.md        # Create file with content; cat writes contents directly into new file via redirect operator which Git will later track once initialized in directory containing these files that were made here using touch and echo commands shown above. This is essential prep work before version control lessons can show you how to commit them [1]  
```

### Viewing File Content
| Command | Example Use Case Before Version Control Work Begins Here Now Via Cat Redirected Into New README Files Created Earlier in This Section So You Can See What Will Be Added When Git Init Happens On Current Working Directory (CWD), Making Those Dotfiles Visible to Git Afterward [1]  
```bash
cat filename.txt                 # Display contents of text file; shows everything that cat reads from stdin or redirects into terminal buffer before saving with > operator on right side after command executed, allowing previewing of files destined for version control tracking via git add and commit workflow taught in next lesson. Use -n flag to show line numbers helpful when reviewing diffs [1]  
cat README.md    # Display full contents if file exists from earlier steps creating new docfiles mentioned above before Git tracks them as changes ready to be committed once repository is initialized here at current location using init command shown below which creates hidden .git folder for version control tracking all files created via touch/echo commands in this primer. This prepares you mentally and practically for what git add, commit, push will do later [1] |

# On Mac or Linux: Use head/tail to view specific file lines if full cat output is too long (Git diffs often show partial changes rather than entire files). tail -n +3 means "show from line 3 onward" so you can quickly skip first few irrelevant sections before committing relevant parts of changed document [1]  
``` |

---

## 4. File Permissions and Operations
On Linux/Mac: permissions affect who can read/write/execute each file in directory hierarchy (useful when preparing codebase for team sharing where `.git` folder contains hidden version tracking metadata). Commands like chmod/chown help manage access levels needed before Git repo setup so collaborators know what files are visible/editable via pull request workflow taught later [1]:

```bash
chmod +x script.sh              # Make file executable (Git tracks changes including permission shifts)  
rm oldfile.txt                  # Remove unwanted files; use with caution! .git directory is never deleted manually because it contains version history data you cannot recreate without using git reflog or clone from remote repository. Always verify target filename before deletion since accidental rm of tracked source code can be recovered via git checkout but lost permissions/data otherwise [1] |
```

**Git-Specific Note:** Version control systems protect against destructive changes during development workflow because committed snapshots preserve previous states accessible via `git log`, `git show --full-diff` etc. Always test risky commands first on backup or local copy before applying production-level changes to live project repositories managed through Git workflows [1].

---

## 5. Windows Command Prompt vs PowerShell Basics (Prerequisites for Cross-Platform Version Control Work)

### Basic Equivalent Commands
| Unix/Linux/Mac | CMD/PowerShell equivalent | What It Does Before Git Init Happens in Either Environment Via Terminal Window Opened Here Now Showing How to Match Paths Between Systems So You Can Use Git on Any OS Without Confusion When Commits Get Made Locally or Pushed Remotely [1]  
```bash
cd ..                    # cd ParentDir equivalent; PowerShell: cd -Parent  if using native Win shell features instead of WSL (Windows Subsystem for Linux) which lets you run true bash commands natively on Windows without needing separate Docker container running Ubuntu/Linux inside it separately from your main desktop apps unless explicitly desired by user who prefers dual-environment setup [1]  
cd ~ /home/user         # Same as PowerShell's $HOME variable; cd HomeDir in cmd.exe (case-insensitive on some setups) or use `&` operator to chain commands like `echo Hello & pwd`. Git works identically whether running via git-bash on Windows, native CMD/PowerShell using WSL features for full Unix compatibility with Linux-style paths shown above [1]  
pwd                     # PowerShell: $PWD; cmd.exe: showcurrentdirectory or use echo %cd% to display current working location. Note that Git accepts forward slashes (/) instead of backslashes (\) even in Windows because path normalizer converts them internally when git init creates initial commit tracking structure for codebase containing files made earlier with mkdir/touch/echo commands taught previously here, making version control consistent across platforms [1]  
ls                       # PowerShell: dir; cmd.exe: dir (shows directory contents including .hidden ones if using ls -a flag which works in both Git Bash on Windows and native shell via homebrew tools installed beforehand to enable Unix-style development workflow compatible with cross-platform team collaboration where teammates use different OS versions simultaneously. Version control systems abstract away path differences automatically once initialized properly after learning these basic command skills [1] |

``` |

--- 

## 6. Copy, Move, Delete Operations (Essential Before Making Git Commits)
| Operation | Linux/Mac Command Sequence for Prep Work  
Copy files to version control directory before adding them: `cp file.txt destination/`. Note that cp -r recursively copies directories with all nested subdirectories and their contents including dotfiles. This mirrors what you'd do when preparing a project folder structure ready for git init tracking [1]. For Mac users specifically who may use Finder GUI alongside terminal commands, both approaches work but Git prefers explicit paths without spaces unless quoted appropriately around special character filenames encountered during collaborative development workflows managed via GitHub/GitLab/etc later in your version control journey. Always test copy/delete operations before making irreversible changes to tracked repositories because accidental rm -rf can destroy commits if not properly backed up first using git log or reflog commands taught next [1].  
Move files within directory hierarchy: mv filename.new other_location/.  Note that this operation renames and relocates file in single step, unlike separate cp+rm approach which takes longer than needed for typical development work. Git tracks these changes automatically once repository initialized here at current location after mastering basic file management skills taught throughout this primer section [1].  
Delete files: rm filename.txt; use rm -rf with extreme caution because it bypasses normal confirmation prompts and removes directories recursively without asking permission before proceeding destructively unless you interrupt or stop command mid-operation. Never delete .git folder manually even if accidentally created during git init since version history is stored there exclusively for later retrieval via checkout commands showing changes made between commits in your project repository managed through GitHub/GitLab/etc services shown next [1] |

```bash
# Example: Copy all files from development directory before committing them to remote branch on Git server: 
cp -r dev_project/. production_server/path/to/repo/   # Copies entire folder structure including dotfiles and subdirectories using recursive flag (-r) so everything gets transferred automatically without needing individual file listing first. After copy completes successfully via terminal commands shown earlier in this primer, you're ready to add these newly copied files to Git tracking system for version control management throughout project lifecycle [1]  
``` |

**PowerShell equivalents:**
| Unix/Mac CMD/PowerShell Command Sequence Before Version Control Lesson Begins Properly Here Now Using Terminal Window Where You Can Test These Operations Yourself With Files Created Earlier via mkdir/touch Commands So You Understand What Will Be Added When Git Init Happens After Learning Navigation Skills Above [1]  
```bash
# Copy single file or entire directory recursively: 
Copy-Item -Path "file.txt" -Destination "$env:USERPROFILE\MyProjects\" -Recurse # Copies all subdirectories including dotfiles like .git once created later via git init command shown in next lesson. $env variable syntax differs from Linux $HOME which uses /home/user style paths instead of Windows C:/Users format used by PowerShell's native environment variables for accessing current working directory location or parent folders when needed before adding files to Git tracking system [1]  
Move-Item -Path "oldname.txt" -Destination "renamed_file.txt"  # Rename operation equivalent to mv command shown above but using Move-Item cmdlet instead of Unix-style syntax which works natively on Windows without needing WSL or Git Bash wrappers unless specifically desired for compatibility with cross-platform team members working remotely via GitHub/GitLab/etc. Use when preparing local copy that will eventually be committed after understanding basic file operations taught here in this primer lesson before version control workflow begins properly [1]  
Remove-Item -Path "file.txt"  # Deletes specified file; add Force flag if target has read-only permissions preventing normal removal attempts without additional permission elevation via sudo or Administrator account access granted to user running command prompt session from which these operations are being performed locally. Git won't automatically track files removed after deletion unless they're staged for addition again using git add -A/--all followed by commit showing all changes including deletions made during development process managed through version control tools shown in next lesson [1] |

``` |
--- 

## 7. Quick Reference Cheat Sheet (Use While Learning Git)

| Action | Terminal Command (Linux/Mac/Git Bash on Windows) | PowerShell Equivalent  
Copy current working directory contents to clipboard: `xclip -selection clipboard` or macOS pasteboard command for copying files directly from terminal window into GUI text editor used later when editing tracked repositories [1]
```bash
cd project_dir                    # Navigate first before committing anything via git add/commit commands shown next. Always test navigation skills here using ls pwd cd operations taught throughout this primer so version control workflow can proceed smoothly once init happens on current working directory path after mastering these basic terminal skills in prior lesson steps [1] |

```bash
pwd                              # Print full physical location of files being prepared for Git tracking system initialization via git init command shown below. This is essential before committing any changes because you must know which branch/remote repository corresponds to codebase currently located at printed path using pwd output as confirmation target matches expected version control server URL [1] |

```bash
ls -la /current/path/file.txt    # List all files in current working directory including hidden ones created during earlier steps of this primer lesson. Git tracks .git folder automatically after running git init command shown below, making it visible only once initialized rather than appearing before version control setup occurs [1] |

```bash
mkdir new_folder                 # Create fresh subdirectory for project codebase structure ready for initializing version control tracking system via git add/commit push workflow taught in next lesson. Always test mkdir -p with nested paths first so .git gets created properly after understanding folder hierarchy skills shown here earlier [1] |
```

--- 

## 8. Git-Specific Preparation Commands (Run After Learning Above Basics, Before Next Lesson Starts)

### Initializing a Repository (Git-specific; runs after file creation/navigation lessons above are complete):
```bash  
git init                         # Creates hidden .git folder containing all version tracking metadata for codebase currently in working directory path shown by pwd command earlier. This marks current location as tracked repository ready to receive commits via add/commit push commands taught next [1] |

# Important: Never delete this manually once created! If accidental damage occurs, use git reflog or clone remote backup instead of manual removal attempts unless fully certain target folder is empty and safe for deletion without destroying project history. Git protects against destructive operations by keeping all commits accessible via log command showing complete revision history even after local changes [1] |

```bash
git status                       # Shows current state: staged files, working directory modifications vs already committed snapshots in remote repository managed through GitHub/GitLab/etc services shown next lesson where pull requests and code reviews happen. Git tracks unstaged changes (unsaved editor work), staged additions ready to commit, and untracked new or modified files not yet added via git add command [1] |

# This helps you understand what will be committed after running init above: 
git status -s                    # Compact output showing only file names + change type. Useful for quick assessment before adding anything manually one-by-one using ls commands shown earlier in this primer to navigate folder structure properly when preparing repository contents ready for commit [1] |
```

--- 

## Conclusion  
This lesson prepared you with essential terminal navigation and file operations needed before advancing into version control systems like Git, which will be covered next. Mastery of these basics ensures smooth progression through more advanced concepts without technical roadblocks preventing forward progress in collaborative development workflows managed via remote repositories hosted on GitHub/GitLab/etc services shown now [1].

**Remember:** Always test commands first in safe environments (e.g., personal backup copy) before applying destructive operations to production-level projects where version control protects against accidental data loss during development workflow activities taught throughout this primer lesson series leading into next course module covering Git fundamentals and collaborative coding practices using pull requests shown above [1].