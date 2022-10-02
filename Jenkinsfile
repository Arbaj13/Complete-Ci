pipeline{
    agent any
    environment{
        RELEASE_REPO='vprofile-release'
        CENTRAL_REPO='vprofile-maven-central'
        NEXUS_GRP_REPO= 'vprofile-group'
        SNAP_REPO ='vprofile-snapshot'
        NEXUSIP= '172.31.29.82'
        NEXUSPORT= '8081'
        NEXUS_USER= 'admin'
        NEXUS_PASS= 'admin'
        NEXUS_LOGIN='nexuslogin'
        SONARSCANNER='sonarscanner'
        SONARSERVER='sonarserver'
    }
stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now Archiving artifacts"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        // stage('Test'){
        //     steps {
        //         sh 'mvn -s settings.xml test'
        //     }

        // }

        stage('Checkstyle Analysis'){
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }

        stage('Sonar Analysis') {
            environment {
                scannerHome = tool "${SONARSCANNER}"
            }
            steps {
               withSonarQubeEnv("${SONARSERVER}") {
                   sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
              }
            }
        }

    }
}