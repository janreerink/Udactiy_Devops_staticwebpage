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
        stage('UploadS3') {
            steps {
                withAWS(credentials:'aws-static', region:'us-west-2') {
                    // upload index.html to s3 bucket
                    s3Upload(bucket:'bucketforudacitydevopsnanodegreejenkinsproject', path:'', includePathPattern:'*.html')
                }
            }

        }
    }
}