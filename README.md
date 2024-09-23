# dot files done right

That's the hope, anyway.

The idea is that you share config files across all projects. It should have files like `.prettierrc` that define the coding standard for all the projects, etc.

Any user preferences don't live here - put them in your home directory, or whereever the application wants them to be.

## How to use this repository

Add it as a forge package (a git submodule under the hood) to your project.

```shell
$ cd <project root>
$ forge install baofinance/dotfiles
```

This creates a library `lib/dotfiles` directory alonside all your other dependencies.

Then, for each config file that you want, symlink the file in the `lib\dotfiles\projectroot` to the respective place in your project,

``` shell
$ ln -s .lib/dotfiles/projectroot/<config-file-or-directory> <config-file-or-directory>`
```
e.g.

``` shell
$ ln -s .lib/dotfiles/projectroot/.prettierrc .`
$ ln -s ..lib/dotfiles/projectroot/.vscode/settings.json .vscode/settings.json`
```

> [!WARNING]
> make sure the symbolic link contains a relative path to the actual file.

> [!TIP]
> If you already have, e.g. a `.prettierrc`, before you create the symlink, you may want to
>
> `$ diff lib/dotfiles/projectroot/.prettierrc .prettierrc`
>
> To check you're not trashing your own carefully crafted config. It should be stored in git anyway so you never lose anything.

> [!TIP]
> To list all your symbolic links, you may want to add this to your `package.json` "scripts" section:
>
> `"dotfiles": "git ls-tree -r HEAD | grep 120000"`
>
> vscode marks symbolic links in the "Explorer" in the sidebar with a ↪️ character on the right

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

## Benefits of this approach

You get to store you config across all projects in one place.

You can update the config from any of your projects and upgrade each of the other projects as needed.

## Caveats

It's not tested on windows, where symlinks don't work so well.

(try cmd /c mklink C:\Users\me\AppData\Roaming\Code\User\settings.json C:\git\config\.vscode\settings.json)

Many don't like git submodules. Yes, I agree, they are a [scunner](https://dsl.ac.uk/entry/dost/scunner_n 'Scots word scunner'), but they do the job right for this purpose, at least, [IMHO](https://en.wiktionary.org/wiki/IMHO).
