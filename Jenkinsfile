pipeline {

    agent any


    stages {
       stage ('GIT') {
            steps {
               echo "Getting Project from Git"; 
               git branch:"amal", url:"https://github.com/amalzouaghi01/ci-timesheet.git"; 
            }
        }

       stage("Build") {
           steps {
                bat "mvn -version"
                bat "mvn clean install"
            }
            post {
            success {
               jacoco()
               }
              } 
           
        }
       stage("Sonar") {
        steps {
           bat "mvn sonar:sonar"
         }
       }
       stage("nexus") {
        steps {
           bat "mvn deploy -Dmaven.test.skip"
         }
       }
       stage ('Email Notification') {
        steps {
         mail bcc: '', body: 'your pipeline is building', cc: '', from: '', replyTo: '', subject: 'Build', to: 'amal.zouaghi@esprit.tn'
          }
       }
       
       
    
   }   
}