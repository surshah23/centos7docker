node{
	stage ('Scm Checkout'){
	git credentialsId: 'github', url: 'https://github.com/anoopgawande/centos7docker.git'}

	stage ('Build Docker Image'){
	sh '/usr/bin/docker build -t agawande/httpd:latest .'}
	
	stage ('Push Docker Image'){
	withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerpwd', usernameVariable: 'dockeruser')]) {
    sh "/usr/bin/docker login -u $dockeruser -p $dockerpwd"}
	sh '/usr/bin/docker push agawande/httpd:latest'}
		stage('deploy k8s') {
    withCredentials([kubeconfigContent(credentialsId: '1k8s', variable: 'KUBECONFIG_CONTENT')]) {
    sh 'kubectl apply -f demo.yaml -n radicalcicd'
    }
  }
}
