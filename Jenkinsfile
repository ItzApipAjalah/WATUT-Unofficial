pipeline {
    agent any


    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Prepare Dependencies') {
            steps {
                echo 'Mengambil dan mem-build coroutil...'
                script {
                    if (isUnix()) {
                        sh '''
                        mkdir -p libs
                        git clone https://github.com/ItzApipAjalah/coroutil-unofficial.git coroutil_repo
                        cd coroutil_repo
                        chmod +x ./gradlew
                        ./gradlew build -b build_fabric.gradle --no-daemon
                        cp build/libs/coroutil-fabric-*.jar ../libs/
                        cd ..
                        '''
                    } else {
                        bat '''
                        if not exist "libs" mkdir "libs"
                        git clone https://github.com/ItzApipAjalah/coroutil-unofficial.git coroutil_repo
                        cd coroutil_repo
                        .\\gradlew.bat build -b build_fabric.gradle --no-daemon
                        copy build\\libs\\coroutil-fabric-*.jar ..\\libs\\
                        cd ..
                        '''
                    }
                }
            }
        }

        stage('Build Fabric') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'chmod +x ./gradlew'
                        sh './gradlew build -b build_fabric.gradle --no-daemon'
                    } else {
                        bat '.\\gradlew.bat build -b build_fabric.gradle --no-daemon'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Build berhasil!'
            // Menyimpan file jar yang dihasilkan sebagai artifact di Jenkins
            archiveArtifacts artifacts: 'build/libs/**/*.jar', allowEmptyArchive: true
        }
        failure {
            echo 'Build gagal. Silakan cek log untuk detailnya.'
        }
    }
}
