# dr
Docker Runner

# Basic Use

Configure dr's main directory for scripts. Only needs to be called once ever per host.
```
dr configure DIRECTORY
```

Install a container supporting dr from DockerHub
```
dr install CONTAINERNAME SERVICENAME
```

Manage that container
```
dr SERVICENAME COMMAND ARGS
```

## Example
Using [simplesecrets](https://github.com/j842/docker-simplesecrets) as the example:
```
dr configure /opt/dr
dr install j842/simplesecrets simplesecrets
dr simplesecrets help
S3KEY=abcde S3SECRET=1234 BUCKET=mybucket dr simplesecrets configure
dr simplesecrets < myfile
```

# Making a container compatible with dr

## Files needed

Create the drinstall script
```
/usr/local/bin/drinstall SERVICENAME   -- populates /dr with everything below.
```

And created by drinstall:
```
/dr/txt/shorthelp.txt                  -- shown when dr is run with no args
/dr/bin/hostinit                       -- automatically run on host when installed
/dr/bin/help                           -- show help for commands available
/dr/bin/run                            -- make the service go!
```
Also create files in bin that can be run on the host to manage the container (e.g. configure).

## Files automatically added by dr

```
/dr/txt/containername.txt              -- e.g. j842/simplesecrets 
/dr/txt/servicename.txt                -- e.g. simplesecrets
```