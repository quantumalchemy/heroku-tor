# Tor Hidden Service Buildpack for Heroku
# UPDATED Tor v 0.4.6.7


This buildpack sets up a Tor hidden service for your app on Heroku.
## Tor Version 3 urls

## Setup

Create a Heroku app as normal, with any buildpacks you typically use.

Then:

```bash
$ heroku buildpacks:add https://github.com/quantumalchemy/heroku-tor.git
```

With the buildpack installed, you'll need to modify your Procfile such that
the hidden service will be setup when the app runs.

```Procfile
web: ./tor/bin/run_tor <cmd you'd normally run>
```

While `web` works just fine, so too will any other process type. Use `web`
if you want the app to be accessible generally, as well as over Tor. Use
`<any other type>` (e.g. `foo`), to avoid Heroku's router routing to your app like so:

```Procfile
foo: PORT=9999 ./tor/bin/run_tor <cmd you'd normally run>
```

Your app will only be accessible over Tor, through your configured
`.onion` address.

## Maintain your own v3 url 
## Setup:

Tor hidden services Once your require that you provide a hs_ed25519_secret_key 
v3 for the .onion name.

1. Create the directory -> 'hidden_service'  in the root of your build repo.
2. Copy ONLY the: hs_ed25519_secret_key file from '/app/hidden_service' the running dyno on first deployment to ->
'hidden_service' that you just created in your git build repo

3. You'll need to provide these as env vars:

* `HIDDEN_DOT_ONION`:  from the hostname file under the running dyno 'hidden_service'
4. After commited changes - re deploy .. and Enjoy!

## Features

* Verifies tor integrity
* Caches compilation
* Updated to work for Tor persistent v3 urls!
