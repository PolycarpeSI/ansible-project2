pipeline{
    agent any
    stages{
        stage("Zip the file"){
            steps{
                sh 'zip ansible-{BUILD_ID}.zip * --exclude Jenkinsfile'
                //sh 'ls -l'
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

        stage("Upload artifact to JFrog"){
            steps{
                sh 'curl -uadmin:APBZrJk8pn85wcNmx47z1AoGCFp -T \
                ansible-{BUILD_ID}.zip \
                "http://ec2-3-94-254-251.compute-1.amazonaws.com:8081/artifactory/ansible/ansible-{BUILD_ID}.zip"'
            }
            post{
                success{
                    echo "========Successfully upload========"
                }
                failure{
                    echo "========Failed upload========"
                }
            }
        }
    }
    
}