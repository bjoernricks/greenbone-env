# greenbone-env

Create an environment for Greenbone/OpenVAS development. This allows to use different versions of OpenVAS at the same
time by seperating the install directory. Highly inspired by [virtualenv](https://github.com/pypa/virtualenv/) for python.

## Install

Clone the repo and run 
```bash
$ path/to/greenbone-env <path/to/env>
```
e.g.
```bash
$ ~/git/greenbon-env/greenbon-env ~/install/master-with-postgres
```
to create a new environment. At the specified environment directory **greenbone-env** adds an *activate* script which must be
sourced to get into the environment.

Running
```bash
$ source path/to/env/activate
```
e.g 
```bash
$ source ~/install/master-with-postgres
```
will start the environment. Afterwards you will get a prompt like
```bash
(env: master-with-postgres) $
```

The environment can be terminated by running
```bash
(env: myenv) $ deactivate
```

## Usage

The *activate* scripts sets some shell environment variables to be able to separate installations. These environment variables
should be used wenn configuring the Greenbone/OpenVAS repos. E.g. to configure [openvas-scanner](https://github.com/greenbone/openvas-scanner/) to be installed within the environment use the following commands:

```bash
(env: myenv) $ cd path/to/scanner-clone
(env: myenv) $ mkdir build
(env: myenv) $ cd build
(env: myenv) $ cmake -DCMAKE_INSTALL_PREFIX=$INSTALL_PREFIX ..
(env: myenv) $ make
(env: myenv) $ make install
```
