 Create a script with a separate functions that uses the following keys:
 
 "without parameters", --all key, --target key


```
#!/usr/bin/env bash

myfunc(){
  if [[ "$1" != "--all" && "$1" != "--target" ]];
  then
    echo "use parameter: --all  (key displays the IP addresses and symbolic names of all hosts in the current subnet)"
    echo "use parameter: --target  (key displays a list of open system TCP ports)"
  elif [ "$1" == "--all" ];
  then
    allip
  else
    allports
  fi
}
```
The --all key displays the IP addresses and symbolic names of all hosts in the current subnet:
```
allip(){
  printf "IPs and names: \n`nmap -sn 192.168.31.1/24 | awk '/report/{print $5,$6}'`\n"
}
```
The --target key displays a list of open system TCP ports:
```
allports(){
  printf "Open ports: \n`netstat -tuna | awk -F: '/tcp/{print $2}' | awk '{print $1}'`\n"
}

myfunc $1
```

And check the results:


![functions](./images/16.png "functions")
