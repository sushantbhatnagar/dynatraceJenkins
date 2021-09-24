node {
   
   stage('Staging') {
     checkout scm
     sh "git rev-parse --short HEAD > .git/commit-id"                        
     commit_id = readFile('.git/commit-id').trim()
   }
   
   stage('Test') {
	echo "Test Pass"
   }
   
   stage('createDynatraceDeploymentEvent') {   
	steps {
		createDynatraceDeploymentEvent(
			envId: '5c27ebbb-fd99-4f71-a1b8-f67bc33efa9f',
			"ciBackLink":"${BUILD_URL}",
			tagMatchRules: [
				[
					meTypes: [[meType: 'SERVICE']],
					tags: [
					  [context: 'CONTEXTLESS', key: 'jenkins']
					]
				]	  
		])
     }
   }
 
 }