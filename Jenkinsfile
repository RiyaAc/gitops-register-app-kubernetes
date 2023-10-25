pipeline {
    agent { label 'node-1' }
    environment {
        APP_NAME = "register-app-pipeline"
        IMAGE_TAG = "your_image_tag_here"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/RiyaAc/gitops-register-app-kubernetes'
            }
        }

        stage("Update the Deployment Tags") {
            steps {
                sh """
                   cat deployment.yaml
                   sed -i 's/\${APP_NAME}.*/\${APP_NAME}:\${IMAGE_TAG}/g' deployment.yaml
                   cat deployment.yaml
                """
            }
        }

        // You can uncomment and modify the following stage if you want to push changes to Git.
        // stage("Push the changed deployment file to Git") {
        //     steps {
        //         sh """
        //            git config --global user.name "RiyaAc"
        //            git config --global user.email "riyaachkarpohre32@gmail.com"
        //            git add deployment.yaml
        //            git commit -m "Updated Deployment Manifest"
        //         """
        //         withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
        //             sh "git push https://github.com/RiyaAc/gitops-register-app-kubernetes main"
        //         }
        //     }
        // }
    }
}
