# Scala - libGDX and IntelliJ
## Simple set up guide

And finally I decided to give Scala a good run. Obviously I wanted to have fun along the way and making a game is always fun. The first step in any language learning process, the setup phase, is often the most daunting one.
So to keep my notes I scribbled down the following.

Using the following introduction to set up a project structure

[http://raintomorrow.cc/post/70000607238/develop-games-in-scala-with-libgdx-getting-started](http://raintomorrow.cc/post/70000607238/develop-games-in-scala-with-libgdx-getting-started)


The following is needed:
scala
sbt (simple build tool)
consscript (tool for installing and updating scala programs)

    brew install scala
    brew install sbt

## Creating a game from a template
First we'll install ``conscript`` and ``giter8`` to download and generate the needed files and directories for our libGDX game

    curl https://raw.github.com/n8han/conscript/master/setup.sh | sh
    cs n8han/giter8


Now when it's done it's time to create the game template

    g8 ajhager/libgdx-sbt-project
    package [my.game.pkg]: se.vojd.bouncer
    name [My Game]: Bouncer
    scala_version [2.10.3]:
    api_level [19]:
    libgdx_version [0.9.9]:

    Template applied in ./bouncer

The project template is finished, time to update the dependencies with ``sbt``

    sbt 
    >  update


## Configuring Android SDK Paths
If you encounter the following:

    [error] Android SDK not found. You might need to set ANDROID_SDK_HOME or ANDROID_SDK_ROOT or ANDROID_HOME

Add the following to your .bash_profile

    export ANDROID_SDK_HOME="/Users/mathias/dev/android_sdk/sdk"

## Create IntelliJ project
Replace ``project/plugins.sbt`` with the following

    resolvers += Resolver.url($
    "scalasbt snapshots", new URL("http://repo.scala-sbt.org/scalasbt/sbt-plugin-snapshots"))(Resolve>
    addSbtPlugin("org.scala-sbt" % "sbt-android" % "0.7")$
    addSbtPlugin("com.hagerbot" % "sbt-robovm" % "0.1.0-SNAPSHOT")$
    addSbtPlugin("com.github.mpeltonen" % "sbt-idea" % "1.5.2")$
    libraryDependencies += "commons-io" % "commons-io" % "2.0"$

Now we have specified the plugin to use with IntelliJ and can successfully create the IntelliJ project

   sbt gen-idea


Open the project in IntelliJ and start the game hacking! Almost...
## Nested module error in IntelliJ
You might stumble upon this error when adding a library to the project
``/path/common/assets/ root already belongs to nested module "desktop"``
To fix this problem, open ``Project Structure`` from the ``File`` menu, navigate to ``Modules``, check the ``desktop`` module and uncheck all red source folders. Mark ``src/main/scala`` as ``Sources`` and check Apply. This should do the trick.




