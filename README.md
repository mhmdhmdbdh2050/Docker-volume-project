# Docker Volume Persistence Lab

A small, repeatable demonstration that a Docker named volume outlives the container that writes to it. This is a learning lab, not a backup strategy: a named volume alone does not protect data from host or disk loss.

## Prerequisites

- Docker Engine
- A shell with Docker CLI access

## Run the persistence demonstration

Create a named volume and write a file from a temporary container:

```bash
docker volume create my-volume
docker run --rm -v my-volume:/data alpine:3 sh -c 'printf "volume data survives container removal\\n" > /data/message.txt'
```

Read the same file from a different temporary container:

```bash
docker run --rm -v my-volume:/data alpine:3 cat /data/message.txt
```

Expected output:

```text
volume data survives container removal
```

The first container was removed by `--rm`; the file remains because it was written to the named volume.

## Inspect and clean up

```bash
docker volume inspect my-volume
docker volume rm my-volume
```

Removing the volume permanently deletes the demonstrated data. Do not remove a volume containing data you need.

## What this demonstrates

- A named volume has a lifecycle separate from an individual container.
- Multiple containers can mount the same volume.
- Removing a container does not remove the named volume.

For a real service, also document backup, restore, ownership, and recovery procedures; persistence by itself is not backup or high availability.
