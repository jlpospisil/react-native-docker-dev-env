- If you are working on an existing react-native application, that project should be loaded into the ./app directory.  That can be done multiple ways, but my suggestion would be to add it as a git submodule.
```
git submodule add https://host.com/user/project app
```

- If there is no app directory, or no package.json file within the app directory, a new react-native project will be created using 'react-native init app' when the container is started.

#### Start the container
```
docker-compose up
```

#### Stop the container
```
docker-compose down
```

#### Connect to physical android device
- If you haven't previously built the docker image, you will have to accept the RSA key and allow debugging and then restart the container.
- I also had to connect the physical device to a PC and run 'adb tcpip 5555' before the device was available in the container.  Before running this, the device kept showing up as offline inside the container.
```
- update ANDROID_DEVICE_IP in react-native/start_app prior to starting container
- docker-compose up
```
OR
```
docker container ls
docker exec <containerid> adb connect <android_device_ip_address>:5555
```

#### Remove all stopped docker containers
```
docker rm $(docker ps -a -q)
```

#### Remove all untagged docker images
```
docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
```
