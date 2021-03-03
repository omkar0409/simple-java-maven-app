#!groovy

def label = "jenkins-slave-${UUID.randomUUID().toString()}"


podTemplate(label: label, yaml: """
apiVersion: v1
kind: Pod
spec:
  securityContext:
    runAsUser: 1000
    serviceAccount: jenkins
  containers:
  - name: test-mvn
    image: maven:3.6.3-openjdk-17-slim
    command: ['cat']
    tty: true
    securityContext:
      runAsUser: 0
      privileged: true
      allowPrivilegeEscalation: true
    volumeMounts:
      - mountPath: /var/run/docker.sock
        name: docker-socket
  volumes:
    - name: docker-socket
      hostPath: 
        path: /var/run/docker.sock  
"""
  ) {
    node(label) {
      container('test-mvn') {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
  }
}    
