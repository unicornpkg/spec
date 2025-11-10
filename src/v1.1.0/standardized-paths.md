unicornpkg recommends the following paths for package contents:

- `/bin` for executable Lua files. This path should be on `shell.path`.
- `/lib` for modules, APIs, and libraries. This path should be on `package.path` if you're writing complementary software.
- `/usr/share/help/` for help files. This path should be on `help.path`.
- `/etc/startup` for files that should be executed when starting the machine.
    - Implementations MAY encourage use `/startup` instead when compatibility with older versions of ComputerCraft is not desired. Such older versions require `/startup` to be a file.
- `/home` for user data, or `/home/{user}` if you are writing a multi-user system.

If your use-case is not specified here, follow IEEE 1003.1-2017 (POSIX).
