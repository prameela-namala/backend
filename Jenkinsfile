pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        // Timeout counter starts BEFORE agent is allocated
        timeout(time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
        //retry(1)
    }
    environment { 
        DEBUG ='true'
        appVersion = ''
                    }
    stages {
        stage('Read the version') {
            steps {
               script{ 
                def packageJson = readJson file: 'package.json'
                appVersion = packageJson.version
                echo " App version: ${appVersion}"
            }
            }
        }
        stage('Test') {
            steps { 
                sh "echo this is test"
            }
        }
        stage('Deploy') {
            when{

                expression {env.GIT_BRANCH != 'origin/main'}
            }
            steps {
                sh "echo this is deploy"
                //error "pipeline failed"
            }
        }
        

    //     stage('approve') {
    //         input {
    //             message "Should we continue?"
    //             ok "Yes, we should."
    //             submitter "alice,bob"
    //             parameters {
    //                 string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    //             }
    //         }
    //         steps {
    //             echo "Hello, ${PERSON}, nice to meet you."
    //         }
    //     }
    // }

    post {
        always {
            echo "this section runs always"
            deleteDir()
        }

        success {

            echo "this section runs when pipeline success"
        }

        failure {
            echo "this section runs when pipeline fails"
        }
    }
}
