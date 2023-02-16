# Elixir - A efficient and reliable web framework?

## Content
- [This Repository](#this-repository)
  - [Short](#short)
  - [Folder Structur](#folder-structure)
- [Phoenix - Guided Steps](#phoenix---guided-steps)
  - [Setup](#setup)
  - [Creating an Application](#creating-an-application)
  - [Routes](#routes)
  - [Plugs](#plugs)

## This Repository

### **Short**

The intention behind this repository is to get to know Elixir and in the end setting up some form of realtime communication web application, possibly making it usable through Module Federation. I am also writing some notes here for future reference.

### **Folder Structure**

I am keeping it simple to start with. Both configs and app folders will be at live at the root.
At least until I get a good enough understanding of the CICD requirements to integrate this with one of the larger build systems.

## Phoenix - [Guided Steps](https://hexdocs.pm/phoenix/up_and_running.html)

### **Setup**
Using a community built devcontainer with VS Code made this rather easy. There are some complaints from ElixirLS that the version of Elixir (1.12) is not compatible with OTP 24. We will have to look at either updating what we have or looking for a newer image. Also a compiler warning that :settext is not needed any more. Tried the easy way of just removing the lines advised, but that prompted a whole page of errors requiring the missing module. I had to do a rollback in the end and just let it be.

#### Notes
- We have to spin up the database separately. Easily achieved by using docker with a compose file.
- We have to spin up the database separately. Easily achieved by using docker with a compose file.
- Remember to forward the ports in the devcontainer.json

### **Creating an Application**
Simple couple of commands and example page is up and rolling. It does comes with it's own dashboard for monitoring the internals of the application out of the box, by default only enabled in development mode. The Phoenix Framework follows the Model-View-Controller pattern all three contained within the lib folder. A detailed breakdown is [here](https://hexdocs.pm/phoenix/directory_structure.html).

#### Notes
- Entrypoint is at \<app>/lib/\<app>/application.ex
- Tests are living in a seperate test folder.

### **Routes**
Defining and creating new routes is rather straight forward. Simple to pass along dynamic rout parameters.

#### Notes
- Assign a response to HTML verbs in \<app>_web/router.ex
- Define response in \<app>_web/controllers/\<name>_controller.ex
- Phoenix is a templating engine

### **Plugs**

#### Notes