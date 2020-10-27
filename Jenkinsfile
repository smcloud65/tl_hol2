node {
    stage('createImage') {
        sh 'echo "Creating Dockerfile..."'
        sh 'echo "FROM ubuntu:latest" > Dockerfile'
        sh 'echo "ENV MYSQL_HOST=DB_Server" >> Dockerfile'
        sh 'echo "ENV MYSQL_PASSWORD=5TTnvuTDJJSq6" >> Dockerfile'
        sh 'echo "LABEL description=Test_Twistlock_Jenkins_Plugin" >> Dockerfile'
        sh 'docker build --no-cache -t dev/my-i:$BUILD_NUMBER .'
    }
    stage('twistlockScan') {
        prismaCloudScanImage ca: '', cert: '', dockerAddress: 'unix:///var/run/docker.sock', image: 'dev/my-i:$BUILD_NUMBER', key: '', logLevel: 'info', podmanPath: '', project: '', resultsFile: 'prisma-cloud-scan-results.json', ignoreImageBuildTime:true
    }
    stage('twistlockPublish') {
        prismaCloudPublish resultsFilePattern: 'prisma-cloud-scan-results.json'
    }
}
