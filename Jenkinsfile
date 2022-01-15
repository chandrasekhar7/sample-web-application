pipeline{

      agent {
                docker {
                image 'maven:3-openjdk-11'

                }
            }
        
        stages{

              stage('Quality Gate Status Check'){
                  steps{
                      script{
			      withSonarQubeEnv('http://34.125.97.214:9000') { 
			      sh "mvn clean sonar:sonar"
                       	     	}
			      timeout(time: 1, unit: 'HOURS') {
			      def qg = waitForQualityGate()
				      if (qg.status != 'OK') {
					   error "Pipeline aborted due to quality gate failure: ${qg.status}"
				      }
                    		}
		    	    sh "mvn clean install"
		  
                 	}
               	 }  
              }	
		
            }	       	     	         
}
