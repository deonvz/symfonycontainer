# symfonydockerized
Docker build project that provides you with Symfony 5, PHP, Nginx and Mariadb. It`s ready to run your app.

1) Clone the Repo
2) Run: docker-compose build
3) Run: docker-compose up

* Place your app in the apps\my-symfony-app location. 

Set variables in the .env file or call a specific env file for your enviroment. 
Example: 
docker-compose --env-file ./config/.env.dev up 
