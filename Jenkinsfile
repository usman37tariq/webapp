pipeline {

agent any
  stages{
stage('Checkout Source') {
steps {
git url:'https://github.com/usman37tariq/webapp.git', branch:'master'
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
 // sh 'ls ${WORKSPACE}'
sh 'cd C:\Windows\System32\config\systemprofile\AppData\Local\Jenkins\.jenkins\workspace\Demo2 && kubectl apply -f deploy.yaml'
}
}
}
}
