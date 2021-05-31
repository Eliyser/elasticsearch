Contributing to elasticsearch
=============================

Elasticsearch is a free and open project and we love to receive contributions from our community — you! There are many ways to contribute, from writing tutorials or blog posts, improving the documentation, submitting bug reports and feature requests or writing code which can be incorporated into Elasticsearch itself.

If you want to be rewarded for your contributions, sign up for the [Elastic Contributor Program](https://www.elastic.co/community/contributor). Each time you
make a valid contribution, you’ll earn points that increase your chances of winning prizes and being recognized as a top contributor.

Bug reports
-----------

If you think you have found a bug in Elasticsearch, first make sure that you are testing against the [latest version of Elasticsearch](https://www.elastic.co/downloads/elasticsearch) - your issue may already have been fixed. If not, search our [issues list](https://github.com/elastic/elasticsearch/issues) on GitHub in case a similar issue has already been opened.

It is very helpful if you can prepare a reproduction of the bug. In other words, provide a small test case which we can run to confirm your bug. It makes it easier to find the problem and to fix it. Test cases should be provided as `curl` commands which we can copy and paste into a terminal to run it locally, for example:

```sh
# delete the index
curl -XDELETE localhost:9200/test

# insert a document
curl -XPUT localhost:9200/test/test/1 -d '{
 "title": "test document"
}'

# this should return XXXX but instead returns YYY
curl ....
```

Provide as much information as you can. You may think that the problem lies with your query, when actually it depends on how your data is indexed. The easier it is for us to recreate your problem, the faster it is likely to be fixed.

Feature requests
----------------

If you find yourself wishing for a feature that doesn't exist in Elasticsearch, you are probably not alone. There are bound to be others out there with similar needs. Many of the features that Elasticsearch has today have been added because our users saw the need.
Open an issue on our [issues list](https://github.com/elastic/elasticsearch/issues) on GitHub which describes the feature you would like to see, why you need it, and how it should work.

Contributing code and documentation changes
-------------------------------------------

If you would like to contribute a new feature or a bug fix to Elasticsearch,
please discuss your idea first on the Github issue. If there is no Github issue
for your idea, please open one. It may be that somebody is already working on
it, or that there are particular complexities that you should know about before
starting the implementation. There are often a number of ways to fix a problem
and it is important to find the right approach before spending time on a PR
that cannot be merged.

We add the `help wanted` label to existing Github issues for which community
contributions are particularly welcome, and we use the `good first issue` label
to mark issues that we think will be suitable for new contributors.

The process for contributing to any of the [Elastic repositories](https://github.com/elastic/) is similar. Details for individual projects can be found below.

### Fork and clone the repository

You will need to fork the main Elasticsearch code or documentation repository and clone it to your local machine. See
[github help page](https://help.github.com/articles/fork-a-repo) for help.

Further instructions for specific projects are given below.

### Tips for code changes
Following these tips prior to raising a pull request will speed up the review
cycle.

* Add appropriate unit tests (details on writing tests can be found in the
  [TESTING](TESTING.asciidoc) file)
* Add integration tests, if applicable
* Make sure the code you add follows the [formatting guidelines](#java-language-formatting-guidelines)
* Lines that are not part of your change should not be edited (e.g. don't format
  unchanged lines, don't reorder existing imports)
* Add the appropriate [license headers](#license-headers) to any new files

### Submitting your changes

Once your changes and tests are ready to submit for review:

1. Test your changes

    Run the test suite to make sure that nothing is broken. See the
[TESTING](TESTING.asciidoc) file for help running tests.

2. Sign the Contributor License Agreement

    Please make sure you have signed our [Contributor License Agreement](https://www.elastic.co/contributor-agreement/). We are not asking you to assign copyright to us, but to give us the right to distribute your code without restriction. We ask this of all contributors in order to assure our users of the origin and continuing existence of the code. You only need to sign the CLA once.

3. Rebase your changes

    Update your local repository with the most recent code from the main Elasticsearch repository, and rebase your branch on top of the latest master branch. We prefer your initial changes to be squashed into a single commit. Later, if we ask you to make changes, add them as separate commits.  This makes them easier to review.  As a final step before merging we will either ask you to squash all commits yourself or we'll do it for you.


4. Submit a pull request

    Push your local changes to your forked copy of the repository and [submit a pull request](https://help.github.com/articles/using-pull-requests). In the pull request, choose a title which sums up the changes that you have made, and in the body provide more details about what your changes do. Also mention the number of the issue where discussion has taken place, eg "Closes #123".

Then sit back and wait. There will probably be discussion about the pull request and, if any changes are needed, we would love to work with you to get your pull request merged into Elasticsearch.

Please adhere to the general guideline that you should never force push
to a publicly shared branch. Once you have opened your pull request, you
should consider your branch publicly shared. Instead of force pushing
you can just add incremental commits; this is generally easier on your
reviewers. If you need to pick up changes from master, you can merge
master into your branch. A reviewer might ask you to rebase a
long-running pull request in which case force pushing is okay for that
request. Note that squashing at the end of the review process should
also not be done, that can be done when the pull request is [integrated
via GitHub](https://github.com/blog/2141-squash-your-commits).

Contributing to the Elasticsearch codebase
------------------------------------------

**Repository:** [https://github.com/elastic/elasticsearch](https://github.com/elastic/elasticsearch)

JDK 15 is required to build Elasticsearch. You must have a JDK 15 installation
with the environment variable `JAVA_HOME` referencing the path to Java home for
your JDK 15 installation. By default, tests use the same runtime as `JAVA_HOME`.
However, since Elasticsearch supports JDK 11, the build supports compiling with
JDK 15 and testing on a JDK 11 runtime; to do this, set `RUNTIME_JAVA_HOME`
pointing to the Java home of a JDK 11 installation. Note that this mechanism can
be used to test against other JDKs as well, this is not only limited to JDK 11.

> Note: It is also required to have `JAVA8_HOME`, `JAVA9_HOME`, `JAVA10_HOME`
and `JAVA11_HOME`, `JAVA12_HOME`, `JAVA13_HOME`, `JAVA14_HOME`, and `JAVA15_HOME`
available so that the tests can pass.

Elasticsearch uses the Gradle wrapper for its build. You can execute Gradle
using the wrapper via the `gradlew` script on Unix systems or `gradlew.bat`
script on Windows in the root of the repository. The examples below show the
usage on Unix.

We support development in IntelliJ versions IntelliJ 2020.1 and
onwards and Eclipse 2020-3 and onwards.

[Docker](https://docs.docker.com/install/) is required for building some Elasticsearch artifacts and executing certain test suites. You can run Elasticsearch without building all the artifacts with:

    ./gradlew :run

That'll spend a while building Elasticsearch and then it'll start Elasticsearch,
writing its log above Gradle's status message. We log a lot of stuff on startup,
specifically these lines tell you that Elasticsearch is ready:

    [2020-05-29T14:50:35,167][INFO ][o.e.h.AbstractHttpServerTransport] [runTask-0] publish_address {127.0.0.1:9200}, bound_addresses {[::1]:9200}, {127.0.0.1:9200}
    [2020-05-29T14:50:35,169][INFO ][o.e.n.Node               ] [runTask-0] started

But to be honest its typically easier to wait until the console stops scrolling
and then run `curl` in another window like this:

    curl -u elastic:password localhost:9200



### Importing the project into IntelliJ IDEA

The minimum IntelliJ IDEA version required to import the Elasticsearch project is 2020.1
Elasticsearch builds using Java 15. When importing into IntelliJ you will need
to define an appropriate SDK. The convention is that **this SDK should be named
"15"** so that the project import will detect it automatically. For more details
on defining an SDK in IntelliJ please refer to [their documentation](https://www.jetbrains.com/help/idea/sdk.html#define-sdk).
SDK definitions are global, so you can add the JDK from any project, or after
project import. Importing with a missing JDK will still work, IntelliJ will
simply report a problem and will refuse to build until resolved.

You can import the Elasticsearch project into IntelliJ IDEA via:

 - Select **File > Open**
 - In the subsequent dialog navigate to the root `build.gradle` file
 - In the subsequent dialog select **Open as Project**

#### Checkstyle

If you have the [Checkstyle] plugin installed, you can configure IntelliJ to
check the Elasticsearch code. However, the Checkstyle configuration file does
not work by default with the IntelliJ plugin, so instead an IDE-specific config
file is generated automatically after IntelliJ finishes syncing. You can
manually generate the file with `./gradlew configureIdeCheckstyle` in case
it is removed due to a `./gradlew clean` or other action.

   1. Open **Preferences > Tools > Checkstyle**
   2. We have some custom Checkstyle rules, and the Checkstyle plugin needs
      to know where to find them. Under the "Third-Party Checks" section,
      click the "+" button.
   3. Select `buildSrc/build-bootstrap/libs/buildSrc-$VERSION.jar` where
      `$VERSION` is something like `7.0.0-SNAPSHOT`. This jar file will
      always exist if you imported the project into IntelliJ before
      configuring Checkstyle.
   4. Make sure that "Checkstyle version" is set to the highest available version
   5. Change the "Scan Scope" to "Only Java sources (including tests)"
   6. Click the "+" under "Configuration file"
   7. Set "Description" to "Elasticsearch"
   8. Select "Use a local Checkstyle file"
   9. For the "File", enter `checkstyle_ide.xml`
   10. Tick "Store relative to project location"
   11. Click "Next", then "Finish".
   12. Click the box next to the new configuration to make it "Active".
       Without doing this, you'll have to explicitly choose the
       "Elasticsearch" configuration in the Checkstyle tool window and run
       the check manually.
   13. Click "OK" to apply the new preferences

#### Formatting

We are in the process of migrating towards automatic formatting Java file
using [spotless], backed by the Eclipse formatter. If you have the [Eclipse
Code Formatter] installed, you can apply formatting directly in IntelliJ.

   1. Open **Preferences > Other Settings > Eclipse Code Formatter**
   2. Click "Use the Eclipse Code Formatter"
   3. Under "Eclipse formatter config", select "Eclipse workspace/project
      folder or config file"
   4. Click "Browse", and navigate to the file `buildSrc/formatterConfig.xml`
   5. **IMPORTANT** - make sure "Optimize Imports" is **NOT** selected.
   6. Click "OK"

Note that only some sub-projects in the Elasticsearch project are currently
fully-formatted. You can see a list of project that **are not**
automatically formatted in [gradle/formatting.gradle](gradle/formatting.gradle).

### REST Endpoint Conventions

Elasticsearch typically uses singular nouns rather than plurals in URLs.
For example:

    /_ingest/pipeline
    /_ingest/pipeline/{id}

but not:

    /_ingest/pipelines
    /_ingest/pipelines/{id}

You may find counterexamples, but new endpoints should use the singular
form.

### Java Language Formatting Guidelines

Java files in the Elasticsearch codebase are formatted with the Eclipse JDT
formatter, using the [Spotless
Gradle](https://github.com/diffplug/spotless/tree/master/plugin-gradle)
plugin. This plugin is configured on a project-by-project basis, via
`build.gradle` in the root of the repository. The formatting check can be
run explicitly with:

    ./gradlew spotlessJavaCheck

The code can be formatted with:

    ./gradlew spotlessApply

These tasks can also be run for specific subprojects, e.g.

    ./gradlew server:spotlessJavaCheck

Please follow these formatting guidelines:

* Java indent is 4 spaces
* Line width is 140 characters
* Lines of code surrounded by `// tag::NAME` and `// end::NAME` comments are included
  in the documentation and should only be 76 characters wide not counting
  leading indentation. Such regions of code are not formatted automatically as
  it is not possible to change the line length rule of the formatter for
  part of a file. Please format such sections sympathetically with the rest
  of the code, while keeping lines to maximum length of 76 characters.
* Wildcard imports (`import foo.bar.baz.*`) are forbidden and will cause
  the build to fail.
* If *absolutely* necessary, you can disable formatting for regions of code
  with the `// tag::NAME` and `// end::NAME` directives, but note that
  these are intended for use in documentation, so please make it clear what
  you have done, and only do this where the benefit clearly outweighs the
  decrease in consistency.
* Note that Javadoc and block comments i.e. `/* ... */` are not formatted,
  but line comments i.e `// ...` are.
* Negative boolean expressions must use the form `foo == false` instead of
  `!foo` for better readability of the code. This is enforced via
  Checkstyle. Conversely, you should not write e.g. `if (foo == true)`, but
  just `if (foo)`.

#### Editor / IDE Support

IntelliJ IDEs can
[import](https://blog.jetbrains.com/idea/2014/01/intellij-idea-13-importing-code-formatter-settings-from-eclipse/)
the same settings file, and / or use the [Eclipse Code
Formatter](https://plugins.jetbrains.com/plugin/6546-eclipse-code-formatter)
plugin.

You can also tell Spotless to [format a specific
file](https://github.com/diffplug/spotless/tree/master/plugin-gradle#can-i-apply-spotless-to-specific-files)
from the command line.

#### Formatting failures

Sometimes Spotless will report a "misbehaving rule which can't make up its
mind" and will recommend enabling the `paddedCell()` setting. If you
enabled this setting and run the format check again,
Spotless will write files to
`$PROJECT/build/spotless-diagnose-java/` to aid diagnosis. It writes
different copies of the formatted files, so that you can see how they
differ and infer what is the problem.

The `paddedCell()` option is disabled for normal operation so that any
misbehaviour is detected, and not just suppressed. You can enabled the
option from the command line by running Gradle with `-Dspotless.paddedcell`.

### Javadoc

Good Javadoc can help with navigating and understanding code. Elasticsearch
has some guidelines around when to write Javadoc and when not to, but note
that we don't want to be overly prescriptive. The intent of these guidelines
is to be helpful, not to turn writing code into a chore.

#### The short version

   1. Always add Javadoc to new code.
   2. Add Javadoc to existing code if you can.
   3. Document the "why", not the "how", unless that's important to the
      "why".
   4. Don't document anything trivial or obvious (e.g. getters and
      setters). In other words, the Javadoc should add some value.

#### The long version

   1. If you add a new Java package, please also add package-level
      Javadoc that explains what the package is for. This can just be a
      reference to a more foundational / parent package if appropriate. An
      example would be a package hierarchy for a new feature or plugin -
      the package docs could explain the purpose of the feature, any
      caveats, and possibly some examples of configuration and usage.
   2. New classes and interfaces must have class-level Javadoc that
      describes their purpose. There are a lot of classes in the
      Elasticsearch repository, and it's easier to navigate when you
      can quickly find out what is the purpose of a class. This doesn't
      apply to inner classes or interfaces, unless you expect them to be
      explicitly used outside their parent class.
   3. New public methods must have Javadoc, because they form part of the
      contract between the class and its consumers. Similarly, new abstract
      methods must have Javadoc because they are part of the contract
      between a class and its subclasses. It's important that contributors
      know why they need to implement a method, and the Javadoc should make
      this clear. You don't need to document a method if it's overriding an
      abstract method (either from an abstract superclass or an interface),
      unless your implementation is doing something "unexpected" e.g. deviating
      from the intent of the original method.
   4. Following on from the above point, please add docs to existing public
      methods if you are editing them, or to abstract methods if you can.
   5. Non-public, non-abstract methods don't require Javadoc, but if you feel
      that adding some would make it easier for other developers to
      understand the code, or why it's written in a particular way, then please
      do so.
   6. Properties don't need to have Javadoc, but please add some if there's
      something useful to say.
   7. Javadoc should not go into low-level implementation details unless
      this is critical to understanding the code e.g. documenting the
      subtleties of the implementation of a private method. The point here
      is that implementations will change over time, and the Javadoc is
      less likely to become out-of-date if it only talks about the what is
      the purpose of the code, not what it does.
   8. Examples in Javadoc can be very useful, so feel free to add some if
      you can reasonably do so i.e. if it takes a whole page of code to set
      up an example, then Javadoc probably isn't the right place for it.
      Longer or more elaborate examples are probably better suited
      to the package docs.
   9. Test methods are a good place to add Javadoc, because you can use it
      to succinctly describe e.g. preconditions, actions and expectations
      of the test, more easily that just using the test name alone. Please
      consider documenting your tests in this way.
   10. Sometimes you shouldn't add Javadoc:
       1. Where it adds no value, for example where a method's
          implementation is trivial such as with getters and setters, or a
          method just delegates to another object.
       2. However, you should still add Javadoc if there are caveats around
          calling a method that are not immediately obvious from reading the
          method's implementation in isolation.
       3. You can omit Javadoc for simple classes, e.g. where they are a
          simple container for some data. However, please consider whether a
          reader might still benefit from some additional background, for
          example about why the class exists at all.
   11. Not all comments need to be Javadoc. Sometimes it will make more
       sense to add comments in a method's body, for example due to important
       implementation decisions or "gotchas". As a general guide, if some
       information forms part of the contract between a method and its callers,
       then it should go in the Javadoc, otherwise you might consider using
       regular comments in the code. Remember as well that Elasticsearch
       has extensive [user documentation](./docs), and it is not the role
       of Javadoc to replace that.
        * If a method's performance is "unexpected" then it's good to call that
           out in the Javadoc. This is especially helpful if the method is usually fast but sometimes
           very slow (shakes fist at caching).
   12. Please still try to make class, method or variable names as
       descriptive and concise as possible, as opposed to relying solely on
       Javadoc to describe something.
   13. Use `@link` to add references to related resources in the codebase. Or
       outside the code base.
       1. `@see` is much more limited than `@link`. You can use it but most of
          the time `@link` flows better.
   14. If you need help writing Javadoc, just ask!

Finally, use your judgement! Base your decisions on what will help other
developers - including yourself, when you come back to some code
3 months in the future, having forgotten how it works.
