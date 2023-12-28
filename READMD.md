# dot files done right
That's the hope, anyway.

The idea is that you share config files across all projects. It should have files like .prettierrc that define the coding standard for all the projects, etc.

Any user preferences don't live here - put them in your home directory

## How to use this repository
Add it as a git submodule to your project. Run the below in the root directory of you project

`$ git submodule add <this repository>`

This creates a submodule in the dotfiles directory off your project root.

Then, for each config file, or config directory, that you want, symlink the git submodule file to the one in the project root directory, 

`$ ln -s dotfiles/projectroot/<config-fire-or-directory> <config-fire-or-directory>`

e.g.

`$ ln -s dotfiles/projectroot/.prettierrc .prettierrc`

If you already have e.g. a `.prettierrc`, before you create the symlink, you may want to

`$ diff dotfiles/projectroot/.prettierrc .prettierrc`

To check you're not trashing your own carefully crafted config. It should be stored in git anyway so you never lose anything.

There's no script to do this as others have done. That's because:
* you may not want all of it and this way allows you to link just the files you need
* the commands are easy to get right, and if you don't get it right first time it's easy to fix.
* it's a one-off command for a few files files, deal with it :-)
* any script needs tests, etc. and my cost-benefit analysis resulted in not writing a script

So that there's a chance this might work on windows, do this:

`$ git config --global core.symlinks true`

This tells `git` to try its best with symlinks on windows. 

## Benefits of this approach
You get to store you config across all projects in one place.

You can update the config from any of your projects and upgrade each of the other projects as needed.

## Caveats

It's not tested on windows, where symlinks don't work so well. 



