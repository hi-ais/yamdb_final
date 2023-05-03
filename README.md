# Study project: yamdb_final
The `api_yamdb` application is packaged in containers. Continuous Integration and Continuous Deployment are configured. Implemented:
-   automatic start of tests,
-   updating images on Docker Hub,
-   automatic deployment to the production server when pushing to the main branch **_main_.**

## Workflow status badge
![workflow](https://github.com/hi-ais/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

## Project setup

1. Clone the repository
 `git@github.com:hi-ais/yamdb_final.git`
2. Create and activate the virtual environment:
 `python -m venv venv` 
 `source venv/Scripts/activate` 
 `python -m pip install`
3. Install dependencies from a folder  `api_yamdb`: 
 `pip install -r requirements.txt`
4. Install the flake8 linter
 `pip install flake8 pep8-naming flake8-broken-line flake8-return flake8-isort`
5. Check code against PEP8 standards and run pytest:
  `python -m flake8`
  `pytest`
## Server preparation
1. Log in to your remote server in the cloud.
2. Stop the nginx service: 
  `sudo systemctl stop nginx`
3. Install Docker: 
   `sudo apt install docker.io`
4. Install docker-compose:
   `sudo apt-get update`
   `sudo apt-get install docker-compose-plugin`
5. Copy files docker-compose.yaml and nginx/default.conf from your project to the server in home/<ваш_username>/docker-compose.yaml and home/<ваш_username>/nginx/default.conf respectively:
    `scp docker-compose.yaml <USER>@<HOST>`
    `scp default.conf <USER>@<HOST>:/nginx/`
## Application Deployment
1. When pushing to the main branch, the application will pass the tests, update the image on DockerHub, and deploy to the server. Next, you need to connect to the server.
 `ssh <USER>@<HOST>`
2.Change to the running `api_yamdb` application container with the command:
`sudo docker container exec -it <CONTAINER ID> bash`
3. Inside the container, you need to perform migrations, connect statics and create a superuser:
 `python manage.py makemigrations reviews`
 `python manage.py migrate`
 `python manage.py collectstatic --no-input`
 `python manage.py createsuperuser`

