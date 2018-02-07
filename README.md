This is a fork from https://github.com/php-pm/php-pm modified to demonstrate the usage of [SonarQube](https://www.sonarqube.org/) in the context of a PHP project.

# Change Log

Modifications compared to the original project:

1. `sonar-project.properties` was added, which is the configuration file for Sonar scanner, the command line tool performing the static code analysis
2. `phpunit.xml.dist` was modified to produce log files that can be picked ob by the Sonar scanner to report test coverage metrics
3. `Vagrantfile` was added to have a clean test environment

# Before Running Sonar Scanner

1. Launch the vagrant box with `vagrant up`
2. Log into the box `vagrant ssh`
3. Go to `/vagrant`
4. Run `composer install`
5. Install Xdebug [following these instructions](https://kevdees.com/installing-xdebug-for-php7/)
6. Run PHPunit `./vendor/bin/phpunit --verbose -c phpunit.xml.dist`

As a result, you should get the files `clover.xml` and `junit-logfile.xml` in your project root.

# Running Sonar Scanner

Exit the Vagrant box and run the Docker container with the Sonar scanner.

    export DOCKERWORKDIR='/vagrant';
    docker run --rm \
        --mount type=bind,source="$(pwd)",target=$DOCKERWORKDIR \
        -w=$DOCKERWORKDIR --network=sonar \
        sonar-scanner:latest sonar-scanner

Note: setting `DOCKERWORKDIR` to `/vagrant` is important because this is the base directory in which PHPUnit was executed, i.e. file references in `clover.xml` use this as the base directory.