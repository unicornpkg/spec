**Package tables** are the primary way of setting up packages with unicornpkg. They are a Lua table or a function that returns a Lua table.

The only required fields are `name` and `pkgType`, but more are recommended if you want your package to be useful.

## Fields
### `unicornSpec`

This specifies the version of the package table. This should always be set to `v1.1.0`.

### `name`

This should be the same as the filename without the `.lua` extension.

### `desc`

A description of the contents of the package table. Can be single-line or multiline.

### `homepage`

A link to the program's homepage, if it has one.

### `maintainer`

The name or pseudonym of the maintainer of the package table.

### `licensing`

The license of the package's contents, expressed as an [SPDX License Expression](https://spdx.github.io/spdx-spec/v3.0.1/annexes/spdx-license-expressions/) as defined in the SPDX Specification, v3.0.1.

Package definitions MAY be a different license from the license of the package's contents.

#### SPDX extensions

Packages MAY use `CCPL` and `MMPL` in license expressions to refer to the ComputerCraft Public License and Minecraft Mod Public License, respectively. New projects SHOULD refrain from using these licenses. If `CCPL` or `MMPL` ever become defined in the SPDX License List, those definitions MUST take precedence.

Other than the exceptions above, implementations SHOULD avoid other extensions to the SPDX License List.

### `version`

The version of a package. If a project does not have versioning, this value SHOULD be set to `nil`.

This field expects a valid [SemVer](https://semver.org) string, without the `v` prefix.

### `instdat`

A table that contains more tables that have information specific to package providers.

Each table should be structured like this:

```lua
{
	{
		provider = "com.github";
		repo_owner = "unicornpkg";
		repo_name = "cli";
		filemaps = {
			["unicorntool/init.lua"] = "/bin/unicorntool.lua";
			["doc/man/unicorntool.txt"] = "/usr/share/help/unicorntool.txt";
		};
	};
	{
		provider = "com.github"; -- You can do multiple tables with the same `provider` value!
		repo_owner = "unicornpkg";
		repo_name = "some-nonexistent-repo";
		filemaps = {
			["init.lua"] = "/bin/some-nonexistent-program.lua";
		}
	};
}
```

See individual [package providers](./package-providers.md) for more information.

### `script`

A table that contains scripts that should be called at various points in the package's life.

#### `script.preinstall`

A block of Lua source code that is called before the package table is installed.

#### `script.postinstall`

A block of Lua source code that is called after the package table is installed.

#### `script.preremove`

A block of Lua source code that is called before the package is removed.

#### `script.postremove`

A block of Lua source code that is called after the package is removed.

### `security`

A table that contains hashes and other security-related data.

#### `security.sha256`

A table that contains a name of the installed file (e.g. `/bin/some-nonexistent-program.lua`) and the corresponding SHA-256 hash (e.g. `00000000000000000000000000000000000000000000000000000000000000000`).

### `rel`

A table that contains information relating to other packages.

#### `rel.depends`

A table that lists required packages.

#### `rel.conflicts`

A numbered table that lists packages which break when they are installed with this package.
