pipeline {
	agent any
	stages {

		stage('Create kubernetes cluster') {
			steps {
				withAWS(region:'ap-south-1', credentials:'sbmvirdi') {
					sh '''
						eksctl create cluster \
						--name capstonecluster \
						--version 1.16 \
						--nodegroup-name standard-workers \
						--node-type t2.small \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto \
						--region ap-south-1 \
						--zones ap-south-1a \
						--zones ap-south-1b \
						--zones ap-south-1c \
					'''
				}
			}
		}

		

		stage('Create conf file cluster') {
			steps {
				withAWS(region:'ap-south-1', credentials:'sbmvirdi') {
					sh '''
						aws eks --region ap-south-1 update-kubeconfig --name capstonecluster
					'''
				}
			}
		}

	}
}
