#!/usr/bin/env bash

echo "simple $1"
myfunc(){

  if [[ "$1" != "--all" && "$1" != "--target" ]];
  then
    echo "use parameter: --all  (key displays the IP addresses and symbolic names of all hosts in the current subnet)"
    echo "use parameter: --target  (key displays a list of open system TCP ports)"
  else
    echo "invalid $1 and ...."
  fi
}

myfunc $1
