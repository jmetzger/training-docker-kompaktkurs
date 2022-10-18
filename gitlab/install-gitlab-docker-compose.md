# Install gitlab with docker-compose

## Walkthrough (with smtp) 

```
mkdir -p /srv/gitlab 
```

```
cd
mkdir gitlab
cd gitlab 
```

```
# nano .env 
GITLAB_HOME=/srv/gitlab
POSTGRE_USR=project 
POSTGRE_PWD=mypass
REDIS_VERSION=7.0.5
GITLAB_VERSION=gitlab-ce:15.4.2-ce.0
```

```
# nano docker-compose.yaml 
version: '3.9'
services:
 
  redis:
    restart: always
    image: redis:${REDIS_VERSION}
    command:
    - --loglevel warning
    volumes:
    - ${GITLAB_HOME}/redis-data:/data
 
  web:
    image: 'gitlab/${GITLAB_VERSION}'
    restart: unless-stopped
    hostname: '${HOSTNAME}'
    healthcheck:
      test: ["CMD", "/opt/gitlab/bin/gitlab-healthcheck"]
      interval: 5m
      timeout: 10s
      retries: 3
      start_period: 5m
    ports:
      - '80:80'
      - '443:443'
#      - '2222:22'  
    depends_on:
      database:
        condition: service_healthy
      redis:
        condition: service_started
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'https://${HOSTNAME}'
        nginx['proxy_set_headers'] = {
          "X-Forwarded-Proto" => "https",
          "X-Forwarded-Ssl" => "on"
        }
        gitlab_rails['time_zone'] = 'UTC'
        redis['enable'] = true
        gitlab_rails['redis_host'] = "redis"
        gitlab_rails['redis_port'] = 6379                 
        gitlab_rails['db_adapter'] = "postgresql"
        gitlab_rails['db_database'] = "gitlab"
        gitlab_rails['db_username'] = "${POSTGRE_USR}"
        gitlab_rails['db_password'] = "${POSTGRE_PWD}"
        gitlab_rails['db_host'] = "database"
        registry['enable'] = false
        gitlab_rails['backup_archive_permissions'] = 0644
        gitlab_rails['backup_keep_time'] = 1468800

    volumes:
      - ${GITLAB_HOME}/gitlab-ee-data_conf:/etc/gitlab
      - ${GITLAB_HOME}/gitlab-ee-data_logs:/var/log/gitlab
      - ${GITLAB_HOME}/gitlab-ee-data_data:/var/opt/gitlab
    shm_size: '256m'     
 
  runner_01:
    image: gitlab/gitlab-runner:alpine  
    restart: always
    depends_on:
      - web
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ${GITLAB_HOME}/gitlab_runner_01_settings:/etc/gitlab-runner
      - ${GITLAB_HOME}/gitlab_runner_01_data:/home/gitlab-runner     
 
  database:
    image: postgres:12-alpine
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "pg_isready", "-q", "-d", "postgres", "-U", "project"]
      timeout: 45s
      interval: 10s
      retries: 10
    environment:
      POSTGRES_USER: "${POSTGRE_USR}"
      POSTGRES_PASSWORD: "${POSTGRE_PWD}"
      POSTGRES_DB: gitlab
    volumes:
      - ${GITLAB_HOME}/gitlab-ee-data_db:/var/lib/postgresql/data
```




## Example (Full)

```
version: '3.9'
services:
 
  redis:
    restart: always
    image: redis:${REDIS_VERION}
    command:
    - --loglevel warning
    volumes:
    - ${GITLAB_HOME}/redis-data:/data
 
  web:
    image: 'gitlab/${GITLAB_VERSION}'
    restart: unless-stopped
    hostname: '${HOSTNAME}'
    healthcheck:
      test: ["CMD", "/opt/gitlab/bin/gitlab-healthcheck"]
      interval: 5m
      timeout: 10s
      retries: 3
      start_period: 5m
    ports:
      - '80:80'
      - '443:443'
#      - '2222:22'  
    depends_on:
      database:
        condition: service_healthy
      redis:
        condition: service_started
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'https://${HOSTNAME}'
        nginx['proxy_set_headers'] = {
          "X-Forwarded-Proto" => "https",
          "X-Forwarded-Ssl" => "on"
        }
        gitlab_rails['time_zone'] = 'UTC'
        redis['enable'] = true
        gitlab_rails['redis_host'] = "redis"
        gitlab_rails['redis_port'] = 6379                 
        gitlab_rails['db_adapter'] = "postgresql"
        gitlab_rails['db_database'] = "gitlab"
        gitlab_rails['db_username'] = "${POSTGRE_USR}"
        gitlab_rails['db_password'] = "${POSTGRE_PWD}"
        gitlab_rails['db_host'] = "database"
        registry['enable'] = false
        gitlab_rails['backup_archive_permissions'] = 0644
        gitlab_rails['backup_keep_time'] = 1468800
        gitlab_rails['smtp_enable'] = true
        gitlab_rails['smtp_address'] = "${SMTP_DOMAIN}"
        gitlab_rails['smtp_port'] = 465
        gitlab_rails['smtp_user_name'] = "${SMTP_USER}"
        gitlab_rails['smtp_password'] = "${SMTP_PASS}"
        gitlab_rails['smtp_domain'] = "${SMTP_DOMAIN}"
        gitlab_rails['smtp_authentication'] = "login"
        gitlab_rails['smtp_enable_starttls_auto'] = true
        gitlab_rails['smtp_tls'] = false
        gitlab_rails['smtp_ssl'] = true
        gitlab_rails['smtp_force_ssl'] = true
        gitlab_rails['gitlab_email_from'] = '${SMTP_EMAIL}'
    volumes:
      - ${GITLAB_HOME}/gitlab-ee-data_conf:/etc/gitlab
      - ${GITLAB_HOME}/gitlab-ee-data_logs:/var/log/gitlab
      - ${GITLAB_HOME}/gitlab-ee-data_data:/var/opt/gitlab
    shm_size: '256m'     
 
  runner_01:
    image: gitlab/gitlab-runner:alpine  
    restart: always
    depends_on:
      - web
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ${GITLAB_HOME}/gitlab_runner_01_settings:/etc/gitlab-runner
      - ${GITLAB_HOME}/gitlab_runner_01_data:/home/gitlab-runner     
 
  database:
    image: postgres:12-alpine
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "pg_isready", "-q", "-d", "postgres", "-U", "project"]
      timeout: 45s
      interval: 10s
      retries: 10
    environment:
      POSTGRES_PASSWORD: "${POSTGRE_PWD}"
      POSTGRES_DB: gitlab
    volumes:
      - ${GITLAB_HOME}/gitlab-ee-data_db:/var/lib/postgresql/data
 ```


## Reference: 

  * https://docs.gitlab.com/ee/install/docker.html#install-gitlab-using-docker-compose
