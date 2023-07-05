pipeline {
   agent {
     label "linux-agent"
    }

   stages{
       //Integracion Continua
       stage('Instalar Dependencias'){
           steps{
              sh 'npm install'
           }
       }
       stage('Correr Pruebas Unitarias'){
           steps{
              echo "etapa de las pruebas unitarias empleando el comando: npm run test"
           }
       }
       stage('Correr SonarQube'){
           steps{
              withSonarQubeEnv('SonarQubeCursoCI'){
                  sh "/opt/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey=AngularApp -Dsonar.sources=src"
              }
           }
       }

       stage('Compilacion del APP'){
           steps{
              sh 'npm run build'
           }
       }

       stage('Mostrar Archivos'){
           steps{
              sh 'ls -la dist/'
           }
       }

       //Despliegue
       stage('Despliegue de la aplicacion'){
           steps{
              sh 'scp dist/cicd-kevin/* root@206.189.254.187:/usr/ucreativa/kevin-dev/'
           }
       }
   }
}