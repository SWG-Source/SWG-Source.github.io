---
title: Building SWG with ANT
---
# Building SWG with ANT

We now use Apache Ant to build the SWG codebase.  Apache Ant is a scripting tool that is specifically made to build software projects into usable applications.  You can find out more here: https://ant.apache.org/

The way Ant works is by calling it from the command line in this format:

`ant <target>`

The "ant" part tells Ant to start building.  The <target> is a representation of which thing or series of things you want to build.  You may specify more than one target.  Each target tells Ant to do a specific thing.  Each target is defined in the `build.xml` file.

The reason why Ant was chosen is for the flexibility to build only a small part that a developer may be working on.  For example, Chat... or Java... or maybe the server code in C++.  It's not necessary to build the entire SWG application so we divided these things up into many targets.  For example, if a user wanted to re-build JUST the Chat application, they could simply call Ant with the "compile_chat" target as defined in the build.xml file like so:

`ant compile_chat`

Additionally, you could also choose to compile the chat application (compile_chat) as well as rebuild the Java scripting files (compile_java) like so:

`ant compile_chat compile_java`

This command would first compile the Station API chat application then when finished, if successful, it would re-compile the Java scripting files.

However, if you simply want to rebuild the entire application, you can make a very simple call as so:

`ant swg`

The SWG target has a dependency on all other targets that tell Ant, "hey, I have to rebuild all this stuff and populate the database, etc." and makes subsequent calls to all targets that are a dependency for `swg` to call itself complete.

Here are the many targets and what they do:

* `swg` - Will rebuild the entire SWG application from start to finish.  This is the one-step does all button.
* `clean` - Will delete the compiled SRC files (the EXE's), then will also delete the entire `data` directory and will remove any symbolic links that are created when building.  It's basically a "start at ground zero" command.
* `clean_src` - Deletes compiled SRC files.
* `clean_dsrc` - Deletes the entire `data` directory.
* `clean_java` - Deletes ONLY the `script` directory where the compiled Java class files live.
* `git_update_submods` - Performs a GIT checkout on the submodule directories in `swg-main` - basically just checks out code from the git repositories.
* `update_configs` - Updates the configuration files for SWG and sets the necessary wildcards to your machine specific settings.  This is only required once and won't do anything running more than once unless you have fresh .cfg files.
* `compile_src` - Will compile the SRC C++ files into EXE binaries (only considers files that are needed to be compiled).
* `compile_chat` - Will compile the Station API chat application (only considers files that are needed to be compiled).
* `compile_java` - Will compile the Java scripting files (stored in the script directory - only considers files that are needed to be compiled).
* `compile` - Will compile all new or changed SRC, Java, Station API, Miff, Tab, TPF files - essentially the NUKE option for compiling files.  Not detrimental - unless you didn't want your changes in the game.
* `compile_tab` - Will compile only new or changed TAB files.
* `compile_miff` - Will compile only new or changed MIF files.
* `compile_tpf` - Will compile only new or changed TPF files.
* `build_object_template_crc` - Will create a new Object Template CRC file (useful when adding new things to the game) and will automatically make sure all TPF and MIF files have also been compiled before doing so.
* `build_quest_crc` - Will create a new Quest CRC file and will automaticaly make sure all TAB files have been compiled as well.
* `load_templates` - Will make sure all CRC files are built (and their requirements met) and will load them into the database such that the server can use them.
* `create_database` - Will create a new database (don't use this if you already have a database created).
* `drop_database` - Will absolutely remove any data you have in the game and set you to a starting point to create a new database - You will get a confirmation message when doing this, but yea, don't do it unless you really want to start fresh.  Very handy if you do though.
* `start` - Starts the SWG application.
* `stop` - Completely hard stops the SWG application (not recommended if you're running a usable server).
