pipeline{
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }   
    environment{
        SNAP_REPO = 'vprofile-snapshot'
        RELEASE_REPO = 'vprofile-release'
        //proxy
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        //NOTE:the nexusip will be be private where the nexus has been installed
        NEXUSIP = '172.31.4.146'
        NEXUSPORT = '8081'
        //The user and pwd is the one through whcich we loging in the web
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        //the "ID" that has been given while creating the nexus credential in jenkins
        NEXUS_LOGIN= 'nexuslogin'

        
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "NOw archiving"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage ('Test') {
            steps{
                sh 'mvn test'
            }
        }
        stage ('Checkstyle Analysis') {
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
    }
}