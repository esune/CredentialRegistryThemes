node { 
  load 'pipeline/config.groovy'  

  stage('Checkout Source') {
    echo "Checking out source code ..."
    // Check out ToB repo, so that we can access the pipeline definition
    checkout([
      $class: 'GitSCM',
      branches: [[name: "*/${TOB_SOURCE_REPO_BRANCH}"]],
      extensions: [
        [$class: 'RelativeTargetDirectory', relativeTargetDir: 'pipeline-conf']
      ],
      userRemoteConfigs: [[url: "${TOB_SOURCE_REPO}"]]
    ])
  }

  // load and run closure from pipeline file
  node {
    load 'pipeline-conf/pipeline/pipeline.groovy'
  }()
}
