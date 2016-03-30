# HelloFSharp

## hello world

1. Use Visual Studio to create a new F# console application

2. Install Paket https://fsprojects.github.io/Paket/getting-started.html

3. Install Suave

Create paket.dependencies in solution folder:

```
source https://nuget.org/api/v2
nuget Suave
```

Create paket.references in project folder

```
Suave
```

4. Create hello world in Program.fs

```fsharp
open Suave

startWebServer defaultConfig (Successful.OK "Hello World!")
```

5. Browse to http://localhost:8083/