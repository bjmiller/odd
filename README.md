# odd

Check a project's dependencies for outdated packages, like `npm outdated`, with an additional column showing when the latest version was published.

## Install

Node.js and npm are required.

From this repository, copy the `odd` file into any location on your path.

## Usage

```text
Usage: odd [options] [path]

Check a project's package.json for outdated dependencies, like `npm outdated`,
and add a "Published" column showing how long ago the latest version of each
package was published. Packages published within the cooldown period are
highlighted in red.

The project directory defaults to the current directory, walking up parent
directories until a package.json is found.

Options:
  -h, --help          Show this help message and exit

  -u, --upgrades      Print space-separated names of outdated packages that are
                      safe to upgrade (latest version published before the
                      cooldown) AND actionable by `npm upgrade` (the declared
                      version spec allows moving to a newer version). Intended
                      for: npm upgrade $(odd -u)

  -m, --major-upgrades
                      The inverse of --upgrades: packages that are safe to
                      upgrade but whose version spec blocks `npm upgrade`
                      (wanted === current while a newer latest exists). Names
                      get an `@latest` suffix for forcing with:
                      npm install $(odd -m)

  -c, --cooldown <time>
                      Set the safety cooldown used for the red highlight and
                      the --upgrades/--major-upgrades filters. <time> is an
                      abbreviated duration: 90s, 30m, 12h, 7d, 2w, 3mo, 1y
                      (a bare number means days). Default: 7d

Exit status:
  0  no outdated packages were found (or in --upgrades/--major-upgrades mode)
  1  outdated packages were found, or an error occurred

Environment:
  ODD_CACHE_DIR       Override npm's cache location (default ~/.npm/_cacache)
  ODD_CACHE_TTL       Cache trust window in minutes (default 60; 0 disables)
  NO_COLOR            Disable colored output
  FORCE_COLOR         Force colored output even when not attached to a TTY
```
