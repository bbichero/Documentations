TaskBoard
------
_Task board php app for projects_

Environment:
```
Distribution: Debian 9.8
Kernel: Linux 4.9.0-8-amd64
```

Clone git repository:    
`git clone https://github.com/kiswa/TaskBoard.git`

Install mandatory package (php7, nginx / apache, mysql):   
`sudo apt install --no-install-recommends php7 php7-fpm php7.0-mbstring php7-mysql nginx maridb-server mariadb-client openjdk-8-jre phpunit composer bzip2`

Build package:   
```
cd TaskBoard
./build/composer.phar self-update
./build/build-all
```

Make www-data group owner of TaskBoard directory:   
```
sudo chown ${USER}:www-data -R ${PATH_TO_TASKBOARD}
sudo chmod 755 -R ${PATH_TO_TASKBOARD}
```

Create nginx web host for taskboard:
`vi /etc/apache2/sites-available/task-board.conf`

Active new virtual host:   
```
sudo ln -s /etc/nginx/site-available/taskboard.conf /etc/nginx/site-enable/taskboard.conf
sudo systemctl reload nginx
```

Connect to the mysql database, create user and database:
```
CREATE DATABASE IF NOT EXISTS task_board CHARACTER SET utf8 COLLATE utf8_general_ci;`
GRANT ALL PRIVILEGES ON ${TASKBOARD_DB}.* TO '${TASKBOARD_DB_USERNAME}'@'localhost' IDENTIFIED BY '${TASKBOARD_DB_PASSWD}';
FLUSH PRIVILEGES;
quit;
```

Edit line in api/api.php to use MySQL instead of SQLite:   
```
-R::setup('sqlite:'.__DIR__.'/taskboard.db');
+R::setup( 'mysql:host=localhost;dbname=${TASKBOARD_DATABASE}', '${TASKBOARD_DB_USERNAME}', '${TASKBOARD_DB_PASSWD}' );
```
