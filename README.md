# Node_app_as_windows_service
Run Node app as a windows service


This page gives the resources and steps to make the node app run as a windows service.
To make the configuration simpler an example of "DartAnalyzeService" is taken here and the configurations are done for the same.
The steps would also ensure that the service is set to auto start so that even on restart of OS the app keeps running.

Resources : (With modifications done for example DartAnalyzeService)
check - daemon.zip


## Steps:
* Unzip this zip to the location of the app which you want to run as a background service.
* Edit the name of all files with the corresponding name of your service you wish to have. Replace "DartAnalyzeService" with your service name.
* Edit the xml file in extracted daemon folder with details of your service:
  * Note : Refer the DartAnalyzeService.xml from above daemon.zip
    * Replace "DartAnalyzeService" with the service name as desired for your service.
    * In the <description> section give the desired description for your service.
    * In the <executable> section give the location of the node.exe you want to run for your app.
      * Note 1 : If your node app is defined in the system path variable then just "node.exe" is enough as done in below example. 
      * Note 2 : If you have a specific version of node.exe to run provide the absolute path of that node executable
    * In <logpath>, provide the path where you want the out, error and wrapper logs to be saved.
    * In <argument> section provide the argument you want to feed to node executable. i,e your js file path as done in below example
    * In <workingdirectory> section provide the desired working directory you want your app to have.
* Edit the below command with your service name (same name as done in above steps) and run it in command prompt with admin rights.
* sc.exe create DartAnalyzeService binpath="C:\tool\dart\analyzeservice\daemon\DartAnalyzeService.exe" start=auto DisplayName="Dart Analyze Service"
* Start your service / restart your system.

## Result:
The stdout logs, error logs and wrapper logs are all saved in the logpath mentioned in the xml.
Once the above steps are done you should see the service running as below. (the deamon.zip attached results to this)

