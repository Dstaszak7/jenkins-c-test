pipeline {
    agent any
    stages {
        stage('Linter: Cppcheck') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    bat '"C:\\Program Files\\Cppcheck\\cppcheck.exe" --enable=all bubble_sort.c'
                }
            }
        }
        stage('Linter: Clang-Tidy') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    // Podajemy pełną ścieżkę, żeby nie było błędu "not recognized"
                    bat '"C:\\Program Files\\LLVM\\bin\\clang-tidy.exe" bubble_sort.c -- -Wall'
                }
            }
        }
        stage('Linter: Splint') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    bat 'C:\\splint\\bin\\splint.exe bubble_sort.c'
                }
            }
        }
        stage('Build: GCC with Warnings') {
            steps {
                bat '"C:\\mingw64\\bin\\gcc.exe" -Wall -Wextra -Wpedantic bubble_sort.c -o bubble.exe'
            }
        }
        stage('Final Run') {
            steps {
                bat 'bubble.exe'
            }
        }
    }
}
