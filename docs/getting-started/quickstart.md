---
layout: wmt/docs
title:  Quickstart
side-navigation: wmt/docs-navigation.html
---

# {{ page.title }}

If you have [installed your own Concord server](./installation.html) or have
access to a server already, you can set up your first simple Concord process
execution with a few simple steps:

- [Create a Git Repository](#create-repository)
- [Add the Concord File](#add-concord-file)
- [Add a Deploy Key](#add-deploy-key)
- [Create Project in Concord](#create-project)
- [Execute a Process](#execute-process)
- [Next Steps](#next-steps)

<a name="create-repository"/>
## Create Git Repository

Concord process definitions and their resources are best managed and source
controlled in a Git repository. Concord can automatically retrieve the contents
of the repository and create necessary resources and executions as defined in
the content.

Start with the following steps:

- Create the repository in your Git management sytem, such as GitHub, using the
  user interface;
- Clone the repository to your local workstation.

<a name="add-concord-file"/>
## Add the Concord File

As a next step, add the Concord file `concord.yml` in the root of the repository.
A minimal example file uses the automatically used `default` flow:

```yaml
flows:
  default:
  - log: "Hello Concord User"
```

The `default` flow in the example simply outputs a message to the process log.

<a name="add-deploy-key"/>
## Add a Deploy Key

In order to grant Concord access to the Git repository via SSH, you need to
create a new key on the Concord server.

- Log into the Concord Console user interface;
- Navigate to _Organizations_ &rarr; _[your organization] &rarr;  Secrets_ (Contact your support team/administrators to create a new organization or have you added to an existing organization)
- Select _New secret_ on the toolbar;
- Provide a string e.g. `mykey` as _Name_ and select _Generate a new key pair_ as _Type_;
- Press _Create_.

The user interface shows the public key of the generated key similar to
`ssh-rsa ABCXYZ... concord-server`. This value has to be added as an authorized deploy
key for the git repository. In GitHub, for example, this can be done in the
_Settings - Deploy keys_ section of the repository.

Alternatively the key can be
[created](../api/secret.html#create-secret) and
[accessed](../api/secret.html#get-key) with the REST API for secrets.


<a name="create-project"/>
## Create Project in Concord

Now you can create a new project in the Concord Console.

- Log into the Concord Console user interface;
- Navigate to _Organizations_ &rarr; _[your organization] &rarr;  Projects_ (Contact your support team/administrators to create a new organization or have you added to an existing organization)
- Select _New project_ on the toolbar;
- Provide a _Name_ for the project e.g. 'myproject';
- Click the _Create_ button;
- Under 'Repositories' tab, select _Add repository_;
- Provide a _Name_ for the repository e.g. 'myrepository';
- Select the _Custom authentication_ button;
- Select the _Secret_ created earlier using the name e.g. `mykey`;
- Use the SSH URL for the repository in the _URL_ field e.g. `git@github.com:me/myrepo.git`;

If global authentication/trust between your GitHub repositories and the Concord
server is configured, you can simply use the HTTPS URL for the repository in the
_URL_ field.

Alternatively you can
[create a project with the REST API](../api/project.html#createproject).

**Note**: project creation in the Default organization might be disabled by
the instance admins using [policies](./policies.html#entity-rule)

<a name="execute-process"/>
## Execute a Process

Everything is ready to kick off an execution of the flow - a process:

- Locate the repository for the project;
- Press on the three dots for the repository on the right;
- Press on the _Run_ button;
- Confirm to start the process by clicking on _Yes_ in the dialog;

A successful process execution results a message such as:

```
{
  "instanceId": "e3fd96f9-580f-4b9b-b846-cc8fdd310cf6",
  "ok": true
}
```

The _Open process status_ button navigates you to the process execution and
provides access to the log, forms and more. Note how the log message
`Hello Concord User` is visible.

Alternatively the process can be accessed via the queue:

- Click on the _Processes_ tab;
- Click on the _Instance ID_ value of the specific process;
- Press on the _Log_ tab to inspect the log.

Alternatively the process can be started via the
[Process REST API](../api/process.html).

<a name="next-steps"/>
## Next Steps

Congratulations, your first process flow execution completed successfully!

You can now learn more about flows and perform tasks such as

- Add a [form](./forms.html) to capture user input;
- Using [variables](../processes-v2/index.html#variables);
- [Groups of steps](../processes-v2/flows.html#groups-of-steps);
- Add [conditional expressions](../processes-v2/flows.html#conditional-expressions);
- [Calling other flows](../processes-v2/flows.html#calling-other-flows);
- Work with [Ansible](../plugins-v2/ansible.html), [Jira](../plugins-v2/jira.html) and [other](../plugins-v2/) tasks;
- Maybe even [implement your own task](../processes-v2/tasks.html#create-task)

and much more. Have a look at all the documentation about the
[Concord DSL](../processes-v2/flows.html), [forms](./forms.html),
[scripting](./scripting.html) and other aspects to find out more!
