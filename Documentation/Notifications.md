# Email Integration

1) Go to "Manage Jenkins --> Manage Plugins" --> Search for and install the "Email Extension"
2) Go to "Manage Jenkins --> Configure System" --> Under "Extended E-mail Notification"-->Enter your SMTP server address and port-->Set authentication details if required
3) Use below script to run
   ```
     pipeline {
    agent {
        node {
            label 'maven'
        }
    }
     stages {  
         stage('DemoTest') {  
             steps {  
                 sh 'echo "Fail!"; exit 1'  
             }  
         }  
     }  
     post {  
         always {  
             echo 'This will always run'  
         }  
         success {  
             echo 'This will run only if successful'  
         }  
         failure {  
             mail bcc: '', body: "<b>Example</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "DemoMail@gmail.com";  
         }  
         unstable {  
             echo 'This will run only if the run was marked as unstable'  
         }  
         changed {  
             echo 'This will run only if the state of the Pipeline has changed'  
             echo 'For example, if the Pipeline was previously failing but is now successful'  
         }  
     }  
   }
   ```
