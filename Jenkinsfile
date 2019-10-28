def getTasks(axisNodes, axisTools) {
    def tasks = [:]
    for(int i=0; i< axisNodes.size(); i++) {
        def axisNodeValue = axisNodes[i]
        for(int j=0; j< axisTools.size(); j++) {
            def axisToolValue = axisTools[j]
            tasks["${axisNodeValue}/${axisToolValue}"] = {
                node(axisNodeValue) {
                    def javaHome = tool axisToolValue
                    println "Java=${javaHome}"
                }
            }
        }
    }
    return tasks
}

pipeline {
    agent none

    stages {

        stage("Before") {
            agent any
            steps {
                echo "before"
            }
        }

        stage("Matrix") {
            steps {
                script {
                    def axisNodes = ["osx-agent-1","osx-agent-2"]
                    def axisTool = ["jdk7","jdk8"]
                    parallel getTasks(axisNodes, axisTool)
                }
            }
        }

        stage("After") {
            agent any
            steps {
                echo "after"
            }
        }
    }
}
