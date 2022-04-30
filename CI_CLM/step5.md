## Using CLM to visualize results in a pull request

It is very tedious to check the results on the logs of the runner at each instance. Instead, now we will try to use CLM to visualize and display the results in a file
that will show up on the pull request page. 


CML can easily display a `.md` file using the command cml-send-comment. So in the yaml file, after running the `python main.py`, write the following commands


          
          echo "## Model metrics" > report.md
          cat results.txt >> report.md
          
          echo "## Plots" >> report.md
          echo "### Loss" >> report.md
          cml-publish loss.png --md >> report.md
          
          echo "### Accuracy" >> report.md
          cml-publish acc.png --md >> report.md
          
          cml-send-comment report.md
                   


As seen above, we are just using `echo` to append the results from `metrics.txt` to `report.md`. The command `cml-publish` is used to add an image to the report, and 'cml-send-comment' is used to put the report on the pull request. When making a change and committing, you should now see the report on your pull request like this

![image](https://user-images.githubusercontent.com/27778126/166103751-ac91c02c-1e0e-46d0-9fc0-23dd6d3965ce.png)



