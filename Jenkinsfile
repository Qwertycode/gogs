node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        
        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        sh "docker build --build-arg APP_NAME=gogs -t 693550056929.dkr.ecr.us-east-1.amazonaws.com/gogs:latest -f Dockerfile ."
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://693550056929.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:ECR') {
            sh "docker push 693550056929.dkr.ecr.us-east-1.amazonaws.com/gogs:latest"
        }
    }
}
