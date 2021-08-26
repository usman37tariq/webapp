pipeline {

agent any
  stages{
stage('Checkout Source') {
steps {
git url:'https://github.com/usman37tariq/-hellowhale.git', branch:'master'
}
}
stage("Build image") {
steps {
script {
myapp = docker.build("usmantariq37/hellowhale:${env.BUILD_ID}")
}
}
}
stage("Push image") {
steps {
script {
docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
myapp.push("latest")
myapp.push("${env.BUILD_ID}")
}
}
}
}
stage('Deploy to Cluster') {
steps {
sh 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl apply -f -'
}
}
}
}
