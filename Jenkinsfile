pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html/demo2"
    }

    stages {
        stage('Build / Validación') {
            steps {
                sh '''
                  if [ ! -f "index.html" ]; then
                    echo "ERROR: no existe index.html en el workspace"
                    exit 1
                  fi
                  # Reemplaza @@VERSION@@ por el número de build de Jenkins
                  sed -i "s/@@VERSION@@/$BUILD_NUMBER/g" index.html
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh """
                  mkdir -p "${DEPLOY_DIR}"
                  cp -v index.html "${DEPLOY_DIR}/index.html"
                """
            }
        }
    }

    post {
        success {
            echo "Despliegue exitoso en ${DEPLOY_DIR}"
        }
        failure {
            echo "Falló el pipeline. Revisá la consola del job."
        }
    }
}
