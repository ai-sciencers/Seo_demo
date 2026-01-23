@Library("shared") _
pipeline {
    agent any
  stages {
        stage('Hello') {
            steps {
                script {
                    
                    hello()
                }
            }
        }
        
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ai-sciencers/Seo_demo.git', branch: 'master'
            }
        }

        stage('List Files') {
            steps {
                echo "Listing project files"
                sh 'ls -R .'
            }
        }

        stage('Validate HTML') {
            steps {
                echo "Validating HTML files"
                sh '''
                for f in *.html; do
                  echo "Checking $f"
                  html-hint $f || true
                done
                '''
            }
        }

        stage('Deploy (Optional)') {
            steps {
                echo "Deploying static site"
                sh 'nohup python3 -m http.server 8080 &'
                echo "Site should be served on port 8080"
            }
        }
    }
}
