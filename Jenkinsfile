def NAME = '${NAME}'
def GIT_URL = '${GIT_URL}'
def GIT_REF = '${GIT_REF}'
def GIT_DIR = '${GIT_DIR}'

// this should be paramised
NAME = 'openshift-example'
GIT_URL = 'https://github.com/steven166/openshift-example.git'
GIT_REF = 'master'
GIT_DIR = '.'

node {
    stage('Checkout') {
        // Checkout repository
        checkout([
                $class                           : 'GitSCM',
                branches                         : [[name: GIT_REF]],
                doGenerateSubmoduleConfigurations: false,
                extensions                       : [],
                submoduleCfg                     : [],
                userRemoteConfigs                : [[url: GIT_URL]]])
    }
    stage('Build preparations') {
        try {
            // Delete old Build Config
            sh 'oc delete bc/' + NAME
        } catch (Exception e) {
        }
        // Create Build Config
        sh 'oc process -f build-config.yml -v NAME=' + NAME + ' -v TAG=dev -v GIT_URL=' + GIT_URL + ' -v GIT_REF=' + GIT_REF + ' -v GIT_DIR=' + GIT_DIR + ' | oc create -f -'
    }
    stage('Build') {
        // Start build and wait to finish it
        //sh 'oc start-build spring-boot-demo --wait --follow'
        openshiftBuild apiURL: '', authToken: '', bldCfg: NAME, buildName: '', checkForTriggeredDeployments: 'true', commitID: '', namespace: '', showBuildLogs: 'true', verbose: 'false', waitTime: '', waitUnit: 'sec'

    }
}