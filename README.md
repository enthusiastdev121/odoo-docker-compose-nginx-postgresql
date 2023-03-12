# Odoo ERP, PostgreSQL and Nginx Compose 🔥 🇧🇷

  + Odoo
  + PostgreSQL
  + Nginx 
  + Installations and use simplified ❤

## Odoo ERP 🖥️
![project-image](https://user-images.githubusercontent.com/59855397/216739166-c91ef374-50d4-4b9e-bfb4-987954f5f0f2.png)


### Clone this repository

    git clone https://github.com/DanielNery/odoo-docker-compose-nginx-postgresql.git --branch=master

### Commands

    # Check services running on ports of interest
    sudo lsof -i -P -n | grep 80

    # Kill process running on port of interest
    sudo service apache2 stop

    # Containers Up
    sudo docker-compose up -d
    # Obs: 'd' is from detached

    # Down containers (Alert: This deletes all config your containers)
    sudo docker-compose down
    

    # See Logs
    sudo docker-compose logs --tail=100 -f
    

    # Start, Stop and check containers
    sudo docker-compose start
    sudo docker-compose stop
    sudo docker-compose ps
    
    # Init database with base modules
    sudo docker-compose stop odoo && \
    sudo docker-compose run --rm odoo odoo -c /etc/odoo/odoo.conf -i base --stop-after-init && \
    sudo docker-compose restart


    # Up Odoo updating modules
    sudo docker-compose stop odoo && \
    sudo docker-compose run --rm odoo odoo -c /etc/odoo/odoo.conf -u modules_name --stop-after-init && \
    sudo docker-compose restart
    

    # Generate database backup
    export DATABASE=your_database && sudo docker-compose run --rm -e PGPASSWORD=odoo -e DATABASE=$DATABASE db pg_dump -h db -U odoo $DATABASE > /tmp/db-${DATABASE}-$(date +%Y%m%d%H%M).dump


    # Restore your database
    cat your_file_name.dump | docker exec -i postgresql psql -U odoo -d your_database_name


    # Security copy 'dumps files' from server to your local machine
    scp server_user@link_server:/tmp/db-your_db_name.dump ~/Downloads/db-your_db_name.dump &&
    scp -r server_user@link_server:/home/ubuntu/projects/your-erp/odoo-web-data/filestore/your_filestore_name ~/Downloads/your_filestore_name


    # List databases on postgres container
    docker exec postgresql psql -U odoo -l


    # Delete databases on postgres container
    docker exec postgresql psql -U odoo drop database your_database_name

##  Documentation 📜

+ https://docs.docker.com/
+ https://docs.docker.com/compose/
+ https://www.odoo.com/documentation/14.0/
+ https://nginx.org/en/docs/
+ https://www.postgresql.org/docs/

### Linux Basic Commands 🐧

` sudo apt update && sudo apt upgrade -y ` <br/>
` sudo apt install docker docker-compose -y ` <br/>
` git clone https://github.com/DanielNery/odoo-docker-compose-nginx-postgresql.git ` <br/>
` cd odoo-docker-compose-nginx-postgresql ` <br/>
` sudo docker-compose up -d ` <br/>

### Windowns or Mac Tutorial 🍎

  + Install Docker Desktop https://www.docker.com/products/docker-desktop/
  
    ` git clone https://github.com/DanielNery/odoo-docker-compose-nginx-postgresql.git ` <br/>
    ` cd odoo-docker-compose-nginx-postgresql ` <br/>
    ` docker-compose up -d ` <br/>


### Update or custom modules 🍺
  
  `docker-compose stop odoo && sudo docker-compose run --rm odoo odoo -c /etc/odoo/odoo.conf -u your_module 
  --stop-after-init && docker-compose start odoo` <br/>
  
### Contact 📞
  
  + Linkedin: https://www.linkedin.com/in/danielpontesnery/
  + Email: danielpontesnery@gmail.com
  
