pipeline{
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0']. description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    environment{
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('server-credentials')
    }
    
    stages{
        stage("build"){
            steps{
                echo 'building the application'
                echo "building version ${NEW_VERSION}"
            }
        }
        stage("test"){
            when {
                expression{
                    params.executeTests
                }
            }
            steps{
                echo 'testing the application'
            }
        }
        stage("deploy"){
            steps{
                echo "deploying the application"
                echo "deploying version ${params.VERSION}"
            }
        }

    }
}
