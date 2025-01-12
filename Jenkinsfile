pipeline{
    agent any
    stages{
        stage("Zip the file"){
            steps{
                sh 'rm -rf *.zip || echo ""'  // This is to  delete all the previous zip code project
                sh 'zip -r ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
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
                ansible-${BUILD_ID}.zip \
                "http://ec2-3-94-254-251.compute-1.amazonaws.com:8081/artifactory/ansible/ansible-${BUILD_ID}.zip"'
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

        stage("Publish to ansible server"){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: ' AnsibleServer', \
                transfers: [sshTransfer(cleanRemote: false, excludes: '', \
                execCommand: '''unzip -o ansible-${BUILD_ID}.zip; rm -rf ansible-${BUILD_ID}.zip
''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, \
patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: '', \
sourceFiles: 'ansible-${BUILD_ID}.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
    
}