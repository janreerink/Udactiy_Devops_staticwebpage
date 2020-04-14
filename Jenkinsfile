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
        }
        stage('UploadS3') {
            steps {
                withAWS(credentials:'aws-static', region:'us-west-2') {
                    // upload index.html to s3 bucket
                    s3Upload(file:'index.html', pathStyleAccessEnabled:true, payloadSigningEnabled: true, bucket:'bucketforudacitydevopsnanodegreejenkinsproject', path:'')
                }
            }
        }
        
    }
}