pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dstaszak7/jenkins-c-test.git'
            }
        }

        stage('Linter: Cppcheck & MISRA') {
            steps {
                echo 'Uruchamianie Cppcheck (Analiza statyczna i style MISRA)...'
                bat '"C:\\Program Files\\Cppcheck\\cppcheck.exe" --enable=all --inline-suppr bubble_sort.c'
            }
        }

        stage('Linter: Clang-Tidy') {
            steps {
                echo 'Uruchamianie Clang-Tidy...'
                bat 'clang-tidy bubble_sort.c -- -Wall'
            }
        }

        stage('Linter: Splint') {
            steps {
                echo 'Uruchamianie Splint...'
                bat 'C:\\splint\\bin\\splint.exe bubble_sort.c'
            }
        }

        stage('Build: GCC with Warnings') {
            steps {
                echo 'Kompilacja z flagami ostrzeżeń (Wall, Wextra, Wpedantic)...'
                bat '"C:\\mingw64\\bin\\gcc.exe" -Wall -Wextra -Wpedantic bubble_sort.c -o bubble.exe'
            }
        }

        stage('Final Run') {
            steps {
                echo 'Uruchamianie gotowego programu...'
                bat 'bubble.exe'
            }
        }
    }
    
    post {
        always {
            echo 'Zakończono proces analizy i budowania.'
        }
    }
}
