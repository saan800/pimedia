# Plex Media Server

## Prep

* In OMV go to `Access Rights Management` > `Shared Folders`
  * Ensure you have the `containers` and `media` folders setup from when you [Installed Open Media Vault](05_install_open_media_vault.md)
  * Take note of `Absolute Path` for shared folders
* From either laptop or Pi command line add the following folders:
  * `containers`
    * `plex` > `config`
    * `plex` > `transcodes`
  * `media`
    * `movies`
    * `tv`
* SSH into pi
  * run `id [USERNAME]`
  * take note of the `uid` and `gid` values


## Install docker image

* Open [Plex docker imgae](https://hub.docker.com/r/linuxserver/plex) details
  * Check that version supports `arm64`
* Login to [Portainer](http://pimedia:9000/)
  * NOTE: Use `docker-compose` config from docker image details at https://hub.docker.com/r/linuxserver/plex
  * Go to Containers and `Add Container`
    * Name: `plex`
    * Registry: `DockerHub`
    * Imgae: `linuxserver/plex-latest`
    * Volumes tab:
      * Map 4 additional volumes and `Bind` all of them
        * container: `/config/`, host: `/srv/[CONTAINER FOLDER PATH]/containers/plex/config/`
        * container: `/transcodes/`, host: `/srv/[CONTAINER FOLDER PATH]/containers/plex/transcodes/`
        * container: `/movies/`, host: `/srv/[MEDIA FOLDER PATH]/movies/`
        * container: `/tv/`, host: `/srv/[MEDIA FOLDER PATH]/tv/`
    * Network tab:
      * Netowk: `host`
    * Env tab:
      * Add 3 environment variables
        * PUID: [From SSH run `id [USERNAME]`]
        * PGID: [From SSH run `id [USERNAME]`]
        * VERSION: docker
    * Restart Policy tab:
      * 



## More details

* [How to install Plex Media Server on OpenMediaVault 5 using Docker with Portainer on Raspberry Pi 4](https://www.youtube.com/watch?v=bEZeroOZVIs&list=PLulABMF2ltKoQFbhWSZpvhQx9KXXMibKa&index=26)