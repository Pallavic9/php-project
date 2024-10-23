pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/Pallavic9/php-project.git/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t pallavic9/phpproject:deploy1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockercreds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push pallavic9/phpproject:deploy1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
                script{
                    sh 'sudo docker run -itd --name My-project-con -p 8089:80 pallavic9/phpproject:deploy1'
                       }
                    }
                }
    }
}
