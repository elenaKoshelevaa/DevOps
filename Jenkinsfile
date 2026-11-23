
pipeline {
    agent any

    options {
        timestamps()
    }

    stages {

        stage('Подготовка окружения') {
            steps {
                echo 'Этап 1: установка Docker и клонирование репозиториев'

                ansiblePlaybook(
                    installation: 'Ansible',
                    playbook: 'ansible/playbook.yml',
                    inventory: 'ansible/hosts',
                    credentialsId: 'vm-ssh-key',
                    vaultCredentialsId: 'ansible-vault-password',
                    tags: 'prepare',
                    hostKeyChecking: false,
                    colorized: true
                )
            }
        }

        stage('Запуск приложений') {
            steps {
                echo 'Этап 2: запуск микросервисов через Docker Compose'

                ansiblePlaybook(
                    installation: 'Ansible',
                    playbook: 'ansible/playbook.yml',
                    inventory: 'ansible/hosts',
                    credentialsId: 'vm-ssh-key',
                    vaultCredentialsId: 'ansible-vault-password',
                    tags: 'start',
                    hostKeyChecking: false,
                    colorized: true
                )
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline успешно выполнен!'
            echo 'Микросервисы frontend и backend запущены.'
        }

        failure {
            echo 'Ошибка при выполнении CI/CD Pipeline!'
        }
    }
}
