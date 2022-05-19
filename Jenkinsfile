pipeline {
    agent { 
        label 'msvc20'
    }
    stages {
       stage('Prepare workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout 3dmmForever repo'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/foone/3DMMForever.git']]])
            }
        }
        stage('build') {
            environment{
                Path = "${MSVCNT_ROOT}\\bin;${PATH}"
                LIB ="${MSVCNT_ROOT}\\lib"
                SOC_ROOT = "${WORKSPACE}"
                KAUAI_ROOT = "${SOC_ROOT}\\kauai"
                INCLUDE ="${MSVCNT_ROOT}\\INCLUDE;${SOC_ROOT}\\INC;${SOC_ROOT}\\BREN\\INC;${KAUAI_ROOT}\\SRC;${SOC_ROOT}\\SRC"
                PROJ='SOC'
                ARCH='WIN'
                TYPE='DBSHIP'
                CHIP='IN_80386'
            }
            steps {
                bat '''cd %KAUAI_ROOT%
                nmake all'''
                bat '''nmake all'''
                bat '''nmake zip'''
                
            }
        }
        stage('Archive artifacts') {
            steps {
                archiveArtifacts artifacts: 'dist/*.zip', caseSensitive: false, followSymlinks: false
            }
        }
    }
}