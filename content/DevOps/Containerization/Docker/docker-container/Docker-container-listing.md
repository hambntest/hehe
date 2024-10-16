# CLI

| Commands                          |
| --------------------------------- |
| `docker ps [OPTIONS]`             |
| `docker container ls [OPTIONS]`   |
| `docker container list [OPTIONS]` |
| `docker container ps [OPTIONS]`   |

| Option         | Default | Description                                             |
| -------------- | ------- | ------------------------------------------------------- |
| `-a, --all`    |         | Show all containers (default shows just running)        |
| `-f, --filter` |         | Filter output based on conditions provided              |
| `--format`     |         | Format output using a custom template                   |
| `-n, --last`   |         | Show n last created containers (includes all states)    |
| `-l, --latest` | `-1`    | Show the latest created container (includes all states) |
| `--no-trunc`   |         | Don't truncate output                                   |
| `-q, --quiet`  |         | Only display container IDs                              |
| `-s, --size`   |         | Display total file sizes                                |
## Show running docker containers 
- for seeing containers (running):
``` bash
docker ps
```
## Show both running and stopped containers (-a, --all)
- The `docker ps` command only shows running containers by default. To see all containers, use the `--all` (or `-a`) flag:
``` bash
docker ps -a
```
## Filtering (--filter)
The `--filter` (or `-f`) flag format is a `key=value` pair. If there is more than one filter, then pass multiple flags (e.g. `--filter "foo=bar" --filter "bif=baz"`).

The currently supported filters are:

| Filter              | Description                                                                                                                         |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `id`                | Container's ID                                                                                                                      |
| `name`              | Container's name                                                                                                                    |
| `label`             | An arbitrary string representing either a key or a key-value pair. Expressed as `<key>` or `<key>=<value>`                          |
| `exited`            | An integer representing the container's exit code. Only useful with `--all`.                                                        |
| `status`            | One of `created`, `restarting`, `running`, `removing`, `paused`, `exited`, or `dead`                                                |
| `ancestor`          | Filters containers which share a given image as an ancestor. Expressed as `<image-name>[:<tag>]`, `<image id>`, or `<image@digest>` |
| `before or since`   | Filters containers created before or after a given container ID or name                                                             |
| `volume`            | Filters running containers which have mounted a given volume or bind mount.                                                         |
| `network`           | Filters running containers connected to a given network.                                                                            |
| `publish or expose` | Filters containers which publish or expose a given port. Expressed as `<port>[/<proto>]` or `<startport-endport>/[<proto>]`         |
| `health`            | Filters containers based on their healthcheck status. One of `starting`, `healthy`, `unhealthy`, or `none`.                         |
| `isolation`         | Windows daemon only. One of `default`, `process`, or `hyperv`.                                                                      |
| `is-task`           | Filters containers that are a "task" for a service. Boolean option (`true` or `false`).                                             |

 for seeing containers that are running:
``` bash
docker ps --filter "status=running"
```

| Status      | Description                                                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `created`   | A container that has never been started.                                                                                                                            |
| `running`   | A running container, started by either `docker start` or `docker run`.                                                                                              |
| `paused`    | A paused container. See `docker pause`.                                                                                                                             |
| `restarting`| A container which is starting due to the designated restart policy for that container.                                                                              |
| `exited`    | A container which is no longer running. For example, the process inside the container completed or the container was stopped using the `docker stop` command.        |
| `removing`  | A container which is in the process of being removed. See `docker rm`.                                                                                              |
| `dead`      | A "defunct" container; for example, a container that was only partially removed because resources were kept busy by an external process. Dead containers cannot be (re)started, only removed. |

## Format the output (--format)
- you can use --filter with this kind of formats too like in this example the command is going to list container ID and name and the uptime 
``` bash
docker ps --format "table {{.ID}}\t{{.Names}}\t{{.Status}}"
```


- for prettier name and image and port detailed one:
``` bash
container_ids=$(sudo docker ps -q)
for id in $container_ids; do
    echo "NAME: $(sudo docker ps --filter "id=$id" --format "{{.Names}}")    IMAGE: $(sudo docker ps --filter "id=$id" --format "{{.Image}}")"
    echo "PORTS: $(sudo docker ps --filter "id=$id" --format "{{.Ports}}")"
    echo ""
done
```
- for prettier fully detailed one:
``` bash
container_ids=$(sudo docker ps -q)
for id in $container_ids; do
    echo "CONTAINER ID: $(sudo docker ps --filter "id=$id" --format "{{.ID}}")"
    echo "NAME: $(sudo docker ps --filter "id=$id" --format "{{.Names}}")"
    echo "IMAGE: $(sudo docker ps --filter "id=$id" --format "{{.Image}}")"
    echo "COMMAND: $(sudo docker ps --filter "id=$id" --format "{{.Command}}")"
    echo "CREATED AT: $(sudo docker ps --filter "id=$id" --format "{{.CreatedAt}}")"
    echo "RUNNING FOR: $(sudo docker ps --filter "id=$id" --format "{{.RunningFor}}")"
    echo "PORTS: $(sudo docker ps --filter "id=$id" --format "{{.Ports}}")"
    echo "STATUS: $(sudo docker ps --filter "id=$id" --format "{{.Status}}")"
    echo "SIZE: $(sudo docker ps --filter "id=$id" --format "{{.Size}}")"
    echo "LABELS: $(sudo docker ps --filter "id=$id" --format "{{.Labels}}")"
    echo "MOUNTS: $(sudo docker ps --filter "id=$id" --format "{{.Mounts}}")"
    echo ""
done
```
> this one gives CONTAINER ID, NAME, IMAGE, COMMAND, CREATED AT, RUNNING FOR, PORTS, STATUS, SIZE, LABELS and MOUNTS (this is basically everything that you can get from docker ps)
## list last created docker containers
- Show n last created containers (includes all states) (default -1) (in this scenario show last 2)
``` bash
docker ps --last 2
```
## list latest created docker container 
- Show the latest created container (includes all states)
``` bash
docker ps --latest
```
## list docker containers without truncate
- show the list without truncating the output
``` bash
docker ps --no-trunc
```
## list docker containers ID only
- show the list with only container IDs
``` bash
docker ps -q
```
## Show disk usage by container (--size)
- The `docker ps --size` (or `-s`) command displays two different on-disk-sizes for each container:
``` bash
docker ps -s
```
- The "size" information shows the amount of data (on disk) that is used for the _writable_ layer of each container
- The "virtual size" is the total amount of disk-space used for the read-only _image_ data used by the container and the writable layer.
