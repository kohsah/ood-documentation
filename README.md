# OOD Documentation

Go to https://osc.github.io/ood-documentation/master/

Or select your version:

- [Development](https://osc.github.io/ood-documentation/develop/)
- [Latest Stable](https://osc.github.io/ood-documentation/master/)
- [1.2](https://osc.github.io/ood-documentation/release-1.2/)
- [1.1](https://osc.github.io/ood-documentation/release-1.1/)
- [1.0](https://osc.github.io/ood-documentation/release-1.0/)

## Development

There are two ways to build the documentation.

1. Use the Docker image that is used to build them in production using Travis.
2. Use pipenv to install local dependencies. `pipenv` has become the [recommended
   package to use by python.org for dependency
   management](https://packaging.python.org/tutorials/managing-dependencies/)

#### Docker

Currently all builds are generated using the
[docker-sphinx](https://github.com/OSC/docker-sphinx/) Docker image. They are
built using the following command from the root of this repo:

```bash
docker run --rm -i -t -v "${PWD}:/doc" -u "$(id -u):$(id -g)" ohiosupercomputer/docker-sphinx make html
```

Or use the rake task added:

```bash
rake docker:build
```

#### pipenv

If you don't want to use Docker, you can also use pipenv.

1. Ensure plantuml and graphviz are installed:

   ```bash
   # on OS X
   brew install plantuml
   brew install graphviz
   ```

2. Install pipenv and use it to install dependencies in same directory:

   ```bash
   pip install -g pipenv

   # then in the documentation root directory:
   WORKDIR=/doc PIPENV_VENV_IN_PROJECT=1 pipenv install

   # or using handy rake task:
   rake pipenv:install
   ```

When building the docs, run this command:

```bash
WORKDIR=/doc PIPENV_VENV_IN_PROJECT=1 pipenv run make html
```

or use the rake task:

```bash
rake pipenv:build

# or

rake build
```

## Contributing

Bug reports and pull requests are welcome on GitHub at
https://github.com/OSC/ood-documentation.

## License

* Documentation, website content, and logo is licensed under
  [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)
* Code is licensed under MIT (see LICENSE.txt)
