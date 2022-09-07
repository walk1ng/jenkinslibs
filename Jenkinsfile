#!groovy

@Library('jenkinslibs') _ 

def tools = new org.devops.tools()

hello()

pipeline {
    agent any
    
    options {
        timestamps()
    }

    parameters {
        string defaultValue: '1', name: 'sprint', trim: true
    }

    stages {
        stage('pwork') {
            parallel {
                // One or more stages need to be included within the parallel block.
                stage("worker 01") {
                    steps {
                        echo 'pwork-worker01-do-work'
                    }
                }
                stage("worker 02") {
                    steps {
                        echo 'pwork-worker02-do-work'
                    }
                }
            }
        }
        stage('GetCode') {
            when {
                environment name: 'mode', value: 'production'
            }
            steps {
                echo 'Get code'
                script {
                    gitHome = tool 'Default'
                    print(gitHome)
                }
                
                input message: 'is it ok?', ok: 'ok, go ahead', parameters: [choice(choices: ['one', 'two'], name: 'your_choice')], submitterParameter: 'who_submit'

            }
        }

        stage('ScanCode') {
            steps {
                echo 'Scan code'
                script {
                    tools.PrintMsg('hello my jenkins library!')
                }
            }
        }
        stage('BuildCode') {
            steps {
                echo 'Build code'
            }
        }
        stage('BuildImage') {
            steps {
                echo 'Build Image'
            }
        }
        stage('PushImage') {
            steps {
                echo 'Push Image'
                echo "${mode}"
            }
        }
    }
    
    post {
          always {
            // One or more steps need to be included within each condition's block.
            echo 'always execute'
            echo "we are working on sprint ${sprint}"
          }
          success {
            // One or more steps need to be included within each condition's block.
            echo 'on success'
          }
          aborted {
              echo 'aborted by someone'
          }
    }
}
