node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        
        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */        
        docker.withRegistry("https://693550056929.dkr.ecr.us-east-1.amazonaws.com", "ecr:us-east-1:ECR") {
            def customImage = docker.build("my-image:${env.BUILD_ID}")
            customImage.push()
            customImage.push('latest')
        }
    }
}
