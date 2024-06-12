###############################################################################################################################################################################

                                                                            -----   Project-4  -------(Completed)
                                                                          ----swiggy-nodejs-devops-project------  

###############################################################################################################################################################################

-->Create a t2.medium instance and the run these cmds
-->sudo yum install git -y
-->sudo yum install docker -y
-->sudo systemctl start docker
-->sudo systemctl enable docker
-->sudo chmod 666 /var/run/docker.sock
-->sudo usermod -a -G docker ec2-user
-->sudo dnf install java-11-amazon-corretto -y
-->sudo dnf install java-17-amazon-corretto -y

-->sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
   sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
   sudo yum install jenkins -y
   sudo systemctl enable jenkins
   sudo systemctl start jenkins
-->Now to Setup Kubernetes on Amazon EKS
   -->1. Setup kubectl
      2. Setup eksctl 
      3. Create an IAM Role and attache it to EC2 instance
      4. Create your cluster and nodes
-->curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
-->chmod +x ./kubectl 
-->sudo mv ./kubectl /usr/local/bin/kubectl
-->Now as already kubectl is already set and we will attach a admin iam role to the instance for now
-->After attaching the role now we should set up eksctl
-->sudo su -
-->curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
-->sudo mv /tmp/eksctl /usr/local/bin
-->eksctl create cluster --name jack   --region us-east-1   --node-type t2.small

-->give  ec2_IP:8080 to access jenkins
-->sudo cat /var/lib/jenkins/secrets/initialAdminPassword
   -->a5036075f0a04d59b3ca5d492266765d

-->Now select install the suggested plugins.

-->Jenkins will now get installed and install all the libraries -> Create an admin user with all username,password,full name with praneeth9630

-->Click on save and continue -> It will take us to Jenkins Dashboard

-->Go to Manage Jenkins → Tools → add java path→ Click on Apply and Save
   -->Use the latest version of Docker

-->Go to Jenkins dashboard -> Manage Jenkins –> Plugins –> Available Plugins -> Search for the Below Plugins and install them -> Go back to the top page
   -->DockerVersion 1.6
      Docker CommonsVersion 439.va_3cb_0a_6a_fb_29
      Docker PipelineVersion 572.v950f58993843
      Docker APIVersion 3.3.4-86.v39b_a_5ede342c
      docker-build-stepVersion 2.11

-->Now add Docker credentials to the Jenkins to log in and push the image -> Manage Jenkins –> Credentials –> global –> add credential 
   -> give kind as username with password and Add DockerHub Username and Password under Global Credentials, id as docker -> click on Create.

