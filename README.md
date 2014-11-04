mitro-heroku-buildpack
======================
A heroku buildpack for the Mitro password manager.

> **Note:** This is a work in progress

## Deploy to Heroku
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/shanewho/mitro/tree/heroku-button)

> This button currently uses a my experimental fork, not the official Mitro repo

## Do it manually

```
git clone https://github.com/mitro-co/mitro.git
heroku create
heroku addons add heroku-postgresql:hobby-dev
heroku config:set RANDOM_KEY=$(openssl rand -base64 256)
heroku config:set BUILDPACK_URL=https://github.com/shanewho/mitro-heroku-buildpack.git
```

## For the paranoid

- I am not a security professional, I do not know all the security risks involved in this setup
- This uses Heroku's free SSL (https://yourapp.heroku.com). You will have a secure connection between your browser and Heroku's servers. The link between Heroku's server (their HTTP router) and the Mitro server is not secure unless you setup *real* SSL with your own certs (i.e., costs money).
- The key used for signing things is based on the RANDOM_KEY value set on your app's config (it is an SHA-1 hash of that key). Make sure RANDOM_KEY is set to something random and unique. Make sure nobody gets access to this value.


## For the extra paranoid

- The buildpack downloads Ant from archive.apache.org and Java from Amazon S3 (the same binaries as Heroku's official Java buildpack)
- The buildpack includes a pre-built *unzip* not included in Heroku's base image
