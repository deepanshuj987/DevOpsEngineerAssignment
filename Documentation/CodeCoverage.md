#JaCoCo Integration

To enable code coverage using JaCoCo and publish report using below script in Jenkins file

```
 pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    stages {
        stage('Build') {
            steps {
                // Build your project (replace with your build command)
                sh 'mvn clean package'
            }
        }

        stage('Test with JaCoCo') {
            steps {
                // Run tests with JaCoCo instrumentation
                sh 'mvn test -Djacoco-agent=yes'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                // Generate the JaCoCo HTML report
                sh 'mvn jacoco:report'
            }
        }

        stage('Publish Coverage Report') {
            steps {
                // Publish the coverage report to Jenkins
                publishCoverage(
                    allowMissing: false,
                    jacocoReportDirectory: 'target/site/jacoco',
                    reportNamePattern: 'index.html'
                )
            }
        }
    }
}
```
