SouthWorks Project

In this repository there is a web API as an example created with ASP.NET Core.

INSTRUCTIONS TO RUN THE APP ON DOCKER

Follow these steps to "Dockerize" your App correctly.

At first you need to create a new file without extension called "Dockerfile" (without quotes) and you're going to copy this code:

FROM microsoft/dotnet:2.1-sdk AS builder
WORKDIR /app
# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore
# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out
# Build runtime image
FROM microsoft/dotnet:2.1-sdk
WORKDIR /app
COPY - from=builder /app/out .
ENTRYPOINT ["dotnet", "southworks.dll"]

Docker also allows you to ignore certains folders or files that are not being used on the build, all you have to do is create a file 
in the project folder (in the same folder where the "Dockerfile" without extension is) with any name you desire and a extension
"title.dockerignore" with this content: 

bin\
obj\

Now you've got the files properly located, we are going to open the command prompt (CMD) and navigate to your project 
folder < cd C:/ "app_folder" >, once you get there put on the prompt:

docker build -t southworks .

After the creation of the image to dockerize your app type this command:

docker run -d -p 8080:80 - name myapp southworks

Now all you have to do is to open your default browser and type in the address bar:

localhost:8080

You have now your app open with docker and it's ready to transport to any other computer with Docker to run it!

Thanks for reading this and good luck!!