-->Now Give this command in CLI
   -->sudo cat /home/ec2-user/.kube/config
      -->
   -->cat /root/.kube/config
      -->
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURCVENDQWUyZ0F3SUJBZ0lJRGdwVGorY3k2NlV3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TkRBMU1Ea3dOVEExTkRoYUZ3MHpOREExTURjd05URXdORGhhTUJVeApFekFSQmdOVkJBTVRDbXQxWW1WeWJtVjBaWE13Z2dFaU1BMEdDU3FHU0liM0RRRUJBUVVBQTRJQkR3QXdnZ0VLCkFvSUJBUURZSjFwZ1FzcDR2bTMxK0tYUERJOElJL2dWZURrUUk4QityWWpkckEveS9wS1NmREM4RjNxYkJNVm8KUk94b3E4S0toVXdnc0xxYWRaYUNPMkxncDVnSk80OU1USWtucWZNUmlxRVp5eE1QaDV1Y0tKTzJRNUdBSEJmRwoyeVdla3FXZ3I3UWkzdE5BdUcwWStvTDg5WS9SOXlpeUsvbGkzeUp4MUsxU0JlcGRaTmVIMHlwMXJCa3hOSXVLCnlGOUtXUmc2Rk1TTnNJV29xd3p3NFU2SUExalMrMkJqSkVsUXVxK25tOXBqc1lKQ09VS1lkS1R4LzBYMENRV0YKc0dheFNFNGViOWk5TjVQZWRHY2RvQUhWS25WNjFPeXFERmczbU9EaEVpN0dNMWVOSDlCVDZqWUh4UTJOa1hXaQpxSFBiQWp5Y25QV3IxRmRqNWpibmNwMUUvcXZQQWdNQkFBR2pXVEJYTUE0R0ExVWREd0VCL3dRRUF3SUNwREFQCkJnTlZIUk1CQWY4RUJUQURBUUgvTUIwR0ExVWREZ1FXQkJRUGFYd0FiQXVKZ0NwbUs5UHBldW1sSnZJMHdqQVYKQmdOVkhSRUVEakFNZ2dwcmRXSmxjbTVsZEdWek1BMEdDU3FHU0liM0RRRUJDd1VBQTRJQkFRQjk3QmtZb2puOQpBVTVsM1EvUGhqSnQrdzBQZHBFSUFFM29oZEMyU3dFb2s5VmxubW5kVXJ3VisvaW9zYlUzVGlYMHI0Z2h2WWRwCjJTMzBZc2NUdE13dGlMQ0ZFYzFuQTZrQUsrczZtc3BYemJDSllZREVtM0xJRjVONW5ReElsTDltRHk5aGpHNVEKRndGVVBqY0d3MEhLclhOT2JjUElUQlF5MFNpUU1XZGlEbVV0aktBTTc1WllnOFozTTFHTVFOTVhqODJYdmlKeQp1OVdBRERHZGdFSDV4b3d6bDFqMTRhS3oyNXZjN3R5Vm1vNmlnZnZxVHVxTmx1M0RJUEI5dzZRS1BCSkh5ZjVUCnBMZnZBSXJwc01Qa3FFbVhVNG4yOFhEbytFNHJ2b2UxclZpdWxBRVdEQ2lQNURvT2lLai96QmdtTG9UYnE4azgKQUpVWnBVVkVya0hSCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: https://2A07C7BD1B5CCA612C60ECBE17BEEA17.gr7.ap-south-1.eks.amazonaws.com
  name: jack.ap-south-1.eksctl.io
contexts:
- context:
    cluster: jack.ap-south-1.eksctl.io
    user: i-0ce1a06c6fee516cd@jack.ap-south-1.eksctl.io
  name: i-0ce1a06c6fee516cd@jack.ap-south-1.eksctl.io
current-context: i-0ce1a06c6fee516cd@jack.ap-south-1.eksctl.io
kind: Config
preferences: {}
users:
- name: i-0ce1a06c6fee516cd@jack.ap-south-1.eksctl.io
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1beta1
      args:
      - eks
      - get-token
      - --output
      - json
      - --cluster-name
      - jack
      - --region
      - ap-south-1
      command: aws
 
-->copy content from api version  -- to   --command aws
   Copy the config file to Jenkins master or the local file manager and save it

-->copy it and save it in documents or another folder save it as secret-file.txt
   Note: create a secret-file.txt in your file explorer save the config in it and use this at the kubernetes credential section.

-->Install Kubernetes Plugin to give the saved file
   -->Kubernetes Client APIVersion 6.10.0-240.v57880ce8b_0b_2
   -->Kubernetes CredentialsVersion 0.11
   -->KubernetesVersion 4214.vf10083a_42e70
   -->Kubernetes CLIVersion 1.12.1

-->Now in jenkins -> credentials -> system -> global credentials -> add credentials -> give kind as secret file ->  id as k8s -> create
-->
   -->
pipeline {
    agent any

    stages {
        stage('Cloning') {
            steps {
                sh "git clone https://github.com/Praneeth9630/Project-4-swiggy-nodejs-devops.git"
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                    dir('Project-4-swiggy-nodejs-devops') {
                        withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                            sh "docker build -t swiggy_1 ."
                            sh "docker tag swiggy_1 praneeth9630/swiggy_1:latest"
                            sh "docker push praneeth9630/swiggy_1:latest"
                        }
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    dir('Project-4-swiggy-nodejs-devops/Kubernetes') {
                        withKubeConfig(caCertificate: '', clusterName: '', contextName: '', credentialsId: 'k8s', namespace: '', restrictKubeConfigAccess: false, serverUrl: '') {
                            sh 'aws eks update-kubeconfig --name jack --region us-east-1'
                            sh 'kubectl apply -f deployment.yml'
                            sh 'kubectl apply -f service.yml'
                        }
                    }
                }
            }
        }
    }
}


-->Apply and save -> build -> 
-->

-->eksctl delete cluster jack  --region us-east-1
