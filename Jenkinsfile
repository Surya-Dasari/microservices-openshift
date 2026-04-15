pipeline {
    agent any

    stages {
        stage('Deploy To OpenShift') {
            steps {
                withCredentials([string(credentialsId: 'openshift-token', variable: 'TOKEN')]) {
                    sh '''
                    oc login https://api.rm2.thpm.p1.openshiftapps.com:6443 \
                    --token=$TOKEN \
                    --insecure-skip-tls-verify=true

                    oc project suryadasari31-dev

                    oc apply -f deployment-service.yml
                    '''
                }
            }
        }
        
        stage('verify Deployment') {
            steps {
                withCredentials([string(credentialsId: 'openshift-token', variable: 'TOKEN')]) {
                    sh '''
                    oc login https://api.rm2.thpm.p1.openshiftapps.com:6443 \
                    --token=$TOKEN \
                    --insecure-skip-tls-verify=true

                    oc project suryadasari31-dev

                    oc get pods
                    oc get svc
                    oc get route
                    '''
                }
            }
        }
    }
}
