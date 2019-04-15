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
                    sh " sudo docker push -t localhost:5000/calculadora"}
                }

           stage('crear contenedor') {
                steps{
                    sh " sudo docker run -d -p 9090:8080 --name calculador -t localhost:5000/calculadora"}
                }


            }
}
        
