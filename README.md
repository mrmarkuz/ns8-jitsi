# ns8-jitsi

[Jitsi](https://jitsi.org/) is an open source video conferencing webapp.

## Install

Install via Software center:

  - Add a Software repository pointing to `https://repo.mrmarkuz.com/ns8/updates/`, see https://repo.mrmarkuz.com for instructions
  - Install Jitsi via Software Center

Instantiate the module with:

    add-module ghcr.io/nethserver/jitsi:1.0.0 1

## Configure

Configure at least an FQDN.
Optionally you can set a user domain for authentication. If unset internal authentication is used.
Browse to `https://<FQDN>`

## Firewall

Jitsi needs port 9999/UDP.
If there's a firewall in front of Jitsi, it's required to open that port on the firewall and forward it to the NS8 node that hosts Jitsi.

## Create internal user

Following command can be used to create an internal user:

    runagent -m jitsi1 podman exec jitsi-prosody prosodyctl --config /config/prosody.cfg.lua register <USERNAME> meet.jitsi <PASSWORD>

For more information about internal auth, see [Jitsi Docker installation documentation](https://jitsi.github.io/handbook/docs/devops-guide/devops-guide-docker/#internal-authentication)

## Customization

To customize Jitsi, custom files need to be created out of the default config: (in this example the Jitsi app instance is jitsi1)
    
    runagent -m jitsi1 podman exec -ti jitsi-web bash -c "cp config.js custom-config.js && cp interface_config.js custom-interface_config.js && exit"

The custom files config is appended to the default configuration files. It's also possible to just append what you like to change instead of copying the original files.

Now it should be possible to change the configuration by editing these files: (in these examples nano is used as editor)

custom-config.js:

    runagent -m jitsi1 podman unshare nano /home/jitsi1/.local/share/containers/storage/volumes/jitsi-web-config/_data/custom-config.js

custom-interface_config.js:

    runagent -m jitsi1 podman unshare nano /home/jitsi1/.local/share/containers/storage/volumes/jitsi-web-config/_data/custom-interface_config.js

See [Jitsi docs](https://jitsi.github.io/handbook/docs/devops-guide/devops-guide-docker/#jitsi-meet-configuration) for more information.

## Uninstall

To uninstall the instance:

    remove-module --no-preserve jitsi1

