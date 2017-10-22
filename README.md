# Docker DEMOS

## PWD Session erzeugen
```
open http://play-with-docker.com
```

## Dateien kopieren
```
git clone https://github.com/git-mgeo/dockerdemos.git
```


## Demos
* Builderdemo - einfacher Container, der nach 10 Sekunden stirbt. ENV-Variable 'TEAM_NAME'
* Fotos von der Dockercon ENV-Variable 'TEAM_NAME' (kein Build notwendig)


### Build

```
cd Builderdemo
make build
```

### Docker-Hybrid
```
make run
```

### SWARM
```
make service_create
```
or
```
make deploy
```

