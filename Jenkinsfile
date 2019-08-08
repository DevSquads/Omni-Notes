pipeline {
    agent any
    stages {
        stage('start emulator') {
             options {
                 timeout(time: 2, unit: 'MINUTES') 
             }
            steps {
                echo "Staring android emulator"
                sh 'emulator-headless -no-window -no-boot-anim -no-skin -no-audio @AVD_API_27 &'
                sh 'adb wait-for-device'
            }
        }
        stage('Building and running tests') {
            steps {
               sh './gradlew connectedAndroidTest'
            }
        }
    }
    post { 
        always {
            junit 'omniNotes/build/outputs/androidTest-results/connected/**/*.xml'
            sh 'adb emu kill'
        }
    }
}
