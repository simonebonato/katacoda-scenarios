## Triggering the GitHub action

At this point we can add some lines to the code that we have just written on the yaml file:

<pre class="file" data-filename="workflow.yml" data-target="prepend">
  echo "Model Metrics"
  cat results.txt
</pre>

Echo simply prints out what follows inside the GitHub actions page when it is triggered (we will see shortly), while cat does the same as Echo, only with the content of the txt file.

This is how your code is supposed to look like at this point:

<pre class="file" data-filename="workflow.yml" data-target="prepend">
name: CI-with-CML
on: [push]
jobs:
  run:
    permissions: write-all
    runs-on: ubuntu-latest
    # optionally use a convenient Ubuntu LTS + DVC + CML image
    container: docker://dvcorg/cml-py3:latest
    steps:
      # may need to setup NodeJS & Python3 on e.g. self-hosted
      # - uses: actions/setup-node@v2
      #   with:
      #     node-version: '16'
      # - uses: actions/setup-python@v2
      #   with:
      #     python-version: '3.x'
      - uses: actions/checkout@v2
      - name: running cml
        env:
            repo_token: ${{ secrets.GITHUB_TOKEN }}
        run: |
          # Your ML workflow goes here
          pip install -r requirement.txt
          python main.py
          echo "Model Metrics"
          cat results.txt
</pre>

Now, instead of committing directly to the master branch, we can create a new branch that we will call "test", in the following way `git checkout -b test`{{execute}}. We can finally add and commit the changes using `git add .`{{execute}} and after `git commit -m "sample message"`{{execute}}. Now we can push it to your forked branch using the command `git push --set-upstream origin test`{{execute}}.


Next we want to open a Pull Request (Go to Pull Requests > New Pull Request), hence press on "New Pull Request" specifying that the branch you want to merge to, is the base repository that you forked initially. You want to compare the test branch you just created with the main branch. 
The PR is a place where it is possible to see what changes have been made to a branch of a repository, and you can discuss with your colleagues whether or not you want your edits to be merged into the main branch. 

What happens next is that, as we are opening a new branch, some code will be automatically pushed to the newly created branch and our GitHub action will be activated. As a consequence, on the PR page you will probably see something like this:

![image](https://user-images.githubusercontent.com/63954877/166104196-c92ddfd9-5ebe-4727-84d7-c138d24feca9.png)

This means that the action that we have created is up and running! If we click on "details" we can observe what is going on inside:

![image](https://user-images.githubusercontent.com/63954877/166104425-195db6d5-f232-4b68-978d-cef9133a447e.png)

You will probably recognize the names, they are the names of the functions described in the yaml file. 
If you press on "running cml" and scroll down until the end, this is what you'll see:

![image](https://user-images.githubusercontent.com/63954877/166104334-00a9a211-3c87-4e33-bfd2-2dcefdf66bd7.png)

Which is exactly what we wanted our action to print. As you can see, seeing the results of the action in this way is a bit clunky and not really informative.

The idea is that, whenever somebody pushes code to the branch we have just created, the action will be triggered, and here on the PR page we can observe the results of our workflow. 

In the next section we will see how to use the CML library to get much better insights!
