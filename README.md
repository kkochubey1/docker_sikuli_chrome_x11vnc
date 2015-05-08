# docker_sikuli_chrome_x11vnc
Docker file to build image with sikuli ide, chrome browser and vnc server for remote access

## Start container 

start container with VNC server on port 5901

```
docker run -d -t --name sikuli_5901 -v $(pwd):/home/seluser/scripts -p 5901:5900 kkochubey1/sikuli_chrome_x11vnc:latest
```

## Open VNC

Use VNC viewer (for example Mac: Screen Share, Win: Tight VNC viewer etc)

Connect to
``` 
192.168.59.103:5901
```
When promped for password, type: secret

If no connection check docker IP by running
```
boot2docker ip
```
or try 
```
127.0.0.1:5901
```

if there is still no connection, check container logs
```
docker logs sikuli_5901
```

## Start chrome browser

Inside VNC screen, open terminal by right mouse click -> Applications -> Terminal Emulators -> XTerm
Run following
```
/opt/google/chrome/google-chrome
``` 

Start chrome browser from command line by docker
```
docker exec -it sikuli_5901 bash -c "sudo -E -i -u seluser /opt/google/chrome/google-chrome --no-default-browser-check"
```

## Start sikuli-ide to edit scripts
```
docker exec -it sikuli_5901 bash -c "sudo -E -i -u seluser /usr/bin/sikuli-ide"
```
Use /home/seluser/scripts folder to save scripts in local folder on host machine

## Start sikuli to run existing scripts 
from current host local folder (assuming there is test.sikuli)
```
docker exec -it sikuli_5901 bash -c "sudo -E -i -u seluser /usr/bin/sikuli-ide -r /home/seluser/scripts/test.sikuli"
```

## Stop and remove working container 

```
docker stop sikuli_5901
docker rm sikuli_5901
```


