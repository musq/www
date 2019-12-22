# www

Source code of — tug.ro


## Table of Contents

- [Requirements](#requirements)
- [Install](#install)
- [Build](#build)
- [Deploy](#deploy)
- [License](#license)


## Requirements

| Dependencies | Purpose |
|:---|:---|
| [`Bundler`][bundler] | Ruby's dependency resolver |
| [`Jekyll`][jekyll] | Static site generator |


## Install

```bash
# Clone this repo
git clone --recurse-submodules git@github.com:musq/www.git

# Go inside
cd www

# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve
```


## Build

```bash
# Generate build
bundle exec jekyll build
```


## Deploy

Use [`www-config`][www-config] to deploy.


## License

The code is available under [GNU GPL v3, or later](LICENSE) license.


<!-- Link labels: -->

[bundler]: https://bundler.io/
[jekyll]: https://jekyllrb.com/
[www-config]: https://github.com/musq/www-config
