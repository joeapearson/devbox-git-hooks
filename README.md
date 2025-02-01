# devbox-git-hooks

A plug-in that integrates git hooks with [devbox], particularly useful for running a `pre-commit` script defined in
devbox.

## Usage

1. Add `"github:joeapearson/devbox-git-hooks"` to your [devbox.json] `include` list.
2. Add scripts to your [devbox.json] `shell.scripts` map matching the name of the git hook you'd like to invoke devbox.

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

When activated:

1. `.git/hooks` will be checked for an existing `pre-commit` script. If one exists, it'll be left unmodified.
2. If not already existing, a `pre-commit` script will be created, pointing to `devbox run pre-commit`

### CI environments

If `CI` environment variable is set then this plug-in does nothing.

[devbox]: https://www.jetify.com/docs/devbox
[devbox.json]: https://www.jetify.com/docs/devbox/configuration/
