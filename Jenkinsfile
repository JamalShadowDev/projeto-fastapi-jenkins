pipeline{
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Fazer checkout do código do Git
                checkout scm
                
                // Debug: mostrar arquivos
                sh 'ls -la'
                sh 'ls -la backend/'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("jamalshadowdev/fastapi-jenkins:${env.BUILD_ID}", "-f ./backend/Dockerfile ./backend")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-credentials') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
        
        stage('Deploy no Kubernetes') {
            environment {
                tag_version = "${env.BUILD_ID}"
            }
            steps {
                script {
                    withKubeConfig([credentialsId: 'kubeconfig']) {
                        sh 'sed -i "s/{{tag}}/$tag_version/g" ./k8s/deployment.yaml'
                        sh 'kubectl apply -f k8s/deployment.yaml'
                    }
                }
            }
        }
    }
    
    post {
        always {
            chuckNorris()
        }
        
        success {
            echo '🚀 Deploy realizado com sucesso!'
            echo '💪 Chuck Norris aprova seu pipeline DevSecOps!'
            echo "✅ Imagem jamalshadowdev/fastapi-jenkins:${env.BUILD_ID} deployada no Kubernetes"
            echo "🌐 Aplicação disponível via Kind cluster"

            script {
                sh '''
                curl -H "Content-Type: application/json" -X POST -d '{
                    "embeds": [{
                        "title": "🚀 Deploy Successful!",
                        "description": "**Build #'"${BUILD_ID}"'** - FastAPI deployada com sucesso!\\n🌐 App: http://localhost:30001/docs",
                        "color": 65280,
                        "timestamp": "'"$(date -u +%Y-%m-%dT%H:%M:%S.000Z)"'"
                    }]
                }' https://discordapp.com/api/webhooks/1382709811996659813/HfYapx2_TVy-up5Vj3uOMKLURqmE8hrweccpd1__VW1lcU_vsNP2EDqLOh8O4wCyO69D
                '''
            }
        }
        
        failure {
            echo '❌ Build falhou, mas Chuck Norris nunca desiste!'
            echo '🔍 Chuck Norris está investigando o problema...'
            echo '💡 Verifique: Docker build, DockerHub push ou Kubernetes deploy'

            script {
                sh '''
                curl -H "Content-Type: application/json" -X POST -d '{
                    "embeds": [{
                        "title": "❌ Deploy Failed!",
                        "description": "**Build #'"${BUILD_ID}"'** falhou. Verificar logs.",
                        "color": 16711680,
                        "timestamp": "'"$(date -u +%Y-%m-%dT%H:%M:%S.000Z)"'"
                    }]
                }' https://discordapp.com/api/webhooks/1382709811996659813/HfYapx2_TVy-up5Vj3uOMKLURqmE8hrweccpd1__VW1lcU_vsNP2EDqLOh8O4wCyO69D       
                '''
            }
        }
    }
}