If you want to backup your data volumes that are attached to running containers in Tutum, you can perform the following steps:

## Downloading volume data locally using the CLI
 
Run a SSH service that mounts the volumes of the service you want to backup (replacing `mysql` with the actual service name):

	tutum service run -n downloader -p 22:2222 -e AUTHORIZED_KEYS="$(cat ~/.ssh/id_rsa.pub)" --volumes-from mysql tutum/ubuntu

Run `scp` to download the files of the data volume (replacing `username` with your username and `/var/lib/mysql` with the path yu want to download):

	scp -r -P 2222 root@downloader-1.username.cont.tutum.io:/var/lib/mysql .
