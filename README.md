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

## Create internal user

Following command can be used to create an internal user:

    runagent -m jitsi1 podman exec jitsi-prosody prosodyctl --config /config/prosody.cfg.lua register <USERNAME> meet.jitsi <PASSWORD>

For more information about internal auth, see [Jitsi Docker installation documentation](https://jitsi.github.io/handbook/docs/devops-guide/devops-guide-docker/#internal-authentication)

## Uninstall

To uninstall the instance:

    remove-module --no-preserve jitsi1

