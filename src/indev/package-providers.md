**Package providers** are the workhorse of unicornpkg; they allow you to use various online services to install packages.

Custom package providers can be created by having a `.lua` file in the `/lib/unicorn/provider` directory. That Lua file should return a single function which takes one argument (a package table) and installs a package table upon being called, with no interactive prompting.
