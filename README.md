https://towardsdatascience.com/net-core-api-for-the-angular-tour-of-heroes-app-5895a36d2129

Used above guide

API handles http requests from app to docker database. Docker database for some reason isn't working for me. The API seems to be hanlding requests just fine though, and the App is still working.

To configure the app, go to Acute-hero/src/app/hero.service.ts and change private heroesURL to the endpoint of which the api is listening to.

To configure the api, go to Heroes.API/Startup.cs

go to public void ConfigureServices

change DockerDB in

services.AddDbContext<HeroesContext>(options =>
options.UseSqlServer(Configuration.GetConnectionString("DockerDB")));

to whatever name you want. ${database}

go to appsettings.json
go to "ConnectionStrings"

"ConnectionStrings": {
    "${name}": "Server=${server},${port};Database={DbName};User ID=SA;Password=${Password}"
  }

Quick things to note.
In the HeroesController in Heroes.API/Controllers, notice how the data set initialized matches
the name of what the DockerDB's databse is supposed to be named. This file manages the requests/connections between the API and database.