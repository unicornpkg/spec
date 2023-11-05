**Package remotes** are a feature in unicornpkg that allow you to download package tables semi-automatically from a server.

## Specification
### Remote

The remote must be a simple HTTPS server. HTTP is allowed, but discouraged. Remotes may also be folders located anywhere in the filesystem. Write access to these filesystem-based remotes is not guaranteed, as some might be located in `/rom`.

Each package should be a file on the package remote ending in `.lua`.  Each package should return the `text/lua` or `text/plain` MIME types.

All packages on the remote, when evaluated, should return valid package tables.

All packages and their versions should be listed in a JSON file (the "manifest") available at `/unicornpkg.remote.json` on the remote. The JSON file should look like this:

```jsonc
{
  spec: "unicornpkg-1.1.0",
  packages: {
    "somepackage": "1.0.1",
    "examplepackage": "1.2.3",
    "anotherexamplepackage": null // No version available for this package; always specify a version where possible
  }
}
```

This file should return the `application/json` MIME type. Manifests should be automatically updated by a script where possible.

### Retrieval on the client

The client will have a folder called `/etc/unicorn/remotes/` that will contain one serialised file per remote. Each serialised file should contain a `url` keyword specifiying the full HTTPS path to the remote.

`unicorn.hoof.update()` should parse each file in `/etc/unicorn/remotes` and check for validity. It should download each remote's manifest into `/var/unicorn/remotes/remotename.json`.

`unicorn.hoof.get()` should parse each manifest in `/var/unicorn/remotes/`. It should evaluate the version strings, find the newest version for a package across all remotes, and then download and install the package table from the remote.
