# Symfony project from scratch

This is a repository with an empty Symfony project.
List of commands to reproduce it:
### Create composer symfony project
```shell
docker run -v "$(pwd)":/app -it --rm --user 1000:1000 composer create-project symfony/skeleton .
```
Install dockerizer to run nginx, php and mysql docker containers: 
```shell
curl -s https://raw.githubusercontent.com/OleksiiBulba/php-dockerizer/feature/create-project-installation/bin/onlinesetup | bash -s -- https://github.com/OleksiiBulba/php-dockerizer feature/create-project-installation
```
Initialize and run project:
```shell
make init
make run
```
Enter the php container:
```shell
make bash
```
And install required composer packages:
```shell
composer require symfony/maker-bundle --dev
composer require template
composer require profiler --dev
```
Maker-bundle for creating symfony objects directly from php cli. Template for twig. Profiler to add Web Profiler Toolbar to every page for debugging.

## PHPStorm setup
Open _File->Settings->PHP->Debug_, check "Break at first line in PHP scripts"
Open _File->Settings->PHP->Servers_, create new server with any name and hostname `nginx` (as container name in .dockerizer/docker-compose.base.yaml), check "Use path mapping" and add one "<project root> -> /var/www/html". From now on when you turn debug on in PHPStorm, every request to localhost will start a new debug session in PHPStorm.