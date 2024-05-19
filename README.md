
Build Image (using cache if possible)
```batch
docker build -t github_test .
```

Build Image without using cache
```batch
docker build --no-cache -t github_test .
```

Run Image
```batch
docker run -it github_test 
```

Run image with .env file
```batch
docker run -it --env-file ./.env github_test 
```

Clone repository for testing
```batch
git clone repo_name
```

Check out branch to rest
```
git checkout branch_name
```

Note that if you clone a repository, you'll need to cd into the repository to emulate the working directory in Github actions (i.e., if you clone `my-repo`, you'll need to then run `cd my-repo`)

## Docker-In-Docker

This is for when you need to run a docker container that itself needs to run docker containers (i.e., if testing a Github Action that creates a docker image).
```
docker run --privileged -it --name github_test -p 5432:5432 docker:dind
```
This command starts the DinD container, mapping port 5432 from the host to port 5432 on the container. This setup is preparation for allowing the Secondary to connect back to Primary's port 5432 if necessary.

```
docker run --env-file ./.env -it --name github_test -v /var/run/docker.sock:/var/run/docker.sock github_test
```