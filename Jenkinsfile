pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/khyati-source/Jenkins_pipeline_khyati.git'
        GIT_BRANCH = 'main'
        FILE_PATH = 'Jenkinsfile_assignment2/test.txt'
    }

    stages {
        stage('Checkout Repository') {
            steps {
                // Checkout the repository using Jenkins' default credentials
                git url: "${env.GIT_REPO}",
                    branch: "${env.GIT_BRANCH}",
                    credentialsId: 'my_github'  // Replace with your Jenkins GitHub credentials ID
            }
        }

        stage('Modify File') {
            steps {
                script {
                    sh """
                        mkdir -p Jenkinsfile_assignment2
                        rm -f Jenkinsfile_assignment2/test.txt
                        touch Jenkinsfile_assignment2/test.txt
                        echo 'Modified' >> Jenkinsfile_assignment2/test.txt
                    """
                }
            }
        }

        stage('Git Commit and Push') {
            steps {
                script {
                    // Commit and push using the default credentials (GitHub credentials in Jenkins)
                    sh '''
                        git config --global user.name "Jenkins User"
                        git config --global user.email "jenkins@yourcompany.com"
                        git add ${FILE_PATH}
                        git commit -m "Local change"
                        git push origin ${GIT_BRANCH}
                    '''
                }
            }
        }
    }
}
