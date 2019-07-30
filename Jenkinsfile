pipeline {
    agent any
    stages {
        stage('start emulator') {
             options {
                 timeout(time: 2, unit: 'MINUTES') 
             }
            steps {
                echo "Staring android emulator"
                sh 'emulator-headless -no-window @Pixel_3_API_27'
                sh 'adb wait-for-device'
            }
        }
        stage('Building and running tests') {
            steps {
               sh './gradlew connectedAndroidTest'
            }
        }
        post { 
            always { 
                sh 'adb emu kill'
            }
        }
    }
}
