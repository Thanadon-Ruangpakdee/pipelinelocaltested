pipeline {
    agent any
    
    // 1. เพิ่มส่วนนี้เพื่อให้ Jenkins รู้จักคำสั่ง npm
    tools {
        nodejs 'node' 
    }

    environment {
        CI = 'true'
    }

    stages {
        stage('Build') {
            steps {
                // 2. แนะนำให้ติดตั้ง dependencies ก่อน
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                // 3. เพิ่มการให้สิทธิ์รันสคริปต์ก่อนเรียกใช้
                sh 'chmod +x jenkins/scripts/test.sh'
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                // 4. ให้สิทธิ์รันสคริปต์สำหรับขั้นตอน Deliver เช่นกัน
                sh 'chmod +x jenkins/scripts/deliver.sh'
                sh './jenkins/scripts/deliver.sh'
                
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                
                sh 'chmod +x jenkins/scripts/kill.sh'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}