## Best practices for securely storing API keys Notes

### Why you shouldn’t store API keys on Git repositories
#### Public Git repositories
1. Anyone on the internet can access a public repository.
2. If the code in the repository is runnable, others can immediately access the API.

#### Private Git repositories
1. Private repository may be exposed to the third party applications when we integrate them to our repository.
2. Third party applications will obtain the access to the private repository. 


### Where should API keys be stored?
1. **Encrypt the files in the repository that contains the sensitive data**
    * Encrypt the whole repository : **git-remote-gcrypt**
    * Encrypt specific files : **git-secret** and **git-crypt**
    * Encrypt specific strings : **BlackBox**
    * Encrypt variables : **Docker Secrets**

2. **Store the sensitive data as config variables**
    * Heroku Configuration, application can access the sensitive data during runtime through the pre-defined config variables.


