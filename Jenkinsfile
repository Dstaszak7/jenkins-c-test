pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dstaszak7/jenkins-c-test.git'
    }
            }
        }
        stage('Build') {
            steps {
                bat '"C:\\mingw64\\bin\\gcc.exe" bubble_sort.c -o bubble.exe'
            }
        }
        stage('Run') {
            steps {
                bat 'bubble.exe'
            }
        }
    }
}
