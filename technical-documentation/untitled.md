# Development Setup

## Local Setup {#local-setup}

1. Install [Docker CE](https://docs.docker.com/engine/installation/) for your OS. Also install Fabric via `pip install fabric`
2. Create .env file with the reference of`.env.example`or receive .env file from your team member.
3. Run`fab up`
4. Login to the backend using `fab ssh:backend`
5. Prepare data: load fixtures & run all required commands from [corresponding section](fixtures-and-management-commands-todo.md).
6. Go to [http://127.0.0.1:8082/](http://127.0.0.1:8082/) to see the frontend / polymer running. The Django app is running under

   ​[http://127.0.0.1:8082/api/](http://127.0.0.1:8082/api/)​

7. Create admin with `python manage.py createsuperuser`
8. Go to [http://127.0.0.1:8082/api/admin/](http://127.0.0.1:8082/api/admin/) login with your credentials.
9. **Important!** User created with superuser command will not be assosiated with any country, so frontend will fail. You need to assign the country manually in the admin panel from user edit page.
10.  And can now go to ​http://127.0.0.1:8082/tpm/ to see the frontend interface.

## Helpful Commands {#helpful-commands}

Here are some docker tips:

display all containers:

```text
$ docker ps
```

ssh into running django\_api container

```text
$ fab ssh:backend
```

stop all containers

```text
$ fab stop_docker_containers
```

cleanup docker system: remove all inactive containers

```text
$ docker system prune
```

