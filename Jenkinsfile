pipeline{
    agent any
    stages{
        stage("Zip the file"){
            steps{
                sh 'zip ansible-{BUILD_ID}.zip * --exclude Jenkinsfile'
                sh 'ls -l'
            }
            post{
                success{
                    echo "========Successfully zip========"
                }
                failure{
                    echo "========Failed zip========"
                }
            }
        }
    }
    
}