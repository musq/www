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
| [`Hugo`][hugo] | Static site compiler |
| [`Hello Friend theme`][hello-friend-theme] | Custom theme |


## Install

```bash
# Clone this repo
git clone --recurse-submodules git@github.com:musq/www.git

# Go inside
cd www

# Run local server
hugo server -t hello-friend

# Run local server (env - production)
hugo server -t hello-friend --disableFastRender -e production
```


## Build

```bash
# Generate build
hugo -t hello-friend
```


## Deploy

Use [`www-config`][www-config] to deploy.


## License

The code is available under [GNU GPL v3, or later](LICENSE) license.


<!-- Link labels: -->

[hugo]: https://gohugo.io/
[hello-friend-theme]: https://github.com/musq/hugo-theme-hello-friend
[www-config]: https://github.com/musq/www-config
