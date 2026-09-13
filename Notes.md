#### Intro
- Github action for market place 
- python , docker, yaml, xml 
- Podcast feed generator - runs in github pages 

#### Ref: 
- https://github.com/planetoftheweb/podcast-test, 
- https://github.com/planetoftheweb/podcast-generator

#### Github Actions
- automate projects, task for repo on timer or event
- Own and Community actions from community market place

+ RSS flavour of XML
  + difficult to create
+ Yaml easily
  + Python for yaml to xml
+ Publish in Github Pages
  + Docker reqd

### Creating Actions 
+ Actions page in repor
  + new workflow > create your won workflow
  + new worfklow : main.yml will be created under .github/workflows directory 
   
### Workflows 
+ Name : name of the action
+ On : when should the action run
+ jobs : different jobs to run in action 
    + provide a job name ( e.g build )
    + runs-on : machine on which the job should run (ubuntu etc )
    + steps - steps of the job 
      + name of the step
      + uses - marketplace action
      + with - to specify pythoin version etc
      + run - to run a shell command
        + run : | pipe for multiline command
  + For pushing anything from the action job we need to do git config as if we were to do it on a new machine as this is a new unconfigured machine
  + any action will run immediately on push to main
  + to enable action to commit to repo we need to provide RW perimission from the repo settings page
### Creating a marketplace version of the actions
  + generator action that can be used by other repos 
    + Dockerfile - controls/configures the cloud virtual machine
      + choose version of OS(ubuntu) using FROM
      + RUN command to apt-get update and install applications ( python , pip and git )
      + COPY to copy application file from the repo to docker
      + ENTRYPOINT to call the script which will execute the genration actions
    + entrypoint - runs when other repos call this action
      + /bin/bash
      + do git config all over in the entrypoint script 
    + action file to application
      + action.yml
      + stays out of the workflows folder
      + will be run in other repos
      + file content :
        + name, author, description, runs - using (docker), image ( docker filename )
        + branding ( for giving icon to action feather icons from mkt place)- icon and color
        + inputs ( required for the action to run )
          + email, name ( Both have descrition, required, default fields )
    + Actions controls whats heppening with the files in the generator repo
      + when you use another repor to run this repo
        + finds action > dockerfile > entrypoint > set git and run app and push change to repo
### Using Action from market place ( then we just created) in another repo
  + Once action is complted it is ready to published in the market place
  + To use this action in another repo
    +   inside steps
      +   - name: Run Feed Generator
          - uses: RBK93/podcastgenerator@main
          -  uses: username/repo@branch
          - Action will be automatically picked
  - any change to action will not reflect until we run the child workflows again
### Release to market place , use github form 
