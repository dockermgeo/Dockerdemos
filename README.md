# Docker DEMOS

## PWD Session erzeugen
```
open http://play-with-docker.com
```

## Dateien kopieren
```
git clone https://github.com/git-mgeo/dockerdemos.git
cd dockerdemos
```


## Dockerdemos
* Builderdemo: Einfacher Container, der nach 10 Sekunden stirbt. ENV-Variable '${TEAM_NAME}'
* Fotoshow: Von der Dockercon ENV-Variable '${HTML_TITLE}' (**! kein Build notwendig**)


## Build (falls noetig)

```
cd Builderdemo
make build
```

## Docker-Hybrid
```
make run
```

## SWARM
```
make service_create
```
or
```
make deploy
```

