pipeline {
    agent any

    environment {
        // Fetch the GitHub username and token stored in Jenkins credentials
        GITHUB_USER = credentials('khyati-source')  // The ID of the credential storing your GitHub username
        GITHUB_TOKEN = credentials('my_github')    // The ID of the credential storing your GitHub token
    }

   stages {
        stage('Checkout Repository') {
            steps {
                git url: 'https://github.com/khyati-source/Jenkins_pipeline_khyati.git',
                    branch: 'main',
                    credentialsId: 'my_github'  // Use credentials stored in Jenkins for Git operations
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
                        cat Jenkinsfile_assignment2/test.txt  # Verify the file content
                    """
                }
            }
        }

       stage('Git Commit and Push') {
            steps {
                script {
                    sh '''
                        git config --global user.name "Jenkins User"
                        git config --global user.email "jenkins@yourcompany.com"
                        git add Jenkinsfile_assignment2/test.txt
                        git commit -m "Local change"
                        git status  # Verify file is staged for commit
                        git log -n 1  # Check the latest commit to confirm commit was successful
                        
                        # Push using credentials passed in environment variables
                        git push https://${GITHUB_USER}:${GITHUB_TOKEN}@github.com/khyati-source/Jenkins_pipeline_khyati.git
                    '''
                }
            }
        }
    }
}
