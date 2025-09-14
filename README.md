## GITLAB CICD

I have created a separate repository with rules and refered them in this repository. This way other common constructs can be moved to the shared repository and be used from different repositories.

### Rules in the shared repository
~~~
# Manual job, fails if run fails
.manual_no_failure:
  rules:
    - when: manual
      allow_failure: false

# Automatic if previous jobs succeed, but also allow manual run
.automatic_no_failure:
  rules:
    - when: on_success
      allow_failure: false
    - when: manual
~~~

## General Flow
stages:
  1. build
  2. systest_deploy
  3. preprod_deploy

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/953716a1-cf23-4740-b63e-8f32ef59cb0a" />



### The main deployment flow would look like this 
<img width="1162" height="450" alt="image" src="https://github.com/user-attachments/assets/5d2ec18e-1e6f-4dde-80aa-ca15030e9850" />

<img width="1631" height="475" alt="image" src="https://github.com/user-attachments/assets/40d1b95c-8f05-4825-8b68-7f0c608f5382" />

<p>Here we intentionally fail the systest db job. If the DB job fails then it should run the subsequent jobs in that stage. But it shouldnt block the preprod db update job to run (not realistic). </p>

