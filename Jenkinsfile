node {
    def app

    triggers {
        cron('H */1 * * 1-7')
    }

    stage('Clone Git repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        checkout scm
    }

    stage('Build Docker image') {
        /* This builds the actual image; synonymous to docker build on the command line */
        app = docker.build("netof/example-app")

    }

    stage('Push image') {
            /* Push the image into Docker Hub */
    		docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {

    			/* We'll push the image with two tags:
    	         * First, the branch name and the latest tag
    	         * Second, the branch name and the incremental build number
    	         * Pushing multiple tags is cheap, as all the layers are reused. */

    			app.push("${env.BRANCH_NAME}-latest")
    			app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
    		}
    	}
}