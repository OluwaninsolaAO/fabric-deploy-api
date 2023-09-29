# Fabric Deploy API

This is a helper script to help automates deployments on a list of remote servers.

### Usage

- Install all required dependencies using the bash script named `fabric-flask` from the project root.
- Copy the following script into the root of your project, create a service file the name `[PSN]_api.service` with the content:

```
[Unit]
Description=[Updates service file description]
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/[PSN]_api
ExecStart=/usr/bin/gunicorn --workers 1 --bind :5001 api.v1.app:app
StandardError=file:/tmp/[PSN]_api-error.log
StandardOutput=file:/tmp/[PSN]_api-access.log

[Install]
WantedBy=multi-user.target
```

> The script assumed the name of the user on the remote server to be ubuntu, and gunicorn if installed, located in `/usr/bin` directory. Also, update all occurrence of `PSN` to match your environment variable with which the fabfile will be working with.


### Fabfile goes full speed

```
$ fab -u ubuntu -H 102.88.88.100 deploy flush_db
```
