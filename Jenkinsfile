pipeline {
    agent any

    tools {
        // Pastikan Anda telah mengonfigurasi JDK 21 di Jenkins (Manage Jenkins -> Global Tool Configuration)
        jdk 'jdk21' 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Prepare Dependencies') {
            steps {
                // Catatan: Karena mod ini membutuhkan coroutil-fabric di folder 'libs', 
                // Anda mungkin perlu menambahkan langkah untuk mendownload/build coroutil terlebih dahulu,
                // atau pastikan file jar tersebut tersedia di environment Jenkins.
                echo 'Memastikan dependencies siap...'
                
                // Contoh jika Anda ingin membuat folder libs:
                // sh 'mkdir -p libs'
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
