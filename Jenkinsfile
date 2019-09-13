// Jenkinsfile (Declarative Pipeline)
pipeline {
    agent { 
        docker { 
            image 'php' 
            args '-u root:sudo'
        } 
    }
    stages {
        stage('build') {
            steps {
                /**
                 * Install packages
                 */
                sh '''apt-get update -q
                apt-get install git -y
                apt install zip -y
                apt install unzip -y
                '''
                /**
                 * Install composer
                 */
                sh '''
                    echo $USER
                    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
                    php -r "if (hash_file('SHA384', 'composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
                    php composer-setup.php
                    php -r "unlink('composer-setup.php');"
                    php composer.phar self-update
                    php composer.phar install --no-interaction
                    ls -la
                    vendor/bin/phpunit
                '''
                
            }
        }
    }
}
