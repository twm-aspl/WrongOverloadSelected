# Suspect wrong overload selected by Fable

This reproduces an issue I've encountered while trying to use the Aether library in a Fable client.

The same F# code is producing different results on the server vs. the client.

I've raised the issue on the Gitter forum and the consensus seems to be that Fable is selecting the wrong overload method:

"It looks like fable is selecting the wrong overload for the >?> operator between Child.g_ and Grandchild.x_. Stepping through in rider, the selected overload is static member (>?>) (Prism, (g2, s2): Prism<'b,'c>) which calls Option.bind and so returns Grandchild.x directly, but the emitted javascript selects overload static member (>?>) (Prism, (g2, s2): Lens<'b,'c>) which calls Option.map, which results in Some g.x and so in test3 produces Some None (i.e.: "Some null")...once I patched the javascript to use the other overload, i got the expected output"


* The essential test code is in Shared.fs.
* The file Optics.fs is straight from https://github.com/xyncro/aether


## Install pre-requisites

You'll need to install the following pre-requisites in order to build SAFE applications

* The [.NET Core SDK](https://www.microsoft.com/net/download)
* The [Yarn](https://yarnpkg.com/lang/en/docs/install/) package manager (you can also use `npm` but the usage of `yarn` is encouraged).
* [Node LTS](https://nodejs.org/en/download/) installed for the front end components.
* If you're running on OSX or Linux, you'll also need to install [Mono](https://www.mono-project.com/docs/getting-started/install/).

## Work with the application

Before you run the project **for the first time only** you should install its local tools with this command:

```bash
dotnet tool restore
```


To concurrently run the server and the client components in watch mode use the following command:

```bash
dotnet fake build -t run
```


## SAFE Stack Documentation

You will find more documentation about the used F# components at the following places:

* [Saturn](https://saturnframework.org/docs/)
* [Fable](https://fable.io/docs/)
* [Elmish](https://elmish.github.io/elmish/)

If you want to know more about the full Azure Stack and all of it's components (including Azure) visit the official [SAFE documentation](https://safe-stack.github.io/docs/).
