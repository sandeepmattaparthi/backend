pipeline {
    agent { label 'AGENT-1' }

    environment { 
        PROJECT = 'EXPENSE'
        COMPONENT = 'BACKEND'
    }

    options {
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }

    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', description: 'Enter a password')
    }

    stages {
        stage('read version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    env.appversion = packageJson.version
                    echo "Version is: ${env.appversion}"
                }
            }
        }

        stage('show parameters') {
            steps {
                echo "Hello ${params.PERSON}"
                echo "Choice selected: ${params.CHOICE}"
                echo "Biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"
            }
        }
    }

    post {
        always {
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure {
            echo 'I will run when pipeline is failed'
        }
        success {
            echo 'I will run when pipeline is success'
        }
    }
}
