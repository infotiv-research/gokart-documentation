### Caution
You cannot turn of the gokart when the wheel are active. Make sure to stop it either using the RC controller or the command below:

```bash
rostopic pub Speed_Request_Speed std_msgs/Float32 0
```

# Turning on the GoKart

Find all host in network with open ssh port
```bash
nmap -Pn -p22 192.168.150.1/24 -oG - | grep "/open" | awk '{ print $2 }'
```
ssh fingerprint:
```bash
ssh -X gokart1@dobby.local
ECDSA key fingerprint is SHA256:GkO/qyuwj+tCfwaZArQbMS8XsPUA4gfbMJdeTnqG1n4.
```

## Access to the camera remotely

After updating the configuration file `rtsp-simple-server.yml` as below

```txt
paths:
  cam:
    runOnInit: ffmpeg -f v4l2 -i /dev/video1 -preset ultrafast -b:v 600k -f rtsp rtsp://localhost:$RTSP_PORT/$RTSP_PATH
    runOnInitRestart: yes
    
```
Execute rtsp-simple-server_v0.19.1_linux_arm64v8/ server:
```bash
./rtsp-simple-server    
```

```bash
vlc -vvv --network-caching 200 rtsp://192.168.150.120:8554/cam
```

## Battery 



## Using Power supply 

## Tests

## Remote control

The right panel can be used to move forward and make quick brakes. To reverse, double back (brake) reverses the gear. (IT is noticable from the beeping sound)


