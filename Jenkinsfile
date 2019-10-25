def axisNode = ["stable","release", "current", "edge"]
def axisTool = ["cl6","cl6h","cl7","cl7h","cl8"]
def tasks = [:]

for(int i=0; i< axisNode.size(); i++) {
    def axisNodeValue = axisNode[i]
    def subTasks = [:]
    for(int j=0; j< axisTool.size(); j++) {
        def axisToolValue = axisTool[j]
        subTasks["${axisNodeValue}/${axisToolValue}"] = {
            def javaHome = tool axisToolValue
            println "Node=${env.NODE_NAME}"
            println "Java=${javaHome}"
        }
    }
    tasks["${axisNodeValue}"] = {
        node(axisNodeValue) {
            parallel subTasks
        }
    }
}

stage ("cpanel") {
    parallel tasks
}
stage ("directadmin") {
    parallel tasks
}   
