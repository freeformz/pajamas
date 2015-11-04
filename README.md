# Migration Example App

This app doesn't contain any migrations, but is an example of using [migrate][migrate] with [godep][godep] and [heroku][heroku].

[godep][godep] only includes files from packages imported in your code. When we want to use a migration tool to help automate database migrations we don't have easy access to the cli commands they provide in the dyno. It's sub optimal to have to run those commands from a local system.

Luckily most of the migration tools are fairly well factored and you can lift their main cli bits out of their packages and into your application. This repo is an example of that.

Using `github.com/mattes/migrate` as an example this repo was constructed by doing the following:

1. `cd <your app>`
1. Write your code. Simulated with a simple `main.go` here.
1. `go get -u github.com/mattes/migrate`
1. `mkdir -p cmd/migrate`
1. `cp $GOPATH/src/github.com/mattes/migrate/{main,version}.go cmd/migrate`
1. `godep save -r ./...`
1. `git add -A .`
1. `git commit -am "includes migration"`
1. `git push heroku master`

FWIW: I consider this a workaround looking for a better, longer term solution.

[migrate]: https://github.com/mattes/migrate
[godep]: https://github.com/tools/godep
[heroku]: https://heroku.com
