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
- In the twelve-factor app, processes are a **first class citizen**.
- Twelve-factor app processes should never daemonize or write PID files.

#### Disposability

- The twelve-factor app’s processes are **disposable**, meaning they can be started or stopped at a moment’s notice.
- Processes should strive to **minimize** startup time. 
- Processes shut down **gracefully** when they receive a SIGTERM signal from the process manager.
- Processes should also be **robust** against sudden death, in the case of a failure in the underlying hardware.

#### Dev/prod parity

**Difference between local development and production**
1. **The time gap**: A developer may work on code that takes days, weeks, or even months to go into production.
2. **The personnel gap**: Developers write code, ops engineers deploy it.
3. **The tools gap**: Developers may be using a stack like Nginx, SQLite, and OS X, while the production deploy uses Apache, MySQL, and Linux.

- The twelve-factor app is designed for continuous deployment by keeping the gap between development and production small. 
1. Make the **time gap small**: a developer may write code and have it deployed hours or even just minutes later.
2. Make the **personnel gap small**: developers who wrote code are closely involved in deploying it and watching its behavior in production.
3. Make the **tools gap small**: keep development and production as similar as possible.

- The twelve-factor developer resists the urge to use different backing services between development and production, even when adapters theoretically abstract away any differences in backing services.

#### Logs

- Logs are the stream of aggregated, time-ordered events collected from the output streams of all running processes and backing services.
- A twelve-factor app never concerns itself with routing or storage of its output stream. 
- In staging or production deploys, each process’ stream will be captured by the execution environment, collated together with all other streams from the app, and routed to one or more final destinations for viewing and long-term archival. 

#### Admin Processes

- One-off admin processes should be run in an **identical environment** as the regular long-running processes of the app. 
- The same **dependency isolation** techniques should be used on all process types. 
- Twelve-factor strongly favors languages which provide a REPL shell out of the box, and which make it easy to run one-off scripts.