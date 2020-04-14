pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps work too"
                    ls -lah
                    '''
            }

            withAWS(credentials:'aws-static', region:'us-west-2') {
                // upload index.html to s3 bucket
                s3Upload(file:'index.html', bucket:'bucketforudacitydevopsnanodegreejenkinsproject', path:'')
            }

        }
    }
}