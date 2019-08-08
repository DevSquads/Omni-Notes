pipeline {
    agent any
    stages {
        stage('start emulator') {
             options {
                 timeout(time: 2, unit: 'MINUTES') 
             }
            steps {
                echo "Staring android emulator"
                sh 'echo $ANDROID_SDK_HOME'
                sh 'echo $ANDROID_SDK_ROOT'
                sh 'emulator-headless -no-window -no-boot-anim -no-skin -no-audio -memory 8192 @AVD_API_28 &'
                sh 'adb wait-for-device'
            }
        }
        stage('Building and running tests') {
            steps {
               sh './gradlew clean'
               sh './gradlew connectedAndroidTest'
            }
        }
    }
    post {
        always {
            sh 'adb emu kill'
            junit 'omniNotes/build/outputs/androidTest-results/connected/**/*.xml'
        }
    }
}
