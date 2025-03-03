pipeline{
    agent {
        docker {
            image "postman/newman"
            args "--entrypoint=''"
        }
        
    }


    parameters {
        choice(name: 'COLLECTION', choices: ['collection1', 'collection2', 'collection3'], description: 'choisir une collection')

    }

    stages{
        stage('verifier la version de newman'){
            steps{
                sh 'newman --version'
            }
        }
        stage('Test API'){
            steps{
                sh 'newman run collections/${params.COLLECTION}.json -r cli,junit --reporter-junit-export="newman-report.xml" -e env.json'
            }
        }
    }
    post{
        always {
            junit 'newman-report.xml'
        }
    }
}