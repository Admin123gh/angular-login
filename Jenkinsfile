node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("xavics/angular-login")
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('http://52.19.183.165:5000', 'docker-registry-credentials') {
            sh 'docker tag xavics/angular-login 52.19.183.165:5000/xavics/angular-login:latest'
            sh 'docker push 52.19.183.165:5000/xavics/angular-login:latest'
        }
    }

}