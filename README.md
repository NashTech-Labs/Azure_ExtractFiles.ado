# Azure_ExtractFiles.ado
Use this task to extract a variety of archive and compression files, such as .7z, .rar, .tar.gz, and .zip in Azure DevOps pipeline.

## Parameters:

The pipeline requires the following parameters to be defined:


| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | :-------------: | :-------------: | ------------- | :-------------: | ------------- |
| Azure_ExtractFiles | Archive file patterns | string | **/*.zip | .7z, .rar, .tar.gz, and .zip | Required | Specifies the file paths or patterns of the archive files to extract. Supports multiple lines of minimatch patterns. |
| destinationFolder | Destination folder | string |  | | Required | Specifies the destination folder into which archive files should be extracted. Use variables if files are not in the repo. For example: $(agent.builddirectory). |
| cleanDestinationFolder | Clean destination folder before extracting | boolean | true | | Optional | Specifies the option to delete the entire content of the destination directory (clean) before archive contents are extracted into it. |
| overwriteExistingFiles | Overwrite existing files | boolean | false | | Optional | Specifies the option to overwrite existing files in the destination directory if they already exist. If the option is false, the script prompts on existing files, asking whether you want to overwrite them. |
| pathToSevenZipTool | Path to 7z utility | string |  | | Optional | Specifies the custom path to 7z utility. For example, C:\7z\7z.exe on Windows and /usr/local/bin/7z on MacOS/Ubuntu. |
--------------------------------------------------------------------------------------------------------------------------------------------------

These parameters provide multiple use case options for the template, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

You can directly call a particular template as per the requirement. for example: 

 ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: your_username/Azure_ExtractFiles.ado
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'

  steps:
  # passing the parameters
  - template: Azure_ExtractFiles.yml
    parameters:
      archiveFilePatterns: '${{parameters.archiveFilePatterns}}' 
      destinationFolder: '${{parameters.destinationFolder}}' 
      cleanDestinationFolder: '${{parameters.cleanDestinationFolder}}' 
      overwriteExistingFiles: '${{parameters.overwriteExistingFiles}}' 
      pathToSevenZipTool: '${{parameters.pathToSevenZipTool}}' 
  ```
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.
