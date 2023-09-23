# VNC

## Connecting via SSH


```shell
ssh -t -L 5900:localhost:5900 home 'x11vnc -localhost -display :0'
```
