# docker-kong

curl -sSv -X POST -H 'Content-type: application/json' master.mesos:8080/v2/apps -d '
{
  "id": "kong-2",
  "instances": 1,
  "cpus": 0.5,
  "mem": 1024,
  "container": {
    "type": "DOCKER",
    "docker": {
      "network": "BRIDGE",
      "image": "mashape/kong:0.5.4",
      "portMappings": [
        {
          "containerPort": 8000,
          "hostPort": 8000
        },
        {
          "containerPort": 8001,
          "hostPort": 8001
        }
      ]
    },
    "volumes": [
      {
        "containerPath": "/etc/kong/kong.yml",
        "hostPath": "./kong.yml",
        "mode": "RO"
      }
    ]
  },
  "uris": [
    "https://raw.githubusercontent.com/tony-kerz/docker-kong/master/kong.yml"
  ],
  "healthChecks": [
    {
      "protocol": "TCP"
    }
  ],
  "constraints": [
    ["hostname", "CLUSTER", "ip-10-0-1-80.ec2.internal"]
  ]
}
'
```
