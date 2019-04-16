pipeline {
    agent any
        stages {
            stage('compilar') {
                steps{ 
                    sh "./gradlew  compileJava"}
                }
            stage('test') {
                steps{ 
                    sh "./gradlew  test"}
                } 
            stage('build') {
                steps{
                    sh "./gradlew build"}
                }

            stage('construir docker') {
                steps{
                    sh "sudo docker build -t localhost:5000/calculadora ."}
                }

	   stage('subir imagen') {
                steps{
                    sh " sudo docker push  localhost:5000/calculadora"}
                }
           
            stage("borrar contenedor") {

            when {

                expression { sh script: '''if [ -z $(docker ps -f name=calculadora -q) ]; then true; else false; fi''', returnStatus: true

                  }

              }

            steps {

                sh "sudo docker stop calculadora"

                sh "sudo docker rm calculadora"

             }

        }


           stage('crear contenedor') {
                steps{
                    sh " sudo docker run -d -p 9090:8090 --name calculadora -t localhost:5000/calculadora"}
                }


            }
}
        
