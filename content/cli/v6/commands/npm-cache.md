---
title: npm-cache
section: 1
description: Manipulates packages cache
github_repo: npm/cli
github_branch: v6
github_path: docs/content/commands/npm-cache.md
redirect_from:
  - /cli-documentation/v6/cache
  - /cli-documentation/v6/cli-commands/cache
  - /cli-documentation/v6/cli-commands/npm-cache
  - /cli-documentation/v6/commands/cache
  - /cli-documentation/v6/commands/npm-cache
  - /cli-documentation/v6/npm-cache
  - /cli/v6/cache
  - /cli/v6/cli-commands/cache
  - /cli/v6/cli-commands/npm-cache
  - /cli/v6/commands/cache
  - /cli/v6/npm-cache
---

### Synopsis

```bash
npm cache add <tarball file>
npm cache add <folder>
npm cache add <tarball url>
npm cache add <name>@<version>

npm cache clean [<path>]
aliases: npm cache clear, npm cache rm

npm cache verify
```

### Description

Used to add, list, or clean the npm cache folder.

* add:
  Add the specified package to the local cache.  This command is primarily
  intended to be used internally by npm, but it can provide a way to
  add data to the local installation cache explicitly.

* clean:
  Delete all data out of the cache folder.

* verify:
  Verify the contents of the cache folder, garbage collecting any unneeded data,
  and verifying the integrity of the cache index and all cached data.

### Details

npm stores cache data in an opaque directory within the configured `cache`,
named `_cacache`. This directory is a `cacache`-based content-addressable cache
that stores all http request data as well as other package-related data. This
directory is primarily accessed through `pacote`, the library responsible for
all package fetching as of npm@5.

All data that passes through the cache is fully verified for integrity on both
insertion and extraction. Cache corruption will either trigger an error, or
signal to `pacote` that the data must be refetched, which it will do
automatically. For this reason, it should never be necessary to clear the cache
for any reason other than reclaiming disk space, thus why `clean` now requires
`--force` to run.

There is currently no method exposed through npm to inspect or directly manage
the contents of this cache. In order to access it, `cacache` must be used
directly.

npm will not remove data by itself: the cache will grow as new packages are
installed.

### A note about the cache's design

The npm cache is strictly a cache: it should not be relied upon as a persistent
and reliable data store for package data. npm makes no guarantee that a
previously-cached piece of data will be available later, and will automatically
delete corrupted contents. The primary guarantee that the cache makes is that,
if it does return data, that data will be exactly the data that was inserted.

To run an offline verification of existing cache contents, use `npm cache
verify`.

### Configuration

#### cache

Default: `~/.npm` on Posix, or `%AppData%/npm-cache` on Windows.

The root cache folder.

### See Also

* [npm folders](/cli/v6/configuring-npm/folders)
* [npm config](/cli/v6/commands/npm-config)
* [npmrc](/cli/v6/configuring-npm/npmrc)
* [npm install](/cli/v6/commands/npm-install)
* [npm publish](/cli/v6/commands/npm-publish)
* [npm pack](/cli/v6/commands/npm-pack)
* https://npm.im/cacache
* https://npm.im/pacote
