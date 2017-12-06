# Setting up

For the demo you need three projects set up in your Openshift environment: skatdemo-build, skatdemo-dev, skatdemo-test. Optionally, you also need a jenkins running in the build project.

## Creating projects

To create the projects, run the follwing commands:

`oc new-project skatdemo-build --display-name="Build project for demo"`

`oc new-project skatdemo-dev --display-name="Development project for demo"`

`oc new-project skatdemo-test --display-name="Test project for demo"`

## Setting up jenkins to build project (optional)

You can add jenkins to the build project via the web console:

Navigate to the project, and click Add to Project -> Browse Catalog -> Continuous Integraiton & Deployment -> Jenkins (persistent) -> Select -> Create.

## Configuring access for jenkins

We are going to assume that jenkins will be using a specific service account for running the jenkins pod: 'jenkins'.

`oc policy add-role-to-user edit system:serviceaccount:skatdemo-build:jenkins -n skatdemo-build`

`oc policy add-role-to-user edit system:serviceaccount:skatdemo-build:jenkins -n skatdemo-dev`

`oc policy add-role-to-user edit system:serviceaccount:skatdemo-build:jenkins -n skatdemo-test`

## Creating the pipeline

We will create the jenkins pipeline directly from git repository. If you didn't set up jenkins, creating the pipeline will also deploy a Jenkins instance to the build-project automatically. To create the jenkins pipeline, run the following command:

`oc new-build https://github.com/jmetso/csv-service.git --context-dir=pipeline2 --strategy=pipeline --name=csv-pipeline -l pipeline=csv -n skatdemo-build`

After creating the pipeline, it will take some time to deploy a jenkins pod and the pipeline to actually start running. Sometimes you may have to cancel the first run and trigger a new run manually.
