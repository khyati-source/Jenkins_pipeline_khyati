pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = credentials('my_github') // Combines username and token
    }

    stages {
        stage('Checkout Repository') {
            steps {
                git url: 'https://github.com/khyati-source/Jenkins_pipeline_khyati.git',
                    branch: 'main',
                    credentialsId: 'my_github'
            }
        }

        stage('Modify File') {
            steps {
                sh '''
                    mkdir -p Jenkinsfile_assignment2
                    echo "Modified on $(date)" > Jenkinsfile_assignment2/test.txt
                '''
            }
        }

        stage('Git Commit and Push') {
            steps {
                sh '''
                    git config --global user.name "Jenkins User"
                    git config --global user.email "jenkins@yourcompany.com"
                    git add Jenkinsfile_assignment2/test.txt || echo "No changes to add"
                    git commit -m "Auto update on $(date)" || echo "No commit needed"
                    git push https://$GIT_CREDENTIALS@github.com/khyati-source/Jenkins_pipeline_khyati.git
                '''
            }
        }
    }
}
