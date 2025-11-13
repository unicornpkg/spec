**Package remotes** are a feature in unicornpkg that allow you to download package tables semi-automatically.

## Specification
### Remote

The remote is a simple HTTPS server. It's usually a GitHub repository, but other hosts should work fine.

Each package should be a file on the package remote ending in `.lua`.

All packages on the remote should return valid package tables.

### Retrieval on the client

The client will have a folder called `/etc/unicorn/remotes/` that will contain one serialised file per remote. Each serialised file should contain a `url` keyword specifiying the full HTTP path to the remote, as well as a `packages` table that contains known packages from that remote.

`unicorn.hoof.update()` should parse each file in `/etc/unicorn/remotes` and update the `packages` table.

`unicorn.hoof.get()` should parse each file in `/etc/unicorn/remotes/` and download the requested file to `/tmp/unicorn/{package_name}.lua`, and then `unicorn.install()` should install said file.
