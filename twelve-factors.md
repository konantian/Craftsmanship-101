## The Twelve Factors

### Methodology
- Use **declarative** formats for setup automation, to minimize time and cost for new developers joining the project;
- Have a **clean contract** with the underlying operating system, offering **maximum portability** between execution environments;
- Are suitable for **deployment** on modern **cloud platforms**, obviating the need for servers and systems administration;
- **Minimize divergence** between development and production, enabling continuous deployment for maximum agility;
- And can **scale up** without significant changes to tooling, architecture, or development practices.

#### Code Base

- A codebase is any single repo or any set of repositories who share a root commit.
- There is only one codebase per app, but there will be many deploys of the app.
- If there are multiple code bases, it’s not an app – it’s a distributed system.
- A deploy is a running instance of the app. This is typically a production site, and one or more staging sites. 

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
- 

#### Backing Services

#### Build, Release, Run

#### Processes

#### Port Binding

#### Concurrency

#### Disposability

#### Dev/prod parity

#### Logs


#### Admin Processes
