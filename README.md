# greenbone-env

## The problem

You need to develop/test/work on different versions/branches/features of the
GVM/OpenVAS modules, it's difficult to track where these versions are installed
and you have to adjust all the paths manually.

## Solution

Create an environment for Greenbone/OpenVAS development. This allows to use
different versions of OpenVAS at the same time by seperating the install
directory. Highly inspired by [virtualenv](https://github.com/pypa/virtualenv/)
for python.

## Install

**greenbone-env** requires Python 3 to be installed.

Clone the repo and run
```bash
$ path/to/greenbone-env <path/to/env>
```
e.g.
```bash
$ ~/git/greenbon-env/greenbon-env ~/install/master-with-postgres
```
to create a new environment. At the specified environment directory
**greenbone-env** adds an *activate* script which must be sourced to get into
the environment.

Running
```bash
$ source path/to/env/bin/activate
```
e.g 
```bash
$ source ~/install/master-with-postgres/bin/activate
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

The *activate* script sets some shell environment variables and shell aliases
to be able to separate installations. These environment variables will be used
when configuring the GVM/OpenVAS repos. E.g. to configure
[openvas-scanner](https://github.com/greenbone/openvas-scanner/) to be installed
within the environment use the following commands:

```bash
(env: myenv) $ mkdir build
(env: myenv) $ cd build
(env: myenv) $ cmake path/to/scanner-git-repo-clone
(env: myenv) $ make
(env: myenv) $ make install
```

The *build* script even simplifies the steps to build a specific GVM/OpenVAS
module. By passing a second parameter to **greenbone-env** it is possible to
customize the source prefix directory where the source of the modules can be
found. The third parameter sets the build prefix directory.

```bash
$ path/to/greenbone-env <path/to/env> <path/to/sources> <path/to/builds>
```

e.g.
```bash
$ ~/git/greenbon-env/greenbon-env ~/install/master-with-postgres ~/sources ~/builds
```

Afterward a module can be build with
```bash
(env: myenv) $ build <modulename>
```

e.g.
```bash
(env: myenv) $ build gvm
```

Example:

```bash
$ ~/git/greenbon-env/greenbon-env ~/install/my-env ~/sources ~/builds
$ source ~/install/my-env/bin/activate
(env: myenv) $ build gvm
```

will build gvm from ~/source/gvm in ~/builds/gvm and installs to ~/my-env.
