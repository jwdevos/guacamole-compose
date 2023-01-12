# guacamole-compose
#### Docker Compose Project For Apache Guacamole

### How To Use
- Clone this repo to a Docker Compose enabled host. For testing, Ubuntu 22.04.1 was used, with Docker installed as described [here](https://docs.docker.com/engine/install/ubuntu/)
- Make sure you're in the guacamole directory, and no interfering containers or volumes are present (verify by running `make status`)
- Run `make bootstrap`
- Run `make up`
- Connect to Guacamole on the IP of the Docker host: `http://X.X.X.X:8080/guacamole`
- If you need a clean environment because something got screwed, run `make prune`. **Be careful:** this will remove all data that might have been added to your Guamole environment
- To bring down the environment without destroying data, run `make down`
- View the status by running `make status`
- Minimal security steps for production use:
  - Change the passwords in the `.env` file
  - Don't connect the containers directly to the internet, use a reverse proxy, TLS, and valid certificates. [This](https://www.conproly.com/blogs/20180920-running-haproxy-and-lets-encrypt-on-docker/) is one way to do it, although outdated and without compose. A lot of firewalls also have built in reverse proxies and support for Let's Encrypt
  - Uncomment the ENABLE_TOTP setting in the compose file to make Guacamole ask for 2FA registration 
