pipeline {
   agent {
     label "linux-agent"
    }

   environment {
       LISTA_CORREOS = 'kevinpavonucreativa@gmail.com'
       CUERPO_CORREO = "El pipeline ${BUILD_URL} se creo sin problemas,"
       CUERPO_CORREO2 = "El pipeline ${BUILD_URL} experimento problemas,"
       TITULO_CORREO = "Detalles pipeline ${BUILD_URL} STATUS"
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
              sh 'ls -la'
           }
       }

       //Despliegue
       //stage('Despliegue de la aplicacion'){
           //steps{
              //sh 'cp dist/CICD-kevin/*'
           //}
       //}
   }

   post {
       success {
          emailext body: "${CUERPO_CORREO} proceso exitoso", subject: "${TITULO_CORREO}", to: "${LISTA_CORREOS}"
       }
       failure {
          emailext body: "${CUERPO_CORREO2} revisar errores ", subject: "${TITULO_CORREO}", to: "${LISTA_CORREOS}"
       }
       
   }
}