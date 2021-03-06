# Read this first!

## Validation

Before running the template with ```up -d``` I recommend you to always check the template first with ```config```.

```shell
docker-compose -f docker-compose.yml -f docker-compose.traefik.yml -f docker-compose.ports.yml config
```

That way you can make sure no environment variables are missing and the labels for Traefik are correct.

## Setup

You need to either specify a bind mount to your games folder or use an [NFS](../README#nfs) share

### Mount games folder locally

If your games are on the same host as your container, you can use a bind mound to a local folder on your host.

```shell
# open .env
editor .env
# and add your games path
PS3NETSRV_VOLUME=$HOME/games
```

### Mount games folder from NFS

See main [README#NFS](../README#nfs)

## Run

To run this container just execute

```shell
docker-compose -f docker-compose.yml -f docker-compose.ports.yml up -d
```

### Troubleshooting

#### I want to switch from bind mount to NFS, but can't reinitialize the games_data volume

Simply purge the container with ```docker-compose down -v``` and then fire it up again with the proper configuration ([see NFS](#nfs)).

#### Port 38008 is already taken

Fret not, you don't need to adjust my compose files, you can just create an ```.env``` file and adjust the ports through that, for example

```shell
# open .env
editor .env
# and add
PS3NETSRV_PORT=38009
```

Now the ps3netsrv is served under port 38009.

#### It's still not working

Consult [the issue tracker](https://github.com/aldostools/webMAN-MOD/issues) first and create a ticket.

If you **made sure** the issue is related to my compose files, create an issue.
