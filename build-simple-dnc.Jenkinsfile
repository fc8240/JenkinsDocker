def dockerImage;

node('docker-ex'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/fc8240/JenkinsDocker']]]);
	}
	stage('build'){
		docker.withRegistry('https://index.docker.io/v1/', 'dockerhubcreds'){
			sh 'docker buildx create --name cbbspace' 
			sh 'docker buildx use cbbspace'
			sh 'docker buildx build -t fc8240/simplednc:jenkinsfile --platform=linux/amd64,linux/arm/v7 - < dncgit.Dockerfile --push'
		}
	}
}