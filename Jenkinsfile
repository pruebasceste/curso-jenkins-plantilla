pipeline {
  agent any                         // usa el agente integrado de Jenkins
  options { timestamps() }          // añade hora a los logs (mejor depuración)

  stages {
    stage('Checkout') {
      steps {
        checkout scm                // clona el repo en el workspace
      }
    }
    stage('Build') {
      steps {
        bat 'echo Compilando...'
        bat 'dir'                   // lista archivos: útil para “ver” el workspace
      }
    }
    stage('Test') {
      steps {
        // “tests” de ejemplo. Cambia el 0 por 1 para simular fallo (rojo).
        bat 'echo Ejecutando tests... & exit /b 0'
      }
    }
    stage('Run script') {
      steps {
        // Ojo Windows: usa 'bat' y dobla la barra invertida en cadenas
        bat 'call scripts\\hola.bat'
      }
    }
    stage('Archive') {
      steps {
        // guarda un artefacto por build (el que crea tu hola.bat)
        archiveArtifacts artifacts: "build-${env.BUILD_NUMBER}.txt", fingerprint: true
      }
    }
  }

  post {
    success { echo '✅ Todo OK' }
    failure { echo '❌ Algo falló' }
    always  { echo "Build #${env.BUILD_NUMBER} finalizado" }
  }
}
