pipeline {
    agent {
  label 'slaves'
}

    stages {
        stage('Build') {
            steps {
                // Checkout the source code
                git branch: 'master', url: 'https://github.com/shekar55/nodejs-app-mss1.git'

                // Install dependencies
                sh 'npm install'

                // Build the app
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                sh 'npm test'
            }
        }
      
         stage('executesonarqubereport') {
             steps  {
                // Run tests
                nodejs(nodeJSInstallationName: 'nodejs18.6.0'){
                sh "npm run sonar"
            }
        }  
         }
        stage('Deploy') {
            steps {
                // Deploy to production server
                sshagent(['my-ssh-key']) {
                    sh 'ssh user@production-server "cd /var/www/my-nodejs-app && git pull && npm install && pm2 restart index.js"'
                }
            }
        }
    }
}
}
