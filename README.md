# docker-kubectl
Docker image containing bash, kubectl, and gettext

![Docker Pulls](https://img.shields.io/docker/pulls/seancallaway/kubectl)

A simple Docker image containing kubectl and the gettext package.

## Usage example

This is intended to be used in a CI/CD pipeline. 

It can be used in a GitLab CI pipeline, like:

```yaml
deploy_dev:
  image:
    name: seancallaway/kubectl
  stage: deploy
  variables:
    MY_NAMESPACE: staging
  before_script:
    - cd k8s
  script:
    - envsubst < env_configmap.yaml > staging_env_configmap.yaml
    - envsubst < secrets.yaml > staging_secrets.yaml
    - envsubst < ingress.yaml > staging_ingress.yaml
    - envsubst < deployment.yaml > staging_deployment.yaml
    - kubectl apply -n ${MY_NAMESPACE} -f staging_env_configmap.yaml
    - kubectl apply -n ${MY_NAMESPACE} -f nginx_configmap.yaml
    - kubectl apply -n ${MY_NAMESPACE} -f staging_secrets.yaml
    - kubectl apply -n ${MY_NAMESPACE} -f staging_deployment.yaml
    - kubectl apply -n ${MY_NAMESPACE} -f service.yaml
    - kubectl apply -n ${MY_NAMESPACE} -f staging_ingress.yaml
  only:
    - development
```


## Meta

Sean Callaway – [@smcallaway](https://twitter.com/smcallaway)

Distributed under the GPLv3 license. See ``LICENSE`` for more information.

[https://github.com/seancallaway/docker-kubectl](https://github.com/seancallaway/docker-kubectl)

## Contributing

1. Fork it (<https://github.com/seancallaway/docker-kubectl/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request
