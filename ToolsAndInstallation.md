# Architecture Components (past and present)

We have, at some point in time, used the following tools:

1. Clojure (using leiningen as a platform/dependency manager)
2. Morse (data visualizer, can run code, and can be quite customizable) Morse has the ability to customize views, using JavaFX as a GUI platform, that allows for user controlled dispay of information in an environment.
3. Transcriptor: This is a 3rd party library designed to run files and log output and process the forms and the environment of the file.
4. nREPL: This is a more customizable version of REPL that is more extensible and customizable, though it is a bit of a legacy tool, and we want to move away from using it. Leiningen uses an nREPL environment by default.
5. Clojure subrepls (via clojure.main/repl): This is a core language feature that allows for the instantiation of a new REPL in the current environment, but exposes various function hooks for customizing the behavior of the REPL environment.
As of this point (9/26/24), we are trying to remove the utilization of nREPL, transcriptor, which we have for the most part been able to accomplish.
Additionally, the current iteration of the tool does not use the transcriptor either, since it is built on top of the existing clojure.main/repl function to extend the REPL environment. The transcriptor, instead, is used to load a file into the transcriptor.

## Project Packaging and Installation instructions

This is for taking the babel project and packaging it into a jar for using as a dependency of other projects.

1. From the babel project, in the main directory, run the following commmands
   1. `lein pom` This updates the pom file for the project.
   2. `lein jar` This packages the project into a jar file for running.
   3. `lein install` This installs the project locally so that it can be used as a dependency in other projects.
2. At this point, the package should be installed locally on the computer, and so to use it in another project,
   you can load this into the project, in the `project.clj` of the new project add the following:
   `:dependencies [babel2 "0.1.0-SNAPSHOT"]`.

### To run babel in the new project

1. Make sure that babel is loaded into the project.
2. Run a REPL environment in the project folder with `lein repl`
3. Load the namespace with `(require '[babel2.core :as babel])` as a standalone line. **This will give an execution error, but it is necessary, and everything else will eventually work.**
4. Now, a babel REPL can be run with `(babel/run-in-repl)` will load a babel environment.

### Deploying to Clojars

When we eventually want to deploy Bable to Clojars, the following links/tutorials should be helpful.

1. [clojars.org](https://clojars.org)
2. [clojars tutorial](https://github.com/clojars/clojars-web/wiki/Tutorial)
