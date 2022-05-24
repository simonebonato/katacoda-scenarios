## Prepare a folder for GitHub action

The CI pipeline that we are implementing makes use of the GitHub actions, lines of code that utilize the so called *workflows*. In a workflow, a server is provided by Github on which code can be executed that is specified in the workflow file. You may either write the code there or create a re-usable action in another repository. You can publish this action for others on the so-called Github market place and also use other persons' actions.

The first step to take is to clone the repository we have just forked, and we can do that by going to the page of the directory, copying the link (as shown in the picture), and finally use the following line on the terminal:

`git clone <your repository name>`

Please make sure that you are cloning the forked version of the repo

![image](https://user-images.githubusercontent.com/63954877/168800397-afd2079c-834d-466c-97ed-72183c833792.png)

In order to use them, what you have to do is create the following folder structure inside of your repository, containing a file with the *.yaml* extension.

.github/workflows/[your_file_name].yaml (1) 

The name of the file can be decided arbitrarily, what matters is that the extension is *.yaml*.

In order to create the file, we can first check the name of the available directories by using the command `ls`{{execute}}, and after that we can use `cd CI-with-CML`{{execute}} to access it.

Once we are inside it, we can create folder structure mentioned above using the following commands `mkdir .github`{{execute}} and once accessing it using `cd .github`{{execute}}, we make `mkdir workflows`{{execute}} and access it in the same way.

At this point we want to create the .yaml file using `touch CML.yaml`{{execute}}

First lets set up the configuration with this command. You need to insert your email id and username here. 
`git config --global user.email <your_email>` and `git config --global user.name <your_name>`.





We can then proceed with the next part of the tutorial!
