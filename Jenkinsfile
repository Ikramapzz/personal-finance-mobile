pipeline {
  agent any
 
  environment {
    APK_PATH = 'android/app/build/outputs/apk/release/app-release.apk'
    JAVA_HOME= '/usr/lib/jvm/java-21-openjdk-amd64'
    ANDROID_HOME = '/home/kiaq-lap-114/android-sdk'
 
  }
 
  stages {
    stage('1. Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/Ikramapzz/personal-finance-mobile.git'
      }
    }
 
    stage('2. npm install') {
      steps {
        sh "npm ci"
      }
    }
 
    stage('3. prebuild') {
      steps {
        sh "npx expo install --fix"
        sh "npx expo prebuild"
      }
    }
 
    stage('4. build apk file') {
      steps {
        sh '''
          cd android &&
          echo "sdk.dir=${ANDROID_HOME}" > local.properties &&
          chmod +x gradlew &&
          sed -i "s|distributionUrl=.*|distributionUrl=https\\\\://services.gradle.org/distributions/gradle-8.13-bin.zip|" gradle/wrapper/gradle-wrapper.properties &&
          ./gradlew assembleRelease --build-cache --no-daemon 
        '''
      }
    }
  }
}
    
