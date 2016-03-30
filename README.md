# HelloFSharp

Use Visual Studio to create a new F# console application

Install Paket https://fsprojects.github.io/Paket/getting-started.html

Install Suave

Create paket.dependencies in solution folder:

source https://nuget.org/api/v2
nuget Suave

Create paket.references in project folder

Suave

Program.fs:

open Suave

startWebServer defaultConfig (Successful.OK "Hello World!")

Browse to http://localhost:8083/