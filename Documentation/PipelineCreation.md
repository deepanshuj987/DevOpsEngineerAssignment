We will be using the Declarative pipeline for Jenkinsfile

To clone code in the System use the below script in "Jenkinsfile"

```
pipeline {
  agent {
    node {
      label 'maven'
    }
  }
  stages {
    stage("Clone-Code") {
      steps {
        git branch:'main',url:'https://github.com/deepnshuj987/*'
      }
    }
}
```

To trigger the pipeline automatically install the GitHub Webhook plugin in Jenkins

# Enable Webhook
1. Install "multibranch scan webhook trigger" plugin  
    From dashboard --> manage jenkins --> manage plugins --> Available Plugins  
    Search for "Multibranch Scan webhook Trigger" plugin and install it. 

2. Go to multibranch pipeline job
     job --> configure --> Scan Multibranch Pipeline Triggers --> Scan Multibranch Pipeline Triggers  --> Scan by webhook   
     Trigger token: `<token_name>`

3. Add webhook to GitHub repository
   Github repo --> settings --> webhooks --> Add webhook  
   Payload URl: `<jenkins_IP>:8080/multibranch-webhook-trigger/invoke?token=<token_name>`  
   Content type: `application/json`  
   Which event would you like to trigger this webhook: `just the push event` 


Once it is enabled make changes to source to trigger the build. 
