# Hadoop 

# Quick install Hadoop

## Step 1 - **Environmental Preparation**

- ubuntu 22.04
- OpenJDK 11
- OpenSSH
- net-tools
- sshpass
    - Automatically install packages if they are not installed

🔸**NameNode**

- Change public key authentication to password-based authentication
- git install
- git clone
    - Git clone for Script Execution

🔸**DataNode**

- Change public key authentication to password-based authentication
- ubuntu passwd
    - Ubuntu Account Password Settings

> ### ❗****Caution****❗
>
> 1. Proceed on **all DataNode’s** unconditionally changing public key authentication to password-based authentication
> 2. **All DataNode’s** ubuntu account set passwords

### ▶**Execute**

🔹NameNode

```java
sudo sed -i "/PasswordAuthentication/ c\PasswordAuthentication yes" /etc/ssh/sshd_config
sudo systemctl restart sshd

sudo apt-get install git
git clone https://github.com/boanlab/aporrima.git
```

🔹DataNode

```java
sudo sed -i "/PasswordAuthentication/ c\PasswordAuthentication yes" /etc/ssh/sshd_config
sudo systemctl restart sshd

sudo passwd ubuntu
```

Input the Ubuntu password you want `ex. ubuntu`

## Step 2 - Install Hadoop & Preparing for Hadoop Start

**2 versions - (password set by sudo passwdu ubuntu)**

1. DataNode's ubuntu account **password is not `ubuntu`**
2. DataNode's ubuntu account **password is `ubuntu`**

> ### ❗****Caution****❗
> 
> 1. When executing the account password ubuntu, the password for **all DataNodes must be `ubuntu`.**
>     - If even one node is different, that node cannot be connected
> 2. **The order** in which the ip addresses are inputed is important
>     - You have to **start with NameNode.**
>     - You don't have to input the password after NameNode.

### ▶**Execute**

1. **DataNode's ubuntu account password is not `ubuntu`**
    
    🔹General Example
    
    ```java
    ./aporrima/hadoop/1.sh (NameNode's ip address) (DataNode's ip address) (DataNode's ubuntu passwd) (DataNode's ip address) (DataNode's ubuntu passwd)...
    ```
    
    🔹Real Example
    
    ```java
    ./aporrima/hadoop/1.sh 10.0.20.157 10.0.20.180 ubuntu 10.0.20.181 ubuntu2
    ```
    
2. **DataNode's ubuntu account password is `ubuntu`**
    
    🔹General Example
    
    ```java
    ./aporrima/hadoop/v2.sh (NameNode's ip address) (DataNode's ip address) (DataNode's ip address)...
    ```
    
    🔹Real Example
    
    ```java
    ./aporrima/hadoop/v2.sh 10.0.20.157 10.0.20.180 10.0.20.181
    ```
    

## Step 3 - Starting Hadoop

You just have to enter the following command in NameNode’s hadoop account

`hdfs namenode -format`

`./hadoop/sbin/start-dfs.sh`

`./hadoop/sbin/start-yarn.sh`  
  
    
# How to add DataNode

Use when you want to **add Datanode after installation**  
**Only one Datanode** can be added per execute

> ### **❗Caution❗**
> 
> 1. The hadoop installation must have been **successful**.
> 2. Must proceed from **ubuntu account**
> 3. **DataNode preset** required

### ****▶Execute****

1. **DataNode preset**

🔹DataNode

```
sudo sed -i "/PasswordAuthentication/ c\PasswordAuthentication yes" /etc/ssh/sshd_config
sudo systemctl restart sshd

sudo passwd ubuntu
```

2. **Proceed from NameNode's ubuntu account**

🔹General Example

```
./aporrima/hadoop/addDataNode.sh (DataNode's ip address) (DataNode's ubuntu passwd)
```

🔹Real Example

```
./aporrima/hadoop/addDataNode.sh 10.0.20.180 ubuntu
```
