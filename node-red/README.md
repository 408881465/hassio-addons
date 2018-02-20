# Node-RED Hass.io Add-On
---------

[Hass.io](https://home-assistant.io/hassio/) add-on for [Node-RED](https://nodered.org/).

## Installation

1. Add my [Hass.io](https://home-assistant.io/hassio/) add-on [repository](https://github.com/notoriousbdg/hassio-addons)
2. Install the "Node-RED" add-on
3. (Optional) To enable SSL support, set SSL to true
    ```json
    {
      "ssl": true,
      "certfile": "fullchain.pem",
      "keyfile": "privkey.pem",
      "users": [
        {
          "username": "admin",
          "password": "password",
          "permissions": "*"
        }
      ],
      "http_node_user": [
        {
          "username": "admin",
          "password": "password"
        }
      ],
      "projects": false
    }
    ```
4. (Optional) Disable IDE authentication by removing all users from users array
    ```json
    {
      "ssl": true,
      "certfile": "fullchain.pem",
      "keyfile": "privkey.pem",
      "users": [
      ],
      "projects": false
    }
    ```
5. (Optional) Disable HTTP Node (Dashboard UI) authentication by removing the user from http_node_user
    ```json
    {
      "ssl": true,
      "certfile": "fullchain.pem",
      "keyfile": "privkey.pem",
      "http_node_user": [
      ],
      "projects": false
    }
    ```
6. (Optional) Add additional IDE users to users array.  Use permission of `read` to grant read-only permissions to additional users.
    ```json
    {
      "ssl": true,
      "certfile": "fullchain.pem",
      "keyfile": "privkey.pem",
      "users": [
        {
          "username": "admin",
          "password": "password",
          "permissions": "*"
        },
        {
          "username": "user2",
          "password": "password2",
          "permissions": "read"
        }
      ],
      "projects": false
    }
    ```
7. (Optional) Enable projects feature in v0.18.x by setting `projects` to `true`. Refer to [Node-RED Projects](https://nodered.org/docs/user-guide/projects/) for additional info about setting up projects.
    ```json
    {
      "ssl": true,
      "certfile": "fullchain.pem",
      "keyfile": "privkey.pem",
      "users": [
        {
          "username": "admin",
          "password": "password",
          "permissions": "*"
        }
      ],
      "http_node_user": [
        {
          "username": "admin",
          "password": "password"
        }
      ],
      "projects": true
    }
    ```
8. Start the "Node-RED" add-on
9. (Optional) Configure [panel_iframe](https://home-assistant.io/components/panel_iframe/) component to embed Node-RED UI into Home Assistant UI using this example:

    ```yaml
    panel_iframe:
      nodered_flows:
        title: 'Node-RED Flows'
        url: 'http://hassio.local:1880'
        icon: mdi:nodejs
    ```

10. (Optional) If you install [Node-RED Dashboard](https://github.com/node-red/node-red-dashboard) in Node-RED, you can expose the dashboard in the [Hass.io](https://home-assistant.io/hassio/) UI using this example to your [panel_iframe](https://home-assistant.io/components/panel_iframe/) section:

    ```yaml
    panel_iframe:
      nodered_ui:
        title: 'Node-RED Dashboard'
        url: 'http://hassio.local:1880/ui'
        icon: mdi:nodejs
    ```

11. (Optional) Install [node-red-contrib-home-assistant](https://flows.nodered.org/node/node-red-contrib-home-assistant) from Manage Palette window. After install place some HA node to flow and setup HA server for it. As you are running Node-RED inside Hass.io addon/container you can use Hass.io API Proxy address `http://hassio/homeassistant` as Home Assistant server address (server node Base URL). This way you don't need any real network address.

## Support

Please use [this thread](https://community.home-assistant.io/t/repository-notoriousbdg-add-ons-node-red-and-ha-bridge/23247) for feedback.

## FAQ

### Q: How do I update to the latest version of Node-RED ASAP?
A: Since this addon is derived from the official Node-RED docker image, you may need to manually force hassio to rebuild the image to get the latest Node-RED version. To force a rebuild of the image to upgrade Node-RED, navigate to http://hassio.local:8123/hassio/addon/27e642c6_nodered then click on "Rebuild".

### Q: How do I update builtin nodes when updating via "Manage palette" fails?
A: The builtin nodes can be updated by manually force hassio to rebuild the image to get the latest Node-RED version. To force a rebuild of the image to upgrade Node-RED, navigate to http://hassio.local:8123/hassio/addon/27e642c6_nodered then click on "Rebuild".


## Changelog

### 0.1.0 (2017-07-31)
#### Initial Release

### 0.1.1 (2017-08-10)
#### Added
- Option to enable SSL

### 0.1.2 (2017-09-15)
#### Changed
- Changed to use host network to allow Node-RED to listen on arbitrary ports

### 0.1.3 (2017-10-10)
#### Added
- Updated to support new hass.io build system

### 0.1.4 (2017-10-24)
#### Changed
- Updated webui links in config.json to support ssl when enabled in the addons

### 0.1.5 (2017-11-25)
#### Changed
- Moved data dir to /share/node-red
#### Added
- Added authentication for editor and admin API

### 0.1.6 (2017-12-13)
#### Changed
- node-red-admin no longer re-installs on every restart of the addon
#### Added
- Added authentication for HTTP nodes (Dashboard UI)

### 0.1.7 (2018-02-15)
#### Changed
- Bumping version to assist with upgrading to Node-RED v0.18.3

### 0.1.8 (2018-02-16)
#### Added
- Added support for [Node-RED Projects](https://nodered.org/docs/user-guide/projects/) in Node-RED v0.18.x

### 0.1.9 (2018-02-20)
#### Changed
- Upgrade node during build to address compatibility issue with node-red-contrib-home-assistant 0.3.0

### 0.1.10 (2018-02-20)
#### Added
- Added auto_uart permission which allows Node-RED nodes to access serial devices such as node-red-contrib-rfxcom.
