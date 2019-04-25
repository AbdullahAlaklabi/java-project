properties([pipelineTriggers([githubPush()])])

node('linux') {
    stage('Unit Tests') {
      git 'https://github.com/AbdullahAlaklabi/java-project.git'
      sh 'ant -f test.xml -v'
      junit 'reports/result.xml'
    }
    stage('Build') {
      sh 'ant -f build.xml -v'
    }
    stage('Deploy'){
        sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://w10abdullah'
    }
    stage('Report'){
withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '463cedc0-1d92-4451-b996-05bca8c2f04e', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    // some block
sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
        }
}
}
