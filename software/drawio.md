# Run draw.io offline
## Docker
Code is [here](https://github.com/jgraph/docker-drawio).

Start draw.io container:
```
docker run -it --rm --name="draw" -p 8080:8080 -p 8443:8443 jgraph/drawio
```

Then browse to http://localhost:8080/?offline=1&https=0.

## Electron
Download the Electron app [here](https://github.com/jgraph/drawio-desktop).
