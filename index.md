## Useful commands
Here is a list of commands that I am using and tend to forget.

# Docker Command

Built image
`docker build -t container_name .`

Create container
`docker-compose up -d --build worker`

Restart container
`docker-compose restart container_name`

Stop & remove docker-compose container
`docker-compose stop container_name` & `docker-compose rm container_name`

Tail the last 50 log entries
`docker-compose logs -tf --tail="50"`

Get stats
`docker stats`

List all images
`docker image ls`

Remove an image
`docker rmi container_name container_name`

Open bash in running docker container
`docker exec -ti container_name bash`

Get IP of a container
`docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name_or_id`

Connect to postgresql db inside a docker container: `docker exec -it docker_postgres_1 psql -U user dbname`

## backup & restore docker volume

make backup
docker run --rm --volumes-from container_name -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /path/to/files/in/container


download to local machine
scp user@ip:~/backup.tar /some/folder/local/computer/backup.tar

upload
scp /some/folder/local/computer/backup.tar user@ip:~/backup.tar

restore volume
1) run a container with volume
2) docker run --rm --volumes-from container -v $(pwd):/backup ubuntu bash -c "cd /path/to/files/in/container && tar xvf /backup/backup.tar --strip 1"

# CRON
add a cron job on ubuntu: `crontab -e`


# Mount NFS disk
Temporary: `mount IP:/path_on_remote_machine path_on_local_machine`
Permanently: edit `/etc/fstab`

# General
Run simple HTML server: `python -m SimpleHTTPServer 8000`

Set up virtualenv: `virtualenv -p python3.7 env` & `source env/bin/activate`

Freeze pip packages: `pip freeze > requirements.txt`

Converts all XLS of one folder to CSV: `for x in $(ls *.xlsx); do x1=${x%".xlsx"}; in2csv $x > $x1.csv; echo "$x1.csv done."; done` (requires `csvkit` from `pip`)

Find modified files from last X days on a mac: `find path_to_folder  -type f -mtime -10 > ~/Desktop/modfiles.txt`

Location of mail on Ubuntu: `/var/mail/<user>`

List failed login attempt on SSH: `grep "Failed password" /var/log/auth.log`

Generate hashed password (for simple auth): `echo $(htpasswd -nbB <USER> "<PASS>") | sed -e s/\\$/\\$\\$/g`
NOTE: need the second part only if putting password directly in docker-compose as one needs to escape $ signs

Solve problem of migration in Django: `python manage.py migrate --run-syncdb`

creater admin user in django: `python manage.py createsuperuser`

Find logs/Events on windows: `Event Viewer`

# Git

`git fetch origin master`
`git merge`
`git add --all`
`git commit -m "some text"`
`git push origin master`
