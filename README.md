Plugin MGNT
============

Bash script to enable and disable Bukkit plugins including version managment and autocomplete support.

## Installation

#### Bash script

    git clone git://github.com/yeahwhat-mc/Plugin-MGNT.git /usr/src/Plugin-MGNT
    ln -s /usr/src/Plugin-MGNT/plugin-* /usr/local/bin/

#### Autocompletion

    ln -s /usr/src/Plugin-MGNT/bash_completion.d/plugin-mgnt /etc/bash_completion.d/plugin-mgnt

## Assumptions

* Minecraft servers in `/opt/minecraft/`, in the examples below: `/opt/minecraft/mc-main`
* Plugin resource folder, to store all .jar's in `/opt/minecraft/.mc-resources/plugins`
* Plugin .jar's have to be named after the name scheme __\<Name>\_\<Version>b\<Build>__  (`DisguiseCraft_1.7.8b55`)
* Plugins are linked from `DisguiseCraft_1.7.8b55.jar` to `DisguiseCraft_latest.jar` in the resource folder
* "Latest" plugins are linked again from resource folder into the productional plugin folder of each Minecraft server: `/opt/minecraft/.mc-resources/plugins/DisguiseCraft_latest.jar` -> `/opt/minecraft/mc-main/plugins/DisguiseCraft_latest.jar`

## Usage

##### List plugins

`$ plugin-list resources`

    ChestShop_3.7.8.jar
    ChestShop_latest.jar -> /opt/minecraft/.mc-resources/plugins/ChestShop_3.7.8.jar
    CraftConomy_3.1.6.jar
    CraftConomy_latest.jar -> /opt/minecraft/.mc-resources/plugins/CraftConomy_3.1.6.jar
    DisguiseCraft_1.7.8b55.jar
    DisguiseCraft_latest.jar -> /opt/minecraft/.mc-resources/plugins/DisguiseCraft_1.7.8b55.jar
    Vault_1.4.1.jar
    Vault_latest.jar -> /opt/minecraft/.mc-resources/plugins/Vault_1.4.1.jar

`$ plugin-list server`

    ChestShop_latest.jar -> /opt/minecraft/.mc-resources/plugins/ChestShop_3.7.8.jar
    CraftConomy_latest.jar -> /opt/minecraft/.mc-resources/plugins/CraftConomy_3.1.6.jar
    Vault_latest.jar -> /opt/minecraft/.mc-resources/plugins/Vault_1.4.1.jar

Shows all plugins and symlinks in your resource and server folder.

##### Bump active plugin version

`$ plugin-version-bump DisguiseCraft_1.7.8b55.jar`

This will update the symlink from `/opt/minecraft/.mc-resources/plugins/DisguiseCraft_1.7.8b55.jar` to `/opt/minecraft/.mc-resources/plugins/DisguiseCraft_latest.jar` which again is linked into the plugin folder of your Minecraft servers.

##### Enable a plugin

`$ plugin-up DisguiseCraft_latest.jar`

First it compares MD5 checksums of the plugin in the ressource folder and the productive plugin in the Bukkit folder, if they are not the same it will symlink the "latest" version of ChestShop from `/opt/minecraft/.mc-resources/plugins/DisguiseCraft_latest.jar` to `/opt/minecraft/mc-main/plugins/DisguiseCraft_latest.jar`.

##### Disable a plugin

`$ plugin-down DisguiseCraft_latest.jar`

Unlinks / disables the productive plugin in the Bukkit plugin folder (`/opt/minecraft/mc-main/plugins/DisguiseCraft_latest.jar`).

##### Download a plugin

`$ plugin-wget http://build.yu8.me:8080/job/DisguiseCraft/55/artifact/target/DisguiseCraft.jar^`

Download a plugin via HTTP or HTTPS directly into your resource folder.

## Todo

- [ ] Screenshot or demo
- [ ] Configuration file
- [ ] `plugin-info` to get status of plugin, versions and modification dates
- [ ] Move all sub commands into one binary
- [X] Plugin downloader (`plugin-wget`)

