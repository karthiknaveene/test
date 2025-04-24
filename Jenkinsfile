pipeline {
    agent any

    // Enable both polling and webhook triggers
    triggers {
        pollSCM('* * * * *')      // Every 5 minutes
        githubPush()                // GitHub webhook
    }

    stages {
        stage('Detect Trigger') {
            steps {
                script {
                    def causeText = ''
                    def causes = currentBuild.rawBuild.getCauses()

                    for (c in causes) {
                        causeText += "Cause: ${c.shortDescription}\n"
                    }

                    echo "Build Causes:\n${causeText}"
                }
            }
        }

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Running build tasks..."
                sh 'git log -1 --oneline'
            }
        }
    }
}
