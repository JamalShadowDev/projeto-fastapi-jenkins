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

        stage('Security Scan - Trivy') {
            steps {
                script {
                    def timestamp = new Date().format("yyyy-MM-dd_HH-mm-ss")
                    def buildTime = new Date().format("yyyy-MM-dd HH:mm:ss")
                    
                    echo "🔍 Iniciando Security Scan com Trivy..."
                    
                    // Instalar Trivy se necessário
                    sh '''
                    if ! command -v trivy &> /dev/null; then
                        echo "📦 Instalando Trivy..."
                        curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin
                    fi
                    '''
                    
                    // Criar pasta logs
                    sh "mkdir -p security-logs"
                    
                    echo "🔍 Executando scan na imagem: jamalshadowdev/fastapi-jenkins:${env.BUILD_ID}"
                    
                    // Executar scan e salvar relatório completo temporário
                    def scanResult = sh(
                        script: """
                        trivy image --exit-code 1 --severity CRITICAL,HIGH \
                        --format table jamalshadowdev/fastapi-jenkins:${env.BUILD_ID} > trivy-temp-report.txt 2>&1
                        """,
                        returnStatus: true
                    )
                    
                    // Ler o relatório completo
                    def fullReport = readFile('trivy-temp-report.txt')
                    
                    // Determinar status do Quality Gate
                    def qualityGateStatus = scanResult == 0 ? "PASSED ✅" : "FAILED ❌"
                    def deployAllowed = scanResult == 0 ? "YES" : "NO"
                    def deployStatus = scanResult == 0 ? "Successful deploy ✅" : "Unsuccessful deploy ❌"
                    
                    // Criar arquivo individual completo (resumo + relatório)
                    def individualReport = """=== SECURITY SCAN REPORT ===
Build: #${env.BUILD_ID}
Timestamp: ${timestamp}
Image: jamalshadowdev/fastapi-jenkins:${env.BUILD_ID}
Quality Gate: ${qualityGateStatus}
Deploy Allowed: ${deployAllowed}
=== END REPORT ===


=== DETAILED TRIVY SCAN RESULTS ===

${fullReport}

=== END DETAILED RESULTS ===
"""
                    
                    // Salvar arquivo individual
                    writeFile file: "security-logs/build-${env.BUILD_ID}-${timestamp}.txt", text: individualReport
                    
                    // Adicionar linha ao arquivo histórico
                    def historyEntry = """Build: #${env.BUILD_ID}
Timestamp: ${timestamp}
${deployStatus}

"""
                    
                    // Append ao arquivo histórico (criar se não existir)
                    sh """
                    echo '${historyEntry}' >> security-logs/builds-history.log
                    """
                    
                    // Limpar arquivo temporário
                    sh "rm -f trivy-temp-report.txt"
                    
                    // Arquivar logs
                    archiveArtifacts artifacts: 'security-logs/**', allowEmptyArchive: true
                    
                    // QUALITY GATE - Bloquear se CRITICAL ou HIGH
                    if (scanResult != 0) {
                        echo """
🚨 SECURITY QUALITY GATE FAILED! 🚨

❌ Vulnerabilidades CRITICAL ou HIGH encontradas!
❌ DEPLOY BLOQUEADO por segurança!

Verifique: security-logs/build-${env.BUILD_ID}-${timestamp}.txt

Chuck Norris não permite HIGH vulnerabilities! 🥋🛡️
"""
                        error("🚨 Security Quality Gate Failed - Deploy bloqueado!")
                    }
                    
                    echo "✅ Security Quality Gate PASSED - Deploy autorizado!"
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
                        "title": "🚀 Secure Deploy Successful!",
                        "description": "**Build #${BUILD_ID}** passou no Security Quality Gate!\\n\\n🌐 **App**: http://localhost:30001/docs\\n🔒 **Security**: No Critical/High vulnerabilities\\n✅ **Status**: Deploy autorizado\\n\\n🛡️ Chuck Norris approved this secure deploy!",
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
                        "title": "❌ Deploy Failed/Blocked",
                        "description": "**Build #${BUILD_ID}** failed!\\n\\n❌ **Possível causa**: Security vulnerabilities\\n🔗 **Logs**: [Build #${BUILD_ID}](${BUILD_URL})\\n\\n🛡️ Chuck Norris protects production!",
                        "color": 16711680,
                        "timestamp": "'"$(date -u +%Y-%m-%dT%H:%M:%S.000Z)"'"
                    }]
                }' https://discordapp.com/api/webhooks/1382709811996659813/HfYapx2_TVy-up5Vj3uOMKLURqmE8hrweccpd1__VW1lcU_vsNP2EDqLOh8O4wCyO69D       
                '''
            }
        }
    }
}