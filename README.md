# Create a language library

🍏 + 🐍 = ❤️

**python-shortcuts** is a library to create [Siri Shortcuts](https://support.apple.com/en-ae/guide/shortcuts/welcome/ios) on your laptop with your favourite text editor.

The library is in a very early development state (PR welcome!), so it does not support all actions from Shortcuts app.

* [Toml tutorial](docs/tutorial.md)
* [Python tutorial](docs/python_tutorial.md)
* [How to add a new action](docs/new_action.md)
* [Supported actions](docs/actions.md)
* [Examples](examples/)
* [Changelog](CHANGELOG.md)
* [Documentation](docs/)

Supported Python version: **>=3.6**.

## Why

I wanted to convert my shortcut to a file in human-readable format. :)

From the code below this library can create a working shortcut:

```toml
[[action]]
type = "ask"
question = "What is your name?"

[[action]]
type = "set_variable"
name = "name"

[[action]]
type = "show_result"
text = "Hello, {{name}}!"
```

Or the same with Python:

```python
from shortcuts import Shortcut, actions


sc = Shortcut()

sc.actions = [
    actions.AskAction(data={'question': 'What is your name?'}),
    actions.SetVariableAction(data={'name': 'name'}),
    actions.ShowResultAction(data={'text': 'Hello, {{name}}!'})
]
```

## How to use

### Installation

```bash
pip install shortcuts
```

### Usage

### shortcut → toml

If you need to convert existing shortcut to a toml file, at first you need to export it.
Go into Shortcuts app, open the shortcut and share it. Choose "Share as file" and use this file with this library.

Convert shortcut file to `toml`:

```bash
shortcuts what_is_your_name.shortcut what_is_your_name.toml
```

### toml → shortcut

Convert a `toml` file to a shortcut file.
After you will need to open the file with iOS Shortcuts app.

```bash
shortcuts examples/what_is_your_name.toml what_is_your_name.shortcut
```

More examples of `toml` files you can find [here](examples/).
And [read the tutorial](docs/tutorial.md)! :)

### URL → [toml|shortcut]

Also, you can download shortcut directly from iCloud.
If somebody shared shortcut link with you, just run:

```bash
shortcuts https://www.icloud.com/shortcuts/... my_shortcut.toml  # or my_shortcut.shortcut
```

And it will download this shortcut and save it in `toml` or `shortcut` format.

### Docker

It's possible to use [pre-built Docker container] with python-shortcuts inside:

```shell
# convert s.toml from the current directory into s.shortcut

docker run -v $(pwd):/files akhmetov/shortcuts-cli /files/s.toml /files/s.shortcut


docker run -v $(pwd):/files akhmetov/shortcuts-cli --help

    usage: shortcuts [-h] [--version] [file] [output]

    Shortcuts: Siri shortcuts creator

    positional arguments:
      file        Input file: *.(toml|shortcut|itunes url)
      output      Output file: *.(toml|shortcut)

    optional arguments:
      -h, --help  show this help message and exit
      --version   Version information
```

## Development

### Tests

Run tests:

```bash
tox
```

### How to add a new action

See [documentation](/docs/new_action.md).

### TODO

* ☑ ~~Conditionals with auto-group_id: if-else, menu~~
* ☐ Nested fields: dict/array/etc
* ☐ Support variables in every field which support them in Shortcuts app
* ☐ Workflow types: widget, etc.
* ☐ Import questions
* ☐ Document all actions
* ☐ Support magic variables
* ☐ Support all current actions from Shortcuts app