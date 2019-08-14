node {
    def app
    stage('Clone Git repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        checkout scm
    }

    stage('Build Docker image') {
        /* This builds the actual image; synonymous to docker build on the command line */
        app = docker.build("netof/example-app")

    }

    stage('Push image') {
        /* Finally, we'll push the image into Docker Hub */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("latest")
        }
    }
}