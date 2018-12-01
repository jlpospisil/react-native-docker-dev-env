If you are working on an existing react-native application, that project should be loaded into the ./app directory.  That can be done multiple ways, but my suggestion would be to add it as a git submodule.
```
git submodule add https://host.com/user/project app
```

If there is no app directory, or no package.json file within the app directory, a new react-native project will be created using:
```
react-native init app
```

#### Start the container
```
docker-compose up
```

#### Stop the container
```
docker-compose down
```
