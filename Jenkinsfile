pipeline {
  agent any
environment {
    // SEMGREP_RULES = "p/security-audit p/secrets" // more at semgrep.dev/explore
      SEMGREP_BASELINE_REF = "origin/${env.CHANGE_TARGET}"
    // == Optional settings in the `environment {}` block
    // Instead of `SEMGREP_RULES:`, use rules set in Semgrep App.
    // Get your token from semgrep.dev/manage/settings.
      SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
      SEMGREP_REPO_URL = env.GIT_URL.replaceFirst(/^(.*).git$/,'$1')
      SEMGREP_BRANCH = "${GIT_BRANCH}"
      SEMGREP_JOB_URL = "${BUILD_URL}"
      SEMGREP_REPO_NAME = env.GIT_URL.replaceFirst(/^https:\/\/github.com\/(.*).git$/, '$1')
      SEMGREP_COMMIT = "${GIT_COMMIT}"
      SEMGREP_PR_ID = "${env.CHANGE_ID}"
    // Never fail the build due to findings.
    // Instead, just collect findings for semgrep.dev/manage/findings
    //   SEMGREP_AUDIT_ON = "unknown"
    // Change job timeout (default is 1800 seconds; set to 0 to disable)
    //   SEMGREP_TIMEOUT = "300"
  }
  stages {
    stage('Semgrep-Scan') {
        steps {
            sh 'echo $SEMGREP_APP_TOKEN'
            sh 'echo $SEMGREP_REPO_URL'
            sh 'echo $SEMGREP_REPO_NAME'
            sh 'echo $SEMGREP_BRANCH'
            sh 'echo $SEMGREP_COMMIT'
            sh 'echo $SEMGREP_BASELINE_REF'
            sh 'ls -la'
            sh 'pip3 install semgrep==0.86.5'
            //sh 'pip3 install semgrep-agent'
            //sh 'semgrep-agent --publish-token $SEMGREP_APP_TOKEN'
            //sh 'semgrep ci --baseline-ref $SEMGREP_BASELINE_REF'
            sh 'semgrep ci --baseline-commit $SEMGREP_BASELINE_REF'
            //sh 'git status'
            //sh 'git show $SEMGREP_BASELINE_REF'
            //sh 'git diff 310b06418f7006ae7d5dd03417127b88070ffcd1'
        }
    }
  }
}
