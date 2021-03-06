pipeline {
    agent any
    environment {
        GIT_LATEST_COMMIT_EDITOR= sh(
            returnStdout:true,
            script: 'git show -s --pretty=%cn '
        ).trim()
        GIT_SSH_URL = sh(
            returnStdout: true,
            script: "git config --get remote.origin.url | sed 's/https:\\/\\/github.com\\//git@github.com:/g'"
        )
        GIT_CURRENT_BRANCH = sh(
            returnStdout: true,
            script: "git rev-parse --abbrev-ref HEAD"
        )
        HOME = '.'
    registry = "charf551/goforwork"
    registryCredential = 'dockerhub'
    dockerImage = ''
	  }

    stages {
        stage ('Show commit author') {
            steps {
                sh "echo '${env.GIT_LATEST_COMMIT_EDITOR}'"
            }
        }
        stage ('Build angular pipeline') {
            steps {
               script { 
                    dockerImage = docker.build(registry + ":Angular V"+"$BUILD_NUMBER","./angular-app/") 
                    docker.withRegistry( '', registryCredential ) { 
                    dockerImage.push() 
                    }
                }

            }
        }
        stage ('Build express-server pipeline') {
            steps {
                script { 
                    dockerImage = docker.build(registry +":Express V"+ "$BUILD_NUMBER","./express-server/") 
                    docker.withRegistry( '', registryCredential ) { 
                    dockerImage.push() 
                    }
                }
            }
        }
                
    }
}