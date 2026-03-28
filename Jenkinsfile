pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Dstaszak7/jenkins-c-test.git'
            }
        }

        stage('Linter: Cppcheck') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    echo '--- ANALIZA CPPCHECK ---'
                    bat '"C:\\Program Files\\Cppcheck\\cppcheck.exe" --enable=all bubble_sort.c'
                }
            }
        }

        stage('Linter: Clang-Tidy') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    echo '--- ANALIZA CLANG-TIDY (WSZYSTKIE TESTY) ---'
                    // Dodano -checks=* dla bogatszego logu
                    bat '"C:\\Program Files\\LLVM\\bin\\clang-tidy.exe" bubble_sort.c -checks=* -- -Wall'
                }
            }
        }

        stage('Linter: Splint') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    echo '--- ANALIZA SPLINT ---'
                    bat 'C:\\splint\\bin\\splint.exe bubble_sort.c'
                }
            }
        }

        stage('Build: GCC with Warnings') {
            steps {
                echo '--- KOMPILACJA GCC (WALL, WEXTRA, WPEDANTIC) ---'
                bat '"C:\\mingw64\\bin\\gcc.exe" -Wall -Wextra -Wpedantic bubble_sort.c -o bubble.exe'
            }
        }

        stage('Final Run') {
            steps {
                echo '--- URUCHOMIENIE PROGRAMU ---'
                bat 'bubble.exe'
            }
        }
    }
}
