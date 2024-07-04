pipeline {
    agent {
        label 'general'
    }

    parameters {
        string(name: 'SERVICE_NAME', defaultValue: '', description: '')
        string(name: 'IMAGE_FULL_NAME_PARAM', defaultValue: '', description: '')
    }

    stages {
        stage('Deploy') {
            steps {
                /*
                Now your turn! implement the pipeline steps ...

                - `cd` into the directory corresponding to the SERVICE_NAME variable.
                - Change the YAML manifests according to the new $IMAGE_FULL_NAME_PARAM parameter.
                  You can do so using `yq` or `sed` command, by a simple Python script, or any other method.
                - Commit the changes, push them to GitHub.
                   * Setting global Git user.name and user.email in 'Manage Jenkins > System' is recommended.
                   * Setting Shell executable to `/bin/bash` in 'Manage Jenkins > System' is recommended.
                */
                sh """
                   cd k8s/$SERVICE_NAME
                   sed -i 's|image: .*|image: ${IMAGE_FULL_NAME_PARAM}|' deployment.yaml
                """
                withCredentials([usernamePassword(credentialsId: 'github', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh """
                        cd k8s/${SERVICE_NAME}
                        git config --global user.name "MohammadKhGh99"
                        git config --global user.email "mohammad.gh454@gmail.com"
                        git add deployment.yaml
                        git commit -m 'Update image to ${IMAGE_FULL_NAME_PARAM}'
                        git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/MohammadKhGh99/NetflixInfra.git HEAD:main
                    """
                }
            }
        }
    }
}