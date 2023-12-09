node {
    stage('git checkout') {
        git 'file:///C:/Projects/SsdtDevOpsDemo'

    }
    
    stage('Build Dacpac from SQLProj') {  
        bat "\"${tool name: 'Default', type: 'msbuild'}\" /p:Configuration=Release"
        stash includes: 'Database1\\bin\\Release\\Database1.dacpac', name: 'theDacpac'
    }
 
    stage('Deploy Dacpac to SQL Server') {
        unstash 'theDacpac'
        bat "\"C:\\Program Files (x86)\\Microsoft SQL Server\\130\\DAC\\bin\\sqlpackage.exe\" /Action:Publish /SourceFile:\"Database1\\bin\\Release\\Database1.dacpac\" /TargetServerName:(local) /TargetDatabaseName:Chinook"
    }
}
