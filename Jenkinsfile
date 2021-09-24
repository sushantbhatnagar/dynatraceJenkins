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
	createDynatraceDeploymentEvent(entityIds: [[$class: 'Service', entityId: 'SERVICE-C839DD873CDBD8A7']], envId: 'Dynatrace') {
    // some block
	
	tagMatchRules: [
				[
					meTypes: [[meType: 'SERVICE']],
					tags: [
					  [context: 'CONTEXTLESS', key: 'jenkins']
					]
				]
			]	  
		}
    }
 
 }