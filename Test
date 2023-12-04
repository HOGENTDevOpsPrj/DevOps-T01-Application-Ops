#!/bin/bash

expected_directory="/gitrepo"

current_directory="$(pwd)"

if [ "$current_directory" != "$expected_directory" ]; then
  echo 'Go to the GIT directory'
  cd /gitrepo 
  $SHELL
  
fi

if [ -n "$(docker ps -f "name=db" -f "status=running" -q )" ] ; then docker rm -f db
fi

if [ -n "$(docker ps -f "name=web" -f "status=running" -q )" ] ; then docker rm -f web
fi

echo "Building.."
docker compose build
	
echo "Testing.."
dotnet restore /src/Server/Server.csproj

echo 'Docker container down'
docker compose down

echo 'Docker container up'
docker compose up -d

exit
