# HSDS and nrel-rex setup
 
### to get NREL WTK, NSRDB, Sup3rCC, etc. data from AWS we need HSDS and nrel-rex

### instructions on setting up HSDS are taken/adjusted from

https://nrel.github.io/rex/misc/examples.hsds.html#

https://github.com/HDFGroup/hsds 

### create coda env

```
conda create --name rex python=3.11 numpy pandas jupyter plotly h5py
conda activate rex
pip install nrel-rex[hsds]>=0.2.88
pip install tables
```

**_NOTE_** `tables` are optional to saving df's as .h5 (much faster read/write than .csv's for large amounts of data)


### HSDS instructions below are for a mac OS.  

### in your ~/.bash_profile add these lines
```
export AWS_S3_GATEWAY=http://s3.us-west-2.amazonaws.com
export AWS_S3_NO_SIGN_REQUEST=1
```

### create a HSDS configuration file at ~/.hscfg with these lines:
```
# Local HSDS server
hs_endpoint = http://localhost:5101
hs_bucket = nrel-pds-hsds
```

### in rex conda env start your server
```
conda activate rex
hsds
```


### you should see:
```
...
INFO:root:all processes ready!
INFO:root:Ready after: 5.02 s

READY! use endpoint: http://localhost:5101
```

### start NEW terminal, activate conda rex env, and check server state
```
conda activate rex
hsinfo

```

### you should see something like:
```
server name: Highly Scalable Data Service (HSDS)
server state: READY
endpoint: http://localhost:5101
username: anonymous 
password: 
server version: 0.8.4
node count: 4
up: 4 min 22 sec
h5pyd version: 0.18.0

```

### to browse AWS NREL data directory tree use hsls CLI

```
hsls /nrel/
hsls /nrel/wtk/
hsls /nrel/sup3rcc/
...
```

**_NOTE_** more CLI comands at: https://github.com/HDFGroup/hsds_examples

### now we can use *rex_tutorial.ipynb* notebook to browse and retrieve AWS NREL datasets






