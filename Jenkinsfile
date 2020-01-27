
node() {
    def app
    stage('Clone repository') { /* Let's make sure we have the
        repository cloned to our workspace */
        checkout scm
    }
    stage('Build image') { /* This builds the actual image; synonymous to *
        docker build on the command line */
            docker.withServer('tcp://52.91.231.138:2375') {
        docker.withRegistry("https://693550056929.dkr.ecr.us-east-1.amazonaws.com", "ecr:us-east-1:ECR") {
            app = docker.build("gogs:${env.BUILD_ID}")
        }
            }
    }

    stage('Push image') { /* This pushes image to ECR registry; synonymous to
        * docker push on the command line */
            docker.withServer('tcp://52.91.231.138:2375') {
        docker.withRegistry("https://693550056929.dkr.ecr.us-east-1.amazonaws.com", "ecr:us-east-1:ECR") {
            app.push()
            app.push('latest')
        }
            }
    }
}
