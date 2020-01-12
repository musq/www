---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

## PGP Keys

|       Active      |          Old          |
|:-----------------:|:---------------------:|
| [013B49A9](/key/) | [C6976479](/key-old/) |

Import command: `curl -L {{ site.url }}/key | gpg --import`

## Projects

|       Name      |       Summary       |
|-----------------|---------------------|
| [syncs][syncs] | Standalone bash script to sync repository remote-local |
| [vim-autobackup][vim-autobackup] | Backup your work in vim every 2 minutes |
| [dotfiles-system][dotfiles-system] | Bash scripts to set up root environment as a system administrator |
| [dotfiles][dotfiles] | Bash scripts to set up local environment as a developer |
| [github-available-usernames][github-available-usernames] | Find out available usernames on GitHub |
| [iitd-proxy-hack][iitd-proxy-hack] | Scripts to get unlimited network quota at IIT Delhi |

## Self-hosted

- [CyberChef][self-cyberchef] — The Cyber Swiss Army Knife
([source][source-cyberchef])
- [Isso][self-isso] — A commenting server similar to Disqus
([source][source-isso])
- [Miniflux][self-miniflux] — A minimalist and opinionated feed reader
([source][source-miniflux])


[syncs]: https://github.com/musq/syncs
[vim-autobackup]: https://github.com/musq/vim-autobackup
[dotfiles-system]: https://github.com/musq/dotfiles-system
[dotfiles]: https://github.com/musq/dotfiles
[github-available-usernames]: https://github.com/musq/github-available-usernames
[iitd-proxy-hack]: https://github.com/musq/iitd-proxy-hack

[self-cyberchef]: cyberchef
[self-isso]: isso/admin
[self-miniflux]: https://read.{{ site.url }}

[source-cyberchef]: https://github.com/gchq/cyberchef
[source-isso]: https://github.com/posativ/isso
[source-miniflux]: https://github.com/miniflux/miniflux
