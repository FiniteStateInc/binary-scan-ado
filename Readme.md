
# [Finite State](https://finitestate.io) `binary-scan` Extension for Azure DevOps

![Finite state logo](./Tasks/binaryScan/screenshots/FS-Logo.png)
[finitestate.io](https://finitestate.io)

The Finite State `binary-scan` Extension allows you to easily integrate the Finite State Platform into your Azure Devops Pipeline.

Here you will find how this [extension was build](https://learn.microsoft.com/en-us/azure/devops/extend/develop/add-build-task?toc=%2Fazure%2Fdevops%2Fmarketplace-extensibility%2Ftoc.json&view=azure-devops) and how to release a new version of the extension.

Our extension executes a [js file](./Tasks/binaryScan/main.js). In that file we execute our python script that uploads the binary other functionality like adding a comment to a PR.

You can see the extension documentation itself [here](Marketplace.md)

## Release a New Version

Requirements:
 - Install [npx](https://www.npmjs.com/package/npx)
 - Install [tfx-cli](https://www.npmjs.com/package/tfx-cli)

Run `make bump` to build a new vsix file to upload to the Azure Markeplace.

## Run Test in Local Environment
You have different commands in [Makefile](Tasks/binaryScan/Makefile) inside the Tasks/binaryScan folder.
```bash
make install-all  # mainly it install python and js dependencies
make test-all     # run js and python tests
```

## Package and Publish Extension
- [Markeplace URL](https://marketplace.visualstudio.com/manage/publishers/finite-state)

- [How to Package and publish extesions](https://learn.microsoft.com/en-us/azure/devops/extend/publish/overview?toc=%2Fazure%2Fdevops%2Fmarketplace-extensibility%2Ftoc.json&view=azure-devops)

- [Publish by command line](https://learn.microsoft.com/en-us/azure/devops/extend/publish/command-line?toc=%2Fazure%2Fdevops%2Fmarketplace-extensibility%2Ftoc.json&view=azure-devops)

### Update Extension

If you want to update the tasks, you will first need to raise the version of the extension, otherwise the marketplace won’t let you publish it. To do this, simply edit the “version” attribute in the [vss-extension.json](vss-extension.json) file, and make sure it is higher than the previous one. When you run `make publish` this is done automatically.

You will also need to update the version of the [tasks](Tasks/binaryScan/task.json) and change the version attribute, which corresponds with the ‘Task version’ dropdown option in the build or release pipeline.

When you raise the ‘Major’ attribute, it will be applied to newly added tasks and enable the option to update existing tasks (by choosing the newer version in the dropdown options). Meanwhile, the ‘Minor’ attribute will automatically update them, and ‘Patch’ is generally reserved for minor bug fixes. One thing to keep in mind, if your update has some breaking changes, it is recommended to update the ‘Major’ version, because it won’t automatically update every all that are already leveraging the extension. This way, those pipelines won’t throw any errors if anything does break.