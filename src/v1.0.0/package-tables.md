**Package tables** are the primary way of setting up packages with unicornpkg. They are a Lua table or a function that returns a Lua table.

The only required fields are `name` and `pkgType`, but more are recommended if you want your package to be useful.

## Fields
### `unicornSpec`

This specifies the version of the package table. This should always be set to `v1.0.0`.

### `name`

This should be the same as the filename without the `.lua` extension.

### `desc`

A description of the contents of the package table. Can be single-line or multiline.

### `maintainer`

The name or pseudonym of the maintainer of the package table.

### `licensing`

The license of the package and its contents. Should be a [valid OSI identifier](https://opensource.org/licenses/alphabetical), or `CCPL` if the license is the ComputerCraft Public License.

### `version`

The version of a package. If a project does not have versioning, do not fill out this field.

This field expects a valid [SemVer](https://semver.org) string, without the `v` prefix.

### `pkgType`

Specifies the package type; see [Package providers](./package-providers/index.md) for more information.

The string is formatted based on the domain of the provider; for example, GitHub's provider is `com.github`, and Bitbucket's provider is `org.bitbucket`.

### `instdat`

A table that contains information specific to the `pkgType`. See individual [package providers](./package-providers/index.md) for more information.

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

A table that contains a name of the file (`k`) and the corresponding SHA-256 hash (`v`).

### `rel`

A table that contains information relating to other packages.

#### `rel.depends`

A numbered table that lists required packages.

#### `rel.conflicts`

A numbered table that lists packages which break when they are installed with this package.
