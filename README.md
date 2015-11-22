# docker-snippets-powershell
The idea is to put together the most useful snippets when you are using docker on a Windows environment and you are using Powershell as your CLI

## Stop containers

```foreach ($id in docker ps -a -q -f status=running) {docker stop $id}```

## Delete stopped containers

```foreach ($id in docker ps -a -q -f status=exited) {docker rm $id}```

## Delete untagged images

```foreach ($id in docker images -a | Select-String -Pattern "<none>" | foreach-object {  $_.ToString().Split("{ }",[System.StringSplitOptions]::RemoveEmptyEntries)[2] }){docker rmi $id}```

## Delete dangling images (Should be the same that the last one)
```foreach ($id in docker images -q -f "dangling=true") {docker rmi $id}```
