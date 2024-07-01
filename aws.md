# Remote Jupyter Notebook via SSH
- On the remote side run: `jupyter lab --no-browser --ip=0.0.0.0 --port=9000`
- On the local device run: `ssh -NL 1234:localhost:9000 remote_user@ip key-pair.pem`
- On the local machine on a browser go to: http://localhost:1234/

1234: port to use on local device

9000: port to use on remote device