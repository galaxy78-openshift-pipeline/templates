## Manual Deploy on OpenShift
Create the following projects for CI/CD components, Dev and Stage environments:
 ```
  # Create Projects
  oc new-project bookstore-dev --display-name="Bookstore - Dev"
  oc new-project bookstore-stage --display-name="Bookstore - Stage"
  oc new-project cicd --display-name="cicd"

  # Grant Jenkins Access to Projects
  oc policy add-role-to-user edit system:serviceaccount:cicd:jenkins -n bookstore-dev
  oc policy add-role-to-user edit system:serviceaccount:cicd:jenkins -n bookstore-stage

  ```  
  
# Installation of templates

  ```
- oc new-app jenkins-persistent -p VOLUME_CAPACITY=100Gi -p MEMORY_LIMIT=8Gi
- oc new-app -f openshift-templates/nexus3-persistent-template.yaml --param=NEXUS_VERSION=latest
- oc new-app -f openshift-templates/sonarqube-template.yaml
  ```  
