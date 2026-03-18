pipeline {
 agent { label 'build' }
 parameters {
     password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Gitlab password')
     string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
     choice(name:'environment', choices: ['functional', 'integration', 'regression', 'uat', 'release' ] ,description: 'select where need to deploy')
 }
 stages {
  stage('Deploy')
  {
    steps { 
        git branch: 'springboot', credentialsId: 'Gitlabcred', url: 'https://gitlab.com/Dikshaturkar10/spingboot-cd-pipeline.git'
      dir ("./${params.environment}") {
              sh "sed -i 's|image: .*|image: dikshat1024/democicd:${IMAGETAG}|g' deployment.yml" 
	    }
       sh 'git add .'
	   sh """
        git commit -a -m "New deployment for Build ${IMAGETAG}" || echo "No changes"
        """
	    sh "git push https://Dikshaturkar10:$PASSWD@gitlab.com/Dikshaturkar10/spingboot-cd-pipeline.git"
    }
  }
 }
}
