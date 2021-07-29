# Description

This role configures [`matterbridge`](https://github.com/42wim/matterbridge) chat bridging software.

# Details

The software runs as a docker container from [`42wim/matterbridge`](https://hub.docker.com/r/42wim/matterbridge/).

The configuration file template is in [`templates/matterbridge.yaml.j2`](./templates/matterbridge.yaml.j2).

# Configuration

```yaml
matterbridge_bridges:
  status:
    bridge:
      Nick: 'bridge.stateofus.eth'
      PrivateKey: '0x04abcXYZ'
      RemoteNickFormat: '**{NICK}**@*{PROTOCOL}*: '

  discord:
    status-pub:
      Token: 'super-secret-token'
      Server: 'Status Community'
      RemoteNickFormat: '{NICK}@{PROTOCOL}'

matterbridge_gateways:
  - { status: "tech",   discord: [{ srv: "status-pub", ch: "tech" }] }
  - { status: "music",  discord: [{ srv: "status-pub", ch: "music" }] }
  - { status: "movies", discord: [{ srv: "status-pub", ch: "movies" }] }
```

# API

To use the Matterbridge API it must be enabled with `matterbridge_api_enabled: true`.
Currently only a single API (called `api`) is supported.

It can be used in a gateway like this:

```
- { discord: [{ srv: "vac", ch: "waku" }], api: ["api"]}
```

The API is running on port 4242 by default (`matterbridge_api_port`). More info
about the API can be found on the [Matterbridge wiki](https://github.com/42wim/matterbridge/wiki/Api).

# Known Issues

If your bridge is posting in a Discord channel but doesn't receive mesages from it you might have to adjust the channel-level permissions to give the bot message read rights.

# Links

* https://github.com/42wim/matterbridge/blob/master/matterbridge.toml.sample
* https://github.com/42wim/matterbridge/wiki/How-to-create-your-config
* https://github.com/42wim/matterbridge/wiki/Settings
* https://notes.status.im/s/slack-bridge-bot-setup
