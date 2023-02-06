Ansible Role: vim_plugins
=========

Ansible role to install vim plugins with Pathogen or Vim native plugins loading system

Requirements
--------------
git

Role Variables
--------------

Available variables are the following:

```yaml
vim_plugins_use_native_packages: false
```

Whether to use the native Vim plugins loading system available since Vim 8.0 or not.
Default value is `false`, and "pathogen" is used instead, to maximize portability.

```yaml
vim_plugins_repositories: []
```

List of dictionaries representing plugins repositories. The `url` key is mandatory,
and represents the url of a repository. The others are optional, with the default
vaules reported below:

```Yaml
vim_plugins_repositories:
  - url: https://github.com/neoclide/coc.nvim # Repository URL (mandatory)
    branch: master    # The repository branch
    category: plugins # Name of the directory created under ~/.vim/pack if using Vim native plugin loading system
    autostart: true   # Used to specify if the plugin should be autostarted when using the Vim native plugin loading system
```

```yaml
vim_plugins_pathogen_url: https://tpo.pe/pathogen.vim
```

The URL of the pathogen plugin repository

```yaml
vim_plugins_user_home: '~'
```

Path to the user home directory

```yaml
vim_plugins_directory: .vim/bundle
```

The path, __relative__  to the specified user home directory, where plugins should be installed __when using pathogen__
(when using the native Vim plugins loading system, this is irrelevant: plugins are always installed under `.vim/pack`).


Dependencies
------------
None

Example Playbook
----------------

Call role to install a plugin from the default branch using pathogen:

```yaml

- hosts: servers
  roles:
    - role: egdoc.vim_plugins
      vim_plugins_repositories:
        - url: https://github.com/preservim/nerdcommenter
```

Call role to install a specific plugin branch using Vim native plugin loading system. Load the plugin on request:

```yaml
- hosts: servers
  roles:
    - role: egdoc.vim_plugins
      vim_use_native_packages: true
      vim_plugins_repositories:
        - url: https://github.com/neoclide/coc.nvim
          branch: release
          autostart: false
```

Notice that if you deploy your .vim directory as a link (from a dotfiles repository, for example),
you must do it __before__ calling this role, which creates it if it doesn't exist.

License
-------

GPLv2

Author Information
------------------

Created by Egidio Docile
