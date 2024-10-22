pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url: 'https://github.com/Pallavic9/php-project.git', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t pallavic9/phpproject:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockercreds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push pallavic9/phpproject:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockercreds', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 pallavic9/phpproject:v1'
                    sshagent(['sshkeypair']) {
                        //change the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@54.174.117.188 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@54.174.117.188 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
}
