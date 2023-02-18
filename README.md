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
At least until I get a good enough understanding of the CICD requirements to integrate this with another build systems.

## Phoenix - [Guided Steps](https://hexdocs.pm/phoenix/up_and_running.html)

### **Setup**
#### - using [Erlang/OTP 24, Elixir 1.12.3, Mix 1.12.3]
Using a community built devcontainer with VS Code made the setupt process easy. When starting the devcontainer ElixirLS sometimes issue a warning that version of Elixir (1.12) is not compatible with OTP 24. Going by the [compatability matrix](https://hexdocs.pm/elixir/1.12/compatibility-and-deprecations.html) it should be compatible.
The container defaulted to Elixr 1.12.3. There are newer versions of Elixir available, I will look into finding or creating a updated image if this test turns out favorably.
Out of the box the compiler printed a warning ```...:settext is not needed any more...```. Following the suggested steps fixed that.

#### Notes
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
Plugs are similar to middleware in other languages. The main difference seems to be that Phoenix is bundling both the request and response into a single object *Plug.Conn*. Can be defined inline or in seperate modules.

#### Notes
- Plugs has broad support throughout the stack and can be put in the router, endpoint or controllers.
- Composability of plug transformation seems to allow for easier logical constructs.
- [Link to documentation for Plugs](https://hexdocs.pm/plug/Plug.Conn.html)
- [Link to Plug Project](https://hexdocs.pm/plug/1.13.6/Plug.html)

### **Routing**
[TODO](https://hexdocs.pm/phoenix/routing.html)

#### Notes