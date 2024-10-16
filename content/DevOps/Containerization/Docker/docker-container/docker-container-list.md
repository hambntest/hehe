
## Description
List containers

# CLI

# docker container ls

| Aliases                           |
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
