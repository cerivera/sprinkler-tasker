## Pre-requisites

Add a `config.py` with the following variables:

```
dark_sky_key = "<DARK SKY API KEY>"
dark_sky_root = "https://api.darksky.net"
```

## Build 

```
$ (host) docker build -t forecast:latest .
```

## Run

### With Defaults
```
$ (host) docker run --rm forecast:latest
Cold days: [Tuesday,Sunday]
Rainy days: [Friday,Saturday]
```

### With Customizations

```
$ (host) docker run --rm forecast:latest python ./main.py --help

Usage: main.py [OPTIONS]

  Get the week's forecast.

Options:
  --lat FLOAT              Latitude
  --lon FLOAT              Longitude
  -rp, --rain_prob FLOAT   Rain probability threshold used to identify rainy
                           days.
  -mt, --max_temp INTEGER  Max temperature threshold used to identify cold
                           days.
  --help                   Show this message and exit.
```

## Managing dependencies

Dependencies should be installed within the docker container to avoid creating a local virtual env.

After building the docker image, you can run it with a volume to make sure any changes in the container show up in the host.

```
$ (host)      docker run -it --rm -v $(pwd):/opt/app forecast:latest
$ (container) pip3 install click
$ (container) pip3 freeze > requirements.txt
$ (container) exit
$ (host)      git add requirements.txt
```