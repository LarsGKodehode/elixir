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
  - [Routing](#routing)
  - [Controllers](#controllers)
- [Useful Links](#useful-links)

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
- Bumping to Elixir 1.14.3, Phoenix 1.6.16 and Node 19 fixes ElixirLS warnings, and no issues srufaced immediately.

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
The router uses macros for HTTP verbs along with a set of others. The macro Resources looks interesting, it expands to a set of routes for a 'RESTful' endpoint. I am presuming it is not to difficult to define your own macros.
Phoenix dynamically generates a set of path helper functions for referencing correct paths in our templates.
For collections of plugs one want to run for the different endpoints Phoenix provides a facade, or pipeline. The pipe_through keyword accepts a list of plugs.

#### Notes
- ```$ mix phx.routes``` Outputs all the routes for the application
- [Link to documentation for macro resources](https://hexdocs.pm/phoenix/Phoenix.Router.html#resources/4)
- The resources macro accepts by passing in ```:only``` or ```:show``` as options
- When nesting routes with scopes, ensure that you do not have any path duplication

#### Asides
Something I am noting here is the lack of IntelliSense code completion for certain things, macros seems to lack atleast some awareness.<br>
[Repo to the 'official' Elixir Language Server.](https://github.com/elixir-lsp/elixir-ls)<br>
*Macros - A reminder*: A macro is a language keyword the preprocessor will expand into a larger set of instructions.

### **Controllers**
Phoenix comes with the basic function for responding we want ```text/2, html/2, json/2``` in addition to its own function for rendering templates ```render/3```. Returning different files by checking for query parameters is quite simple.

#### Notes
- For the ```render/3``` function to work correctly the controller **and** the veiw must share the same root name.
- Mind the file ending for non HTML view files, *\*.eex* **not** *\*.heex*.
 [Forum post.](https://elixirforum.com/t/why-does-phoenix-1-6-use-html-heex-as-the-suffix-of-the-template-file/42013)
- [Docs for MIME types](https://hexdocs.pm/mime/2.0.2/MIME.html)
- [Docs for Status Codes mapped to atoms](https://hexdocs.pm/plug/1.13.6/Plug.Conn.Status.html#code/1)

#### Asides
The documentation for the ```use``` macro recommends using ```import``` instead, when possible. The guide uses **use**. I do need to read up on how Elixir handles modules. 

## Useful Links
- [**Tool: Code Analysis for Elixir**](https://github.com/rrrene/credo)
- [Summary of web project requirements](https://elixirforum.com/t/is-learning-only-elixir-enough-as-a-backend-developer-to-develop-any-project/44100/14)
- [Curated list of Elixir and Erlang libs, resources ++](https://github.com/h4cc/awesome-elixir)