# dot files done right

That's the hope, anyway.

The idea is that you share config files across all projects. It should have files like `.prettierrc` that define the coding standard for all the projects, etc.

Any user preferences don't live here - put them in your home directory, or whereever the application wants them to be.

## How to use this repository

Add it as a git submodule to your project. Run the below in the root directory of you project

`$ git submodule add <this repository>`

This creates a submodule in the `dotfiles` directory off your project root.

Then, for each config file, or config directory, that you want, symlink the git submodule file to the one in the project root directory,

`$ ln -s dotfiles/projectroot/<config-file-or-directory> <config-file-or-directory>`

e.g.

`$ ln -s dotfiles/projectroot/.prettierrc .prettierrc`

> [!TIP]
> If you already have, e.g. a `.prettierrc`, before you create the symlink, you may want to
>
> `$ diff dotfiles/projectroot/.prettierrc .prettierrc`
>
> To check you're not trashing your own carefully crafted config. It should be stored in git anyway so you never lose anything.

> [!WARNING]
> For `.vscode` files `settings.json` and `launch.json`, you need to symlink the directory, because for some reason (probably windows symlink limitations) symlinks for the files don't work:
>
> `$ ln -s dotfiles/projectroot/.vscode .vscode`

> [!NOTE]
> There's no script to do this as others have done for good reasons:
>
> - You may not want all of it and this way allows you to link just the files you need
> - The commands are easy to get right, and if you don't get it right first time it's easy to fix.
> - It's a one-off command for a only few files files, deal with it :smiley:
> - Any script needs tests, etc. and my cost-benefit analysis of this resulted in me not writing a script.

> [!TIP]
> So that there's a chance this might work on windows, do this:
>
> `$ git config --global core.symlinks true`
>
> This tells `git` to try its best with symlinks on windows.

## Updating dotfiles from the source repository

When someone else has added an enhancemenrt that you want do this:

`$ git submodule update --remote dotfiles`

This updates your `dotfiles` submodule and so all symlinked files are updated in one go. Magic!

## Updating your local copy and pushing it to the source repository

`$ cd dotfiles`

> [!WARNING]
> Make sure your git submodule is not detached - if it is:
>
> `$ git checkout main`
>
> follow the instructions to create a new branch from the detached head, e.g.
>
> `$ git branch <new-branch-name> <the hash it gave you>`
>
> make sure main is up to date
>
> `$ git fetch`
>
> `$ git pull`
>
> switch it all to your new branch
>
> `$ git checkout <new-branch-name>`
>
> `$ git merge main`

If the git submodule is not detached

` $ git checkout <new-branch-name>`

Everything is now on your new branch which you can now create a pull request from

## Benefits of this approach

You get to store you config across all projects in one place.

You can update the config from any of your projects and upgrade each of the other projects as needed.

## Caveats

It's not tested on windows, where symlinks don't work so well.

(try cmd /c mklink C:\Users\me\AppData\Roaming\Code\User\settings.json C:\git\config\.vscode\settings.json)

Many don't like git submodules. Yes, I agree, they are a [scunner](https://dsl.ac.uk/entry/dost/scunner_n 'Scots word scunner'), but they do the job right for this purpose, at least, [IMHO](https://en.wiktionary.org/wiki/IMHO).
