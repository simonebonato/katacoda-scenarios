## Prepare a folder for GitHub action

The CI pipeline that we are implementing makes use of the GitHub actions, which are lies of code that are executed automatically any time they are triggered, for example when some new code is pushed to the repo.

In order to use them, what you have to do is create the following folder structure inside of your repository, containing a file with the *json* extension.

.github/workflows/[your_file_name].yaml (1) 

The name of the file can be decided arbitrarily, what matters is that the extension is *json*.

In order to create the file, simply get into the main GitHub repo, press "Add file", then "Create new file" and on top write (1), inserting a name instead of the brackets (we will use "cml").
Then simply commit the code (green button below) directly to the main branch.
![image](https://user-images.githubusercontent.com/63954877/165971853-fb6ead44-bc24-4116-9f75-445cd8b79ff2.png)


This if a picture of how it has to look like in the end:
![image](https://user-images.githubusercontent.com/63954877/165970477-25920180-e3a7-470b-94f7-c2306dbfefc5.png)

And inside the workflows folder:
![image](https://user-images.githubusercontent.com/63954877/165970525-4e608d82-c4ab-4144-aff4-a7b0a240f516.png)

