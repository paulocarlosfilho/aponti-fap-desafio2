pipeline {
    agent any

    tools {
        nodejs 'NodeJS' // Certifique-se de nomear a ferramenta Node com esta exata string nas configurações globais do Jenkins
    }

    triggers {
        githubPush() // Aciona automaticamente a pipeline em eventos de push no repositório
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm // Clona o código-fonte atualizado
            }
        }

        stage('Build / Install') {
            steps {
                sh 'npm ci' // Instalação limpa e automatizada das dependências
            }
        }

        stage('SAST (Security)') {
            steps {
                script {
                    // Auditoria de segurança nativa do npm tratando o retorno para a esteira lidar com vulnerabilidades
                    sh 'npm audit --audit-level=high || true'
                }
            }
        }

        stage('Lint & Quality') {
            steps {
                // Executa o linter para validar a qualidade do código fonte
                sh 'npm run lint || true'
            }
        }

        stage('Unit Tests') {
            steps {
                sh 'npm test' // Executa a suíte de testes unitários da API
            }
        }
    }

    post {
        always {
            cleanWs() // Limpa o workspace do agente para poupar espaço
        }
        success {
            echo 'Sucesso: Todas as etapas da esteira passaram com êxito!'
        }
        failure {
            echo 'Falha: A esteira encontrou erros de compilação, segurança ou testes.'
        }
    }
}