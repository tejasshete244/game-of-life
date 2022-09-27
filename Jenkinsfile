pipeline {
    agent {
        label {
            label 'built-in'
            customWorkspace '/mnt/projects/'
        }
    }
    stages {
        stage ('repo-clone'){
            steps {
                sh "rm -rf *"
                sh "git clone https://github.com/tejasshete244/game-of-life.git"
                sh "rm -rf /root/.m2/repository"
            }
        }
        stage ('mvn-build'){
            steps {
                dir('/mnt/projects/game-of-life/'){
                    sh 'mvn clean install'
                }
            }
        }
        stage ('deploy of war on node-a'){
            steps {
                sh "scp -i /mnt/WINDOWSKEYPAIR.pem /mnt/projects/game-of-life/gameoflife-web/target/gameoflife.war ec2-user@172.31.32.238:/mnt/web-server/apache-tomcat-9.0.65/webapps/"
            }
        }
        stage ('deploy of war on node-b'){
            steps {
                sh "scp -i /mnt/WINDOWSKEYPAIR.pem /mnt/projects/game-of-life/gameoflife-web/target/gameoflife.war ec2-user@172.31.36.227:/mnt/web-server/apache-tomcat-9.0.67/webapps/"
            }
        }
    }
}
