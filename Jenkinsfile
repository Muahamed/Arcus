/**
 * This pipeline will run a Docker image build1
 */

podTemplate(label: 'docker',
  containers: [containerTemplate(name: 'docker', image: 'docker:1.11', ttyEnabled: true, command: 'cat'),
  containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.0', command: 'cat', ttyEnabled: true),],
  volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]
  ) {

  def image = "chinmaydc/weather-ui"
  node('docker') {
    stage('Build weather-ui') {
      git 'https://prasannachowdary12:prasanna123@prasannachowdary12@bitbucket.org/prasannachowdary12/weather-ui.git'
      container('docker') {
        sh "docker login -u chinmaydc -p Work42@ls"
        sh "docker build -t ${image}:${env.BUILD_NUMBER} ."
        sh "docker push ${image}:${env.BUILD_NUMBER} "
      }
      container('kubectl') {
           sh "kubectl get nodes"
           sh "kubectl create -f service.yaml"
           sh "kubectl create -f deployment.yaml"
   }
  }
 }
}

