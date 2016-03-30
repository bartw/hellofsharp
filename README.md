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

## Nancy

https://github.com/NancyFx/Nancy/wiki/Hosting-Nancy-with-Suave.IO

1. Add "nuget Nancy.Owin" to paket.dependencies

2. Add "Nancy.Owin" to paket.references

3. Create sample app in Program.fs

	```fsharp
	namespace Suave.NancyFx

	open Suave
	open Suave.Owin
	open Nancy
	open Nancy.Owin

	type App() as x =
	  inherit NancyModule()
	  do
		x.Get.["/"] <- fun _ -> "Hello World, from NancyFx on Suave!" :> obj
		x.Get.["/fsharp"] <- fun _ -> "I can into F#" :> obj
		x.Get.["/json"] <- fun _ -> x.Response.AsJson([ "Test" ]) :> obj
		x.Get.["/complex"] <- fun _ -> 
		  let response = x.Response.AsJson(["This is my Response"])
		  response.ContentType <- "application/json"
		  response.Headers.Add("Funky-Header", "Funky-Header-Value")
		  response :> obj

	module Program =

	  [<EntryPoint>]
	  let main argv =
		let opts = new NancyOptions()
		let app = OwinApp.ofMidFunc "/" (NancyMiddleware.UseNancy(opts))
		startWebServer defaultConfig app
		0
	```

5. Browse to http://localhost:8083/, http://localhost:8083/fsharp, http://localhost:8083/json, http://localhost:8083/complex.