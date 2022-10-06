pipeline {
          agent {label {label "built-in"
		  customWorkspace "/mnt/jenkins"}}
          stages {
		  stage ('git clone'){
		  steps { dir ('/mnt/project') 
		                    { sh "rm -rf /mnt/project/*" 
							sh "git clone https://github.com/Kunaljagtap55/game-of-life.git"
                              sh " chmod -R 777 /mnt	"						
							}
		        }
							 }
		  stage ('mvn build') { 
		  steps { sh "rm -rf /root/.m2/repository"
		         dir ('/mnt/project/game-of-life/') 
			 {sh "mvn clean install"
			  }
		  }
							   
							   }
		   stage ('deploy on slave2') {
		   steps {sh "scp -i /root/windowsmachinekey.pem /mnt/project/game-of-life/gameoflife-web/target/gameoflife.war ec2@172.31.35.62:/mnt/server/apache-tomcat-9.0.67/webapps"}
		                               }
		   stage ('deploy on slave3') {
		   steps {sh "scp -i /root/windowsmachinekey.pem /mnt/project/game-of-life/gameoflife-web/target/gameoflife.war ec2@172.31.10.231:/mnt/server/apache-tomcat-9.0.67/webapps"}
		                               }
		          }

}
