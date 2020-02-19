# PartsUnlimited
This ARM template is intended for use with the Azure DevOps demo labs Parts Unlimited project, located [here](https://azuredevopslabs.com/labs/azuredevops/continuousdeployment/). Use of this template will replace Task 1 of the lab.


## Step 1 ##

- Download the *parameters.json* and *template.json* files from the PartsUnlimited folder.

## Step 2 ##

- Open the PartsUnlimited project in Visual Studio.
- Create a topic branch from *master*.
- Create a new solution folder called *deployment*.
- Upload the *parameters.json* and *template.json* files to the *deployment* folder.
- Push your topic branch and create a pull request.
- Complete the pull request to merge into *master*

## Step 3 ##

- Navigate to Pipelines > Builds and edit the *PartsUnlimtedE2E* pipeline.
- Modify the **Copy Files** task so to the following values:
<table>
<thead>
<tr>
  <th>Parameter</th>
  <th>Value</th>
</tr>
</thead>
<tbody>
<tr>
  <td><b>Source Folder</b></td>
  <td>PartsUnlimited-aspnet45/deployment</td>
</tr>
<tr>
  <td><b>Contents</b></td>
  <td>**/*.json</td>
</tr>
<tr>
  <td><b>Target Folder</b></td>
  <td>$(build.artifactstagingdirectory)</td>
</tr>
</tbody>
</table>

- Save the pipeline.

## Step 4 ##

- During Task 2 of the lab, add a *Azure Resource Group Deployment* task to the release pipeline and drag it to the top as the first step.
- Add the following variables to the release pipeline:
<table>
<thead>
<tr>
  <th>Name</th>
  <th>Value</th>
</tr>
</thead>
<tbody>
<tr>
  <td><b>sqlServerPassword</b></td>
  <td>A unique password that you can remember (you can write it down for the lab).</td>
</tr>
<tr>
  <td><b>sqlServerName</b></td>
  <td>A unique name to Azure. Suggest using: {your initials}-qa-sql</td>
</tr>
<tr>
  <td><b>websiteName</b></td>
  <td>A unique name to Azure. Suggest using: {your initials}-qa-pul</td>
</tr>
</tbody>
</table>

- In the *Azure Resource Group Deployment*, edit the Template section with the following values:
 
<table>
<thead>
<tr>
  <th>Parameter</th>
  <th>Value</th>
</tr>
</thead>
<tbody>
<tr>
  <td><b>Template</b></td>
  <td>$(System.DefaultWorkingDirectory)/_PartsUnlimitedE2E/drop/template.json</td>
</tr>
<tr>
  <td><b>Template parameters</b></td>
  <td>$(System.DefaultWorkingDirectory)/_PartsUnlimitedE2E/drop/parameter.json</td>
</tr>
<tr>
  <td><b>Override template parameters</b></td>
  <td>-administratorLoginPassword $(sqlServerPassword) -sqlServerName $(sqlServerName) -websiteName $(websiteName)</td>
</tr>
</tbody>
</table>

- Complete the rest of the lab, skipping Task 3.
