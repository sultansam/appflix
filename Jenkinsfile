def secret = 'server'
def server = 'ubuntu@192.168.100.71'
def directory = 'appflix-front'
def branch = 'master'

pipeline{
	agent any
	stages{
	   stage ('mengosongkan'){
		steps{
			   sshagent([secret]) {
				   sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
					cd ${directory}
					docker-compose down
					docker system prune -f
					git pull origin ${branch}
					exit
					EOF"""
				}
          		  }
      		 }
		
		stage ('membangun'){
			steps{
				sshagent([secret]) {
				sh """ssh -o StrictHostkeyChecking=no ${server} << EOF
				cd ${directory}
				docker-compose build
				exit
				EOF"""
		 		}
			}
		}
		stage ('meluncurkan'){
           		steps{
		 		sshagent([secret]) {
			 	sh """ssh -o StrictHostkeyChecking=no ${server} << EOF
				cd ${directory}
				docker-compose up -d
				exit
				EOF"""
	     		}
         	}
     	}
   }
}
