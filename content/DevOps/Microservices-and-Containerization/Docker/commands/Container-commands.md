
# Container controls

# Container listing commands
### listing running docker containers 
for seeing containers (running):
``` bash
docker ps
```
or:
``` bash
docker container ls
```
### listing all docker containers
>instead of -a, --all can be used

for seeing all containers (running or stopped):
``` bash
docker ps -a
```
or:
``` bash
docker container ls -a
```
### listing all docker containers with filter
>instead of --filter, --format or -f can be used

for seeing containers that are running:
``` bash
docker ps --filter "status=running"
```
for seeing all containers that are stopped:
``` bash
docker ps --filter "status=exited"
```
you can use --filter with this kind of formats too like in this example the command is going to list container ID and name and the uptime 
``` bash
docker ps --format "table {{.ID}}\t{{.Names}}\t{{.Status}}"
```
for prettier name and image and port detailed one:
``` bash
container_ids=$(sudo docker ps -q)
for id in $container_ids; do
    echo "NAME: $(sudo docker ps --filter "id=$id" --format "{{.Names}}")    IMAGE: $(sudo docker ps --filter "id=$id" --format "{{.Image}}")"
    echo "PORTS: $(sudo docker ps --filter "id=$id" --format "{{.Ports}}")"
    echo ""
done
```
for prettier fully detailed one:
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
### list last created docker containers
>instead of --last, -n can be used

Show n last created containers (includes all states) (default -1) (in this scenario show last 2)
``` bash
docker ps --last 2
```
### list latest created docker container 
>instead of --latest, -l can be used

Show the latest created container (includes all states)
``` bash
docker ps --latest
```
### list docker containers without truncate
show the list without truncating the output
``` bash
docker ps --no-trunc
```
### list docker containers ID only
>instead of -q, --quiet can be used

show the list with only container IDs
``` bash
docker ps -q
```
### listing all docker containers with their size
>instead of -s, --size can be used

show the list with total file sizes
``` bash
docker ps -s
```


# Container managing
# Container logs

