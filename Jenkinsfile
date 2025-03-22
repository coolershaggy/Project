pipeline {
    agent any

    parameters {
        // Parameter to select the build type (Debug, Release, ReleaseInternal)
        choice(name: 'BUILD_TYPE', choices: ['Debug', 'Release', 'ReleaseInternal'], description: 'Choose the build configuration')
        // Parameter to enable or disable additional projects (ProjectC and ProjectD)
        booleanParam(name: 'ENABLE_CD', defaultValue: false, description: 'Enable ProjectC and ProjectD')
    }

    environment {
        // Set directories for build target, binaries, and libraries
        BLDTARGET = "${params.BUILD_TYPE}" // The build type selected by the user
        DSTDIR = "build\\${BLDTARGET}\\bin" // Path for executable binaries
        LIBDIR = "build\\${BLDTARGET}\\lib" // Path for libraries
    }

    stages {
        stage('Setup') {
            steps {
                echo "Preparing build environment..."
                echo "Build type: ${BLDTARGET}"
                echo "Binary output directory: ${DSTDIR}"
                echo "Library output directory: ${LIBDIR}"
            }
        }

        stage('CMake Configure') {
            steps {
                bat """
                mkdir build
                cd build
                cmake -G "Visual Studio 17 2022" -DCMAKE_BUILD_TYPE=${BLDTARGET} -DENABLE_CD=${params.ENABLE_CD ? 1 : 0} ..
                """
            }
        }

        stage('CMake Build') {
            steps {
                bat """
                cd build
                cmake --build . --config ${BLDTARGET}
                """
            }
        }

        stage('CMake Install (Optional)') {
            when {
                expression { params.BUILD_TYPE == 'ReleaseInternal' } // Install only for ReleaseInternal
            }
            steps {
                bat """
                cd build
                cmake --install . --config ${BLDTARGET}
                """
            }
        }

        stage('Conditionally Build ProjectC and ProjectD') {
            when {
                expression { return params.ENABLE_CD }
            }
            steps {
                echo "Building additional projects (ProjectC and ProjectD)..."
                bat """
                cd build
                cmake --build . --target ProjectC --config ${BLDTARGET}
                cmake --build . --target ProjectD --config ${BLDTARGET}
                """
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed!'
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Please check the logs for errors.'
        }
    }
}