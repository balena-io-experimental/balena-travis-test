# resin-travis-test ![It builds!](https://travis-ci.org/resin-io-projects/resin-travis-test.svg?branch=master)

Continuous Integration on your devices:

Deploy to [resin.io](https://resin.io) from Github using [Travis CI](https://travis-ci.org).

## Description

This repo is a simple example on how to use Travis CI to push code to your devices on resin.io.
The [travis.yml](./.travis.yml) file specifies the script that "builds" the project - in this case, the build consists in adding the Resin git remote and pushing to it. This will trigger the build in Resin's servers and deploy the code to your devices.

The script could, of course, be modified to include tests, other builds or whatever you need for your own project. Pushing different branches to different apps (if you have a staging app, for instance), could easily achieved by adding git push commands to different remotes.

## Configuration

The travis.yml file uses just two environment variables: `RESIN_REMOTE` and `RESIN_DEPLOY_KEY`. This can be set in the Travis Settings page for the repo.

`RESIN_REMOTE` is just the ssh address of the Resin git remote, e.g. `gh_pcarranzav@git.resinstaging.io:gh_pcarranzav/supertestrpi.git`.

`RESIN_DEPLOY_KEY` should be a *private* SSH key so that Travis can push to Resin. You can generate the key like this:
```bash
ssh-keygen # Will prompt for a file name, input one like 'id_rsa'
echo -n "\""; cat id_rsa | awk 1 ORS='\\n'; echo "\""
```
This last command will print the SSH key in a format that can be inputted in the Travis Settings GUI, that is, between quotes and with newlines replaced by "\n" (a slash followed by an n, not the newline character).

The *public* key can then be added on the [Resin dashboard](https://dashboard.resin.io/preferences?tab=sshkeys).

This could alternatively be done by using Travis' [file encryption feature](http://docs.travis-ci.com/user/encrypting-files/).
