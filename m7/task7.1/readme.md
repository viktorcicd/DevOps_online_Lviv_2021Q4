 ### Part 1
 
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
    echo "please enter local subnet address: "
    read x
    allip $x
  else
    allports
  fi
}
```
The --all key displays the IP addresses and symbolic names of all hosts in the current subnet:
```
allip(){
  printf "IPs and names: \n`nmap -sn $x/24 | awk '/report/{print $5,$6}'`\n"
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


 ### Part 2
 
 1. Script for: From which ip were the most requests?
```
cat apache_logs.txt | awk '{print $1}' | sort | uniq -c | sort -nr | head -1 | awk '{print $2}'
```
2. What is the most requested page?
```

```
3. How many requests were there from each ip?
```
cat apache_logs.txt | awk '{print $1}' | sort | uniq -c | sort -nr | awk '{print "quantity = "$1 ",  IP = "$2}'
```
4. What non-existent pages were clients referred to?
```
cat apache_logs.txt | awk '/error/{print $7}'
```
5. What time did site get the most requests?
```

```
6. What search bots have accessed the site? (UA + IP)
```

```

