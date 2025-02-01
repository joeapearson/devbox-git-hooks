# devbox-git-hooks

A plug-in that integrates git hooks with [devbox], particularly useful for running a `pre-commit` script defined in
devbox.

## Usage

### Installation

Add `"github:joeapearson/devbox-git-hooks"` to your [devbox.json] `include` list.

### Adding hooks

1. Add a script to your [devbox.json] `shell.scripts` map matching the name of the git hook you'd like to invoke devbox. For example, `"pre-commit"`, `"post-commit"` and so on.
2. `.git/hooks` will be checked for an existing hook. If one exists, it'll be left unmodified.
3. If not already existing, a hook will be created, pointing to `devbox run HOOK_NAME`

More information on git hooks is found [here](https://git-scm.com/docs/githooks).

### Removing hooks

1. Remove the entry from `shell.scripts`.
2. Check and delete the associated `.git/hooks/HOOK_NAME`

### Example devbox.json

```json
{
  "$schema": "https://raw.githubusercontent.com/jetify-com/devbox/0.13.7/.schema/devbox.schema.json",
  "packages": ["shellcheck@latest"],
  "shell": {
    "scripts": {
      "pre-commit": ["shellcheck *.sh"]
    }
  },
  "include": ["github:joeapearson/devbox-git-hooks"]
}
```

Demonstrates how you might use [shellcheck] to lint shell scripts before committing changes.

### CI environments

If `CI` environment variable is set then this plug-in does nothing.

[devbox]: https://www.jetify.com/docs/devbox
[devbox.json]: https://www.jetify.com/docs/devbox/configuration/
[shellcheck]: https://www.shellcheck.net
