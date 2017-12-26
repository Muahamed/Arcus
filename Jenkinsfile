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
           sh "ls -ltr"
           sh "pwd"
           sh "echo "{
  "apiVersion": "extensions/v1beta1",
  "kind": "Deployment",
  "metadata": {
    "creationTimestamp": null,
    "labels": {
      "app": "weather-ui",
      "name": "weather-ui",
      "type": "web"
    },
    "name": "weather-ui"
  },
  "spec": {
    "replicas": 2,
    "selector": {
      "matchLabels": {
        "app": "weather-ui",
        "name": "weather-ui",
        "type": "web"
      }
    },
    "strategy": {
      "rollingUpdate": {
        "maxSurge": 1,
        "maxUnavailable": 1
      },
      "type": "RollingUpdate"
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "weather-ui",
          "name": "weather-ui",
          "type": "web"
        },
        "name": "weather-ui"
      },
      "spec": {
        "containers": [
          {
            "image": "chinmaydc/weather-ui",
            "imagePullPolicy": "IfNotPresent",
            "name": "weather-ui",
            "ports": [
              {
                "containerPort": 5000
              }
            ]
          }
        ],
        "dnsPolicy": "ClusterFirst",
        "restartPolicy": "Always",
        "securityContext": {},
        "terminationGracePeriodSeconds": 30
      }
    }
  }
} " > deploy.json "
           sh "kubectl create -f deploy.json"
   }
  }
 }
}

