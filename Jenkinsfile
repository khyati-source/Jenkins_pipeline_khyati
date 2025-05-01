pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = credentials('my_github') // Jenkins Username+Password credential ID
    }

    stages {
        stage('Checkout Repository') {
            steps {
                git url: 'https://github.com/khyati-source/Jenkins_pipeline_khyati.git',
                    branch: 'main',
                    credentialsId: 'my_github'
            }
        }

        stage('Modify or Create File') {
            steps {
                sh '''
                    mkdir -p Jenkinsfile_assignment3
                    echo "Modified on $(date)" > Jenkinsfile_assignment3/test.txt
                '''
            }
        }

        stage('Git Commit and Push') {
            steps {
                sh '''
                    git config user.name "Jenkins User"
                    git config user.email "jenkins@yourcompany.com"
                    git pull origin main || echo "Nothing to pull"
                    git add Jenkinsfile_assignment3/test.txt || echo "Nothing to add"
                    git commit -m "Auto update on $(date)" || echo "Nothing to commit"
                    git push https://$GIT_CREDENTIALS@github.com/khyati-source/Jenkins_pipeline_khyati.git
                '''
            }
        }
    }
}
