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
       }

    }
}