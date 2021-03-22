## The Twelve Factors

### Methodology
- Use **declarative** formats for setup automation, to minimize time and cost for new developers joining the project;
- Have a **clean contract** with the underlying operating system, offering **maximum portability** between execution environments;
- Are suitable for **deployment** on modern **cloud platforms**, obviating the need for servers and systems administration;
- **Minimize divergence** between development and production, enabling continuous deployment for maximum agility;
- And can **scale up** without significant changes to tooling, architecture, or development practices.

#### Code Base

- A codebase is any single repo or any set of repositories who share a **root** commit.
- There is only one codebase per app, but there will be many deploys of the app.
- If there are multiple code bases, it’s not an app – it’s a **distributed** system.
- A deploy is a running **instance** of the app. This is typically a **production** site, and one or more **staging** sites. 

#### Dependencies

- A twelve-factor app never relies on **implicit** existence of system-wide packages. 

- A twelve-factor app **declares** all dependencies, completely and exactly, via a dependency declaration manifest.

**Examples**
1. **package.json** managed by npm or yarn which used to list all packages.
2. **requirements.txt** managed by pip which used to list all python libraries. 
3. Gemfile managed by Bundler.

- Furthermore, it uses a dependency isolation tool during execution to ensure that no implicit dependencies “leak in” from the surrounding system.

**Examples**
1. **Virtualenv** can be used to isolated all dependencies for a python program.
2. Npm creates a special directory **"node_modules"** to achieve dependency isolation. 

- No matter what the tool chain, dependency declaration and isolation must always be used together.

**Examples**
1. **requirements.txt** and **virtualenv** are always used together.
2. **package.json** and **node_modules** are always used together.

- Twelve-factor apps also do not rely on the implicit existence of any system tools.
#### Config

- Do not store config as **constants** in the code, config should strict separation from the code.
- Using **config files** is a huge improvement but still has weakness.
- The twelve-factor app stores config in **environment variables**.
- Env vars are easy to change between deploys without changing any code; unlike config files, there is little chance of them being checked into the code repo accidentally

#### Backing Services

- A backing service is any service the app consumes over the **network** as part of its normal operation.
- Backing services like the **database** are traditionally managed by the same systems administrators who deploy the app’s runtime
- The code for a twelve-factor app makes no distinction between local and third party services. 
- Resources can be **attached** to and **detached** from deploys at will.

#### Build, Release, Run

**Codebase to Deployment in 3 steps**
1. The build stage is a transform which converts a code repo into an executable bundle known as a build.
2. The release stage takes the build produced by the build stage and combines it with the current config of deploy.
3. The run stage (also known as “runtime”) runs the app in the execution environment, by launching some set of the app’s processes against a selected release.

- The twelve-factor app uses **strict separation** between the build, release, and run stages.
- Deployment tools typically offer release **management tools**, most notably the ability to **roll back** to a previous release.
- Every release should always have a **unique** release ID, such as a timestamp of the release.

#### Processes

- Twelve-factor processes are **stateless** and **share-nothing**.
- Any data that needs to persist must be stored in a **stateful backing service**, typically a database.
- **Sticky sessions** are a violation of twelve-factor and should never be used or relied upon. 

#### Port Binding

- The twelve-factor app is completely **self-contained** and does not rely on runtime injection of a webserver into the execution environment to create a web-facing service. 
- The web app **exports HTTP as a service by binding to a port**, and listening to requests coming in on that port.
- Note also that the port-binding approach means that one app can become the **backing service** for another app.

#### Concurrency

- Any computer program, once run, is represented by one or more processes.
- In the twelve-factor app, processes are a first class citizen
- Twelve-factor app processes should never daemonize or write PID files.

#### Disposability

#### Dev/prod parity

#### Logs

#### Admin Processes
