pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "ymg2-maven2" // Container adları ymg_backend gibi olur
    }

    stages {
        stage('🧬 Repoyu Klonla') {
            steps {
                git branch: 'main', url: 'https://github.com/yarenibis/ymg2-maven.git'
            }
        }

        stage('🐳 Docker Compose ile Build Et') {
            steps {
                echo 'Docker Compose ile tüm servisler build ediliyor...'
                bat 'docker-compose -f docker-compose.yml build'
            }
        }

        stage('🧹 Eski Konteynerları Durdur & Sil') {
            steps {
                echo 'Var olan konteynerlar durduruluyor (varsa)...'
                bat '''
                    docker-compose -f docker-compose.yml down || exit 0
                '''
            }
        }

        stage('🚀 Servisleri Başlat') {
            steps {
                echo 'Tüm servisler başlatılıyor...'
                bat 'docker-compose -f docker-compose.yml up -d'
            }
        }
    }

    post {
        success {
            echo '✅ Yayın başarıyla tamamlandı!'
        }
        failure {
            echo '❌ Yayın başarısız oldu, lütfen logları kontrol edin.'
        }
    }
}