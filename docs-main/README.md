![Verity](https://be-network.github.io/docs/images/Verity-Logo.png)

This documentation is publicly accessible at https://be-network.github.io/docs/

The official public URL is https://docs.be-net.com

**Windows** and **MAC** Users probably want to drop down to the end.

## Security Toolchain

This repository uses a standardized security baseline implemented via GitHub Actions workflows:

- `.github/workflows/security-baseline.yml`

SAST:

- `.github/workflows/codeql.yml`

Dependency update automation:

- `.github/dependabot.yml`

Central standard:

- https://github.com/BE-Network/verity-monitoring/blob/main/SECURITY_TOOLCHAIN_STANDARD.md

# Contributing

## How to Contribute (Recommended)

1. Clone this repo to your desktop.

2. Set up your python3 environment as usual, and use [venv](https://docs.python.org/3/library/venv.html) or [pipx](https://github.com/pypa/pipx) to isolate libraries from stomping on each other.  

Setup mkdocs env:
```cat requirements.txt | sed -e 's/#.*//' | xargs pipx inject mkdocs```

Then:

```mkdocs serve```

3. Create a branch with your initials + dash + feature/title (ex. js-fixed_typos).
4. Commit your changes to the branch.
5. Submit a PR to main or the release branch you are working on.

Note:

These documents are written in Markdown. Editing and previewing can be done with any off the shelf Markdown editor including VS Code. To view documentation in its rendered web form simply run the command above and browse to the 
127.0.0.1 URL provided in the output.


## Using Git/Github

Contributing to this repository is currently limited to BE Networks employees.

## Windows Users - Local Setup

1. Install Git.
1. Make sure you run:
    ```
    git config --global user.name "John Doe"
    git config --global user.email johndoe@example.com
    ```
1. Install pipx.
    1. At the end of the install you will get a warning like "WARNING: The script pipx.exe is installed in `<USER folder>\AppData\Roaming\Python\Python3x\Scripts` which is not on PATH"
    1. Navigate to this directory.
    1. Run **.\pipx.exe ensurepath**
1. Open a new terminal session to get your updated PATH.
1. Run **pipx** and make sure it works properly.
1. Git clone this directory to your computer, wherever you want.
    1. i.e **git clone https://github.com/BE-Network/docs.git**
1. Navigate to the directory in your terminal.
1. Run the following commands:

    ```
    pipx install mkdocs
    pipx install mkdocs-material
    pipx inject mkdocs mkdocs-material
    pipx inject mkdocs mike 
    pipx inject mkdocs pymdown-extensions
    pipx inject mkdocs mkdocs-glightbox
    pipx inject mkdocs mkdocs-macros-plugin
    pipx inject mkdocs mkdocs-with-pdf
    pipx inject mkdocs mkdocs-swagger-ui-tag
    pipx inject mkdocs mkdocs-unused-files
    ```

1. Run **mkdocs serve**
1. You should see that the server is running and you can open your browser to http://127.0.0.1:8000 and see the site running locally on your laptop.

## Windows Users - Using Git

Do this before continuing:

1. Open a terminal and go into the docs repo and enter **git checkout -b <yourname>-edits**.  This creates your own branch of the repo where you can make and commit changes.
1. Git will automatically track changes to files in the docs repo.  Most of the docs you willneed to edit are in the /docs subdirectory.  If you edit and save a file it will automatic
1. After saving an edit, you can type **git status** to see the files that have been changed.
1. To add a changed file to your branch type "git add <filename>. Typing git status again will show you that it has been added.
1. When you have completed all of your changes type **git commit -m "/<commit message/>"**.
1. Type **git push origin <yourname>-edits** to push the branch to github.
1. The output of this command will give you a link where you can create a pull request to get this branch added to the main release branch.  This is what will update the public docs with your changes.

## Windows Advice

1. It's going to be best to use a fully integrated editor that includes git/terminal/etc.  It will be easier to use one window rather than 3-4.
1. Using WSL is advisable, this is tested against Ubuntu/OSX.
1. In addition to seeing repo status in VS Code, I suggest using power-level-10k: https://github.com/romkatv/powerlevel10k so you can see your git status in the prompt.  It will help in the long run.

## Apple Mac OSX

1. Use brew to install git, iterm2, and powerlevel10k.
1. Use the linux instructions above, they should work.
1. Enjoy.