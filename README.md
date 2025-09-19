# Golang library of OpenPBS

**This is not an official Paratera product**

This is a thin Go wrapper around the C library (libpbs) for the [OpenPBS resource manager]

## 1.Requirements

## 1.1.OS

You must install some requirements on CentOS 7.

```bash
# yum groupinstall "Development Tools" -y
# yum install -y sudo tar wget openssh-server openssh-clients openssl openssl-devel
# yum install -y gcc make rpm-build libtool hwloc-devel libX11-devel libXt-devel libedit-devel libical-devel ncurses-devel perl postgresql-devel python-devel tcl-devel tk-devel swig expat-devel libXext libXft autoconf automake
# yum install -y expat libedit postgresql-server python sendmail tcl tk libical
```

And on CentOS 8 Stream

```bash
# yum groupinstall "Development Tools" -y
# yum install -y sudo tar wget openssh-server openssh-clients openssl openssl-devel
# yum install --enablerepo powertools -y gcc make rpm-build libtool hwloc-devel libX11-devel libXt-devel libedit-devel libical-devel ncurses-devel perl postgresql-devel python3-devel tcl-devel tk-devel swig expat-devel libXext libXft autoconf automake
#
```

## 1.2.Download && Build OpenPBS

Download OpenPBS

```bash
# git clone https://github.com/openpbs/openpbs
# ./autogen.sh
# ./configure --prefix=/opt/pbs
# make -j4
# make install
```

## 1.3.Environment

```bash
# export LD_LIBRARY_PATH=/opt/pbs/lib
# export PBS_EXEC=/opt/pbs
# export PBS_SERVER=pm01
# export PBS_HOME=/opt/pbs
```

## 1.4.PBSpro Cluster

A PBSpro Cluster to test.


## 2.Install

```bash
# go get github.com/mrobbert/go_pbspro
```

## 3. Usage

```go
    package main

    import (
        "github.com/mrobbert/go_pbspro"
        "log"
    )

    func main() {
            qstat, err := NewQstat("172.18.7.10")
        	if err != nil {
        		t.Error(err)
        	}
        
        	qstat.SetAttribs(nil)
        	qstat.SetExtend("")
        
        	err = qstat.ConnectPBS()
        	if err != nil {
        		fmt.Println("ConnectPBS Error")
        		t.Error(err)
        	}
        
        	err = qstat.PbsServerState()
        	if err != nil {
        		fmt.Println(err.Error())
        	}
        	//Print Server State Informations.
        	fmt.Println(qstat.ServerState)
        
        	err = qstat.DisconnectPBS()
        	if err != nil {
        		fmt.Println("DisconnectPBS Error")
        		t.Error(err)
            }
        // ...
    }
```
