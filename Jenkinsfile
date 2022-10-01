pipeline{
    agent any
    environment{
        RELEASE_REPO='vprofile-release'
        CENTRAL_REPO='vpro-maven-central'
        NEXUS_GRP_REPO= 'vpro-maven-group'
        SNAP_REPO ='vprofile-snapshot'
        NEXUSIP= '172.31.27.56'
        NEXUSPORT= '8081'
        NEXUS_USER= 'admin'
        NEXUS_PASS= 'admin'
        NEXUS_LOGIN='nexuslogin'
    }
   stages {
       stage('Build'){
           steps{
               sh 'mvn -s settings.xml -DskipTests install'
           }
           post{
               success{
                   echo "now Archiving"
                   archiveArtifacts artifacts: '**/target/*.war'

               }
           }
       }
       stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

	// stage('INTEGRATION TEST'){
    //         steps {
    //             sh 'mvn -s settings.xml verify -DskipUnitTests'
    //         }
    //     }
		
        stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }


    }
}