pipeline {
   agent any

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


   }

   post {
       success {
          emailext body: "${CUERPO_CORREO} proceso exitoso", subject: "${TITULO_CORREO}", to: "${LISTA_CORREOS}"
       }
       failure {
          emailext body: "${CUERPO_CORREO2} hay errores que revisar", subject: "${TITULO_CORREO}", to: "${LISTA_CORREOS}"
       }
       
   }
}