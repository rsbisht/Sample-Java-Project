#!groovy

// node('Server_Group_1') {
   node {

    currentBuild.result = "SUCCESS"

    try {

            stage('Checkout'){

            env.NODE_ENV = "Checkout"
            print "[Stage] : ${env.NODE_ENV}"

            sh "echo                                                       > ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"
            sh "echo Checking out the code...                             >> ${env.JOB_NAME}.log"

            checkout scm
       }

       stage('Build'){

            env.NODE_ENV = "Build"
            print "[Stage] : ${env.NODE_ENV}"

   	    sh "echo                                                      >> ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"
 	    sh "echo Building the code...                                 >> ${env.JOB_NAME}.log"

            // sh 'export MAVEN_HOME=/opt/maven; cd ${WORKSPACE}; ${MAVEN_HOME}/bin/mvn clean install'

	    sh "javac SimpleForLoop.java"
	    sh "java SimpleForLoop                                        >> ${env.JOB_NAME}.log"
       }

       stage('Test'){

            env.NODE_ENV = "Test"
            print "[Stage] : ${env.NODE_ENV}"

   	    sh "echo                                                      >> ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"
 	    sh "echo Testing the code...                                  >> ${env.JOB_NAME}.log"

	    sh "javac SimpleForLoop.java                                  >> ${env.JOB_NAME}.log"
	    sh "ls -lrt ${WORKSPACE}                                      >> ${env.JOB_NAME}.log"
	    sh "java SimpleForLoop                                        >> ${env.JOB_NAME}.log"
       }

       stage('Deploy'){

            env.NODE_ENV = "Deploy"
            print "[Stage] : ${env.NODE_ENV}"

	    sh "echo                                                      >> ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"
	    sh "echo Deploying the code....                               >> ${env.JOB_NAME}.log"

            //  print "scp -r ${WORKSPACE}/Jenkinsfile root@15.213.52.106:/tmp"
	    //  sh "scp -r ${WORKSPACE}/Jenkinsfile root@15.213.52.106:/tmp"

	    sh "rm -f /tmp/Jenkinsfile; cp -r ${WORKSPACE}/Jenkinsfile /tmp"
	    sh "rm -f /tmp/SimpleForLoop.class; cp -r ${WORKSPACE}/SimpleForLoop.class /tmp"
       }

       stage('Notify'){

            env.NODE_ENV = "Notify"
            print "[Stage] : ${env.NODE_ENV}"

	    sh "echo                                                      >> ${env.JOB_NAME}.log"
            sh "echo [ Stage: ${env.NODE_ENV} ] :: Node: ${env.NODE_NAME} >> ${env.JOB_NAME}.log" 
	    sh "echo                                                      >> ${env.JOB_NAME}.log"
	    sh "echo Sending notification...                              >> ${env.JOB_NAME}.log"

	    mail    from: 'rsbisht@hpe.com',
                 replyTo: 'rsbisht@hpe.com',
                      to: 'rsbisht@hpe.com',
                 subject: "Jenkins:: Job Name: ${env.JOB_NAME} - Build#: ${env.BUILD_NUMBER} :: Status: ${currentBuild.result}",
	            body: "Project Build Successful. You can find the details here: ${env.BUILD_URL}"
       }
    }

    catch (err) {

        currentBuild.result = "FAILURE"

            mail    from: 'rsbisht@hpe.com',
                 replyTo: 'rsbisht@hpe.com',
                      to: 'rsbisht@hpe.com',
                 subject: "Jenkins:: Job Name: ${env.JOB_NAME} - Build#: ${env.BUILD_NUMBER} :: Status: ${currentBuild.result}",
	            body: "Project Build Failed ! You can find the error is here: ${env.BUILD_URL}" 

        throw err
    }
}
