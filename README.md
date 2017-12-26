### `npm start`

Runs the app in the development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br>
You will also see any lint errors in the console.

### `npm run build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!

{
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
}
