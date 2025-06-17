// Jenkinsfile (Declarative Pipeline)

// pipeline : Blok kode yang mendefinisikan seluruh Pipeline.
// Pipeline ini berisi serangkaian langkah(stages) yang otomatis, seperti build, testing, dan deploy aplikasi, yang dieksekusi secara berurutan atau paralel.

pipeline {
    // 1. agent: Mendefinisikan di mana pipeline akan berjalan
    agent any // Atau agent { docker { image 'maven:3.8.6-openjdk-11-slim' } } untuk spesifik

    // 2. tools: Mendefinisikan alat yang akan digunakan (misalnya, Maven, JDK)
    tools {
        // Nama alat harus sesuai dengan yang dikonfigurasi di "Manage Jenkins" -> "Tools"
        jdk 'JDK_21'
        maven 'Maven_V3'
    }

    // 3. stages: Blok utama yang berisi satu atau lebih stage
    stages {
        // Stage 1: Checkout source codw
        stage('Checkout') {
            steps {
                // Pull kode dari repositori Git
                git branch: 'master', url: 'https://github.com/Danu-prasetyo/simple-java-maven-app.git'
            }
        }

        // Stage 2: Membangun aplikasi (compile & package)
        stage('Build') {
            steps {
                // Menjalankan perintah Maven untuk membersihkan dan menginstal build
                sh 'mvn clean install'
            }
        }

        // Stage 3: Menjalankan unit tes
        stage('Test') {
            steps {
                // Menjalankan perintah Maven untuk menjalankan tes
                sh 'mvn test'
                // Opsi: Menerbitkan laporan tes JUnit
                // junit '**/target/surefire-reports/*.xml'
            }
        }

        // Stage 4: Deploy (simulasi)
        stage('Deploy') {
            steps {
                echo 'Simulating deployment...'
                // Kita bisa menambahkan langkah deployment yang sebenarnya di sini,
                // seperti menyalin JAR ke server lain, membangun Docker image, dll.
                sh 'cp target/*.jar /path/to/deployment/folder || true' // Contoh copy (akan gagal di Docker kontainer, hanya ilustrasi)
                echo 'Deployment simulated successfully!'
            }
        }
    }

    // 4. post: Tindakan yang akan dijalankan setelah pipeline selesai (selalu, berhasil, gagal, dll.)
    post {
        always {
            echo 'Pipeline finished.'
            // cleanWs() // Membersihkan workspace setelah build selesai
        }
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}