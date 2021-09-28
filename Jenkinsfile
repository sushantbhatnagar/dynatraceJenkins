node {
   
   stage('Staging') {
     checkout scm
     sh "git rev-parse --short HEAD > .git/commit-id"                        
     commit_id = readFile('.git/commit-id').trim()
   }
   
   stage('Test') {
	echo "Test in-progress"
   }
   
   stage('createDynatraceDeploymentEvent') {  
	
	 createDynatraceDeploymentEvent(envId: 'Dynatrace', tagMatchRules: [[meTypes: [[meType: 'SERVICE']], tags: [[context: 'CONTEXTLESS', key: 'jenkins']]]]) {
                    echo 'Testing Pass'
                }	
	}
	
	stage('recordDynatraceDeploymentEvent') {
	recordDynatraceSession(entityIds: [[$class: 'Service', entityId: 'SERVICE-C839DD873CDBD8A7']], envId: 'Dynatrace', testCase: 'testDynatrace') {
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
	
	stage('PerformanceSignatureReports') {
		perfSigDynatraceReports envId: 'Dynatrace', nonFunctionalFailure: 2, specFile: 'specfile.json'
	} 
 }
