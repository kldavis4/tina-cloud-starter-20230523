---
title: 'Using Nothing But Docker For Projects'
slug: using-nothing-but-docker-projects
author: raphael-amoedo
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c9ceed27-0128-4001-b8b7-91aee374a9d5/using-nothing-but-docker-projects.jpg
date: 2022-07-14T07:30:00.000Z
summary: >-
  Using only Docker to build and run applications and commands removes the need for previous knowledge in some tool or programming language. Also, it avoids the necessity to install new modules and dependencies directly to the system, which makes development machine-independent.
description: >-
  Using only Docker to build and run applications and commands removes the need for previous knowledge in some tool or programming language. Also, it avoids the necessity to install new modules and dependencies directly to the system, which makes development machine-independent.
categories:
  - Tools
  - Coding
---

Imagine the following situation: you start working on a new project, maybe also with a different programming language you’re not used to. So, the project is there, and you should be able to run it.

You hope there’s any documentation telling you what to do &mdash; which is not that common &mdash; and if/when there’s any, it usually doesn’t work. You need to know *what* to install, *where* to install it, *how* to set it up, etc. It’s not an uncommon scenario, and you can actually expect that at some point. But what if there was a way to ensure this won’t happen again?

Throughout this post, we’ll see different approaches we could use to make this easier using only Docker.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09e35bd9-d020-4d9b-9f92-28bba104289f/1-using-nothing-but-docker-projects.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09e35bd9-d020-4d9b-9f92-28bba104289f/1-using-nothing-but-docker-projects.jpg" width="800" height="554" sizes="100vw" caption="(Source: <a href='https://www.pngfind.com/mpng/iomTxhb_code-frameworks-docker-programmer-png-transparent-png/'>pngfind.com</a>) (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/09e35bd9-d020-4d9b-9f92-28bba104289f/1-using-nothing-but-docker-projects.jpg'>Large preview</a>)" alt="Programming languages" >}}

## Level One: Using Alias With Docker

### Example With Java + Maven

Let’s consider a Java project, for example. Usually, to run a Java application, you run `java -jar application.jar`.

To generate the `jar` file and manage project dependencies, you can use a lot of different tools, with the most known being Maven and Gradle. Let’s consider Maven for this example. Let’s see some Maven commands:

- `mvn dependency:copy-dependencies`  
Downloads the dependencies if they’re not downloaded yet.
- `mvn package`  
Builds the application and generates the `jar`. It also downloads the dependencies if they’re not downloaded yet. If you want to skip running the tests in the building process, you can also pass the `-Dmaven.test.skip=true` parameter.

Assuming we need Maven 3 and Java 11, that’s how you could use Docker:

<div class="break-out">

<pre><code class="language-bash">alias java='docker run -v "$PWD":/home -w /home openjdk:11-jre-slim java'
alias mvn='docker run -it --rm --name maven -v "$(pwd)":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-11-slim mvn'</code></pre>
</div>

This way, you can run any Maven and Java commands without having to install Java or Maven. You can test the commands by running `java -version` or `mvn -version`. Usually, the official Docker image of these tools gives you instructions on how to run it, and you can just create an alias for that.

#### Pros:

- If you don’t need to use it anymore, you can remove the related Docker image.
- It’s easy to change the version.

#### Cons:

- In this example, you still need to find out what Java version is used and what tool is used (in this case, Maven) and its version.
- If you’re dealing with a programming language you don’t know, it will take even more time to understand what to do.
- You still need to know which commands to run.

It’s a fair approach, especially if you know what you’re doing. But that doesn’t come with the project itself. So, let’s try to improve it a bit.

{{% feature-panel %}}

## Level Two: Using Docker For Running The Application

That’s where [Dockerfile](https://docs.docker.com/engine/reference/builder/) starts to shine. We know how to run commands using only Docker, but how to run the application?

A common Dockerfile for that situation could be:

<pre><code class="language-bash">FROM openjdk:11-jre-slim

ARG JAR&#95;FILE=target/&#42;.jar

ADD ${JAR&#95;FILE} app.jar

ENTRYPOINT ["java", "-jar", "/app.jar"]</code></pre>

And you can build it the way you normally build a docker image, using `docker build -t my-application .`, for example.

You can see that it depends on an existing `JAR` file to build it. As you saw on the previous topic, we know how to generate it, but we would be in trouble if it were another programming language or tool.

It seems like a really minor improvement, but that helps a lot already, as you can see in its pros/cons:

#### Pros

- The Dockerfile should come within the project. So, it tells you already how to run the application regardless of programming language knowledge.
- It also tells you which version and image are being used.
- It inherits the pros from the *Level One* topic if you also apply *Level One* knowledge.

#### Cons

- You still need to find out how to build the application.
- It also means you still need to know which commands to run.

It’s a good approach. You can merge *Level One* and *Level Two* to achieve a better result. The project should have Dockerfile, and life gets a bit easier already. But let’s see how life can be even *easier*.

{{% ad-panel-leaderboard %}}

## Level Three: Using Docker For Building And Running The Application

What if you didn’t know anything about Java and Maven, and you were still able to build the application with just one command you already know?

That’s where [Multi-Stage builds](https://docs.docker.com/develop/develop-images/multistage-build/) shine.

<blockquote>With multi-stage builds, you use multiple `FROM` statements in your Dockerfile. Each `FROM` instruction can use a different base, and each of them begins a new stage of the build. You can selectively copy artifacts from one stage to another, leaving behind everything you don’t want in the final image.</blockquote>

How can that help us? Well, let’s consider the previous Dockerfile. We needed a `JAR` file to build the Docker image. With Multi-Stage Build, Dockerfile itself can be responsible for generating it. In a simple approach, that Dockerfile would look like this:

<div class="break-out">

<pre><code class="language-bash"># ============= DEPENDENCY + BUILD ===========================
# Download the dependencies on container and build application
# ============================================================

FROM maven:3-jdk-11-slim AS builder

COPY ./pom.xml /app/pom.xml
COPY . /app

WORKDIR /app

RUN mvn package $MAVEN&#95;CLI&#95;OPTS -Dmaven.test.skip=true

# ============= DOCKER IMAGE ================
# Prepare container image with application artifacts
# ===========================================

FROM openjdk:11-jre-slim

COPY --from=builder /app/target/&#42;.jar app.jar

ENTRYPOINT ["java", "-jar", "/app.jar"]</code></pre>
</div>

Let’s see what’s happening here.

From the first `FROM` to the first `RUN` statement, it’s doing things related to Maven &mdash; copying the files that need to be copied and running the command that downloads the dependencies and builds the application. It’s doing that by using the `maven:3-jdk-11-slim` image, and it’s setting the name `builder`.

After that, you see the second `FROM` statement using the `openjdk:11-jre-slim` image. You also see a `COPY` statement which copies from a place called `builder`. But what’s that *place*? What’s that *builder*?

That’s the name we set for the Maven image at the first `FROM` statement. It’s copying the `jar` file from that container. So, you can literally play with different `FROM` entries to build whatever you want, and the command to build the Docker image is still the same: `docker build -t my-application .`.

#### Pros:

- Regardless of the programming language, if the project has this approach, you can run the application without installing anything other than Docker.
- It inherits the pros from *Level One* and *Level Two*.

Worth saying that you can also use this Dockerfile with [Docker Compose](https://docs.docker.com/compose/gettingstarted/#step-3-define-services-in-a-compose-file), which can be really powerful, especially if your application needs to expose ports, sharing volumes, or it depends on other images.

{{% ad-panel-leaderboard %}}

## Appendix: Using Docker For Every Major Command

Now that you know how to play with different `FROM` statements, another possible Dockerfile could be:

<div class="break-out">

<pre><code class="language-javascript"># ============= DEPENDENCY RESOLVER =============
# Download the dependencies on container
# ===============================================

FROM maven:3-jdk-11-slim AS dependency&#95;resolver

# Download all library dependencies
COPY ./pom.xml /app/pom.xml

WORKDIR /app

RUN mvn dependency:copy-dependencies $MAVEN&#95;CLI&#95;OPTS

# ============= TESTING =================
# Run tests on container
# =======================================

FROM dependency_resolver AS tester

WORKDIR /app

CMD mvn clean test $MAVEN&#95;CLI&#95;OPTS

# ============= BUILDER =================
# Build the artifact on container
# =======================================

FROM dependency_resolver as builder

# Build application
COPY . /app

RUN mvn package $MAVEN&#95;CLI&#95;OPTS -Dmaven.test.skip=true

# ============= DOCKER IMAGE ================
# Prepare container image with application artifacts
# ===========================================

FROM openjdk:11-jre-slim

COPY --from=builder /app/target/&#42;.jar app.jar

ENTRYPOINT ["java", "-jar", "/app.jar"]</code></pre>
</div>

So, now we have four different steps: `dependency_resolver`, `tester`, `builder`, and the application itself.

If we want either build the application or test it, we need the project dependencies. Thus, there’s a `dependency_resolver` step there. In the second and the third `FROM` statements, you can see that they depend on `dependency_resolver`.

**Important**: *If you try to build the docker image with `docker build -t my-application .`, only the first, the third, and the last step (`dependency_resolver`, `builder`, and the application itself, respectively) would run.* 

**But why?**

When you try to build the image, it will try to see what the end state of the image is, which would be the application itself. As we know and can see, the last step depends on `builder` (`COPY` statement). If we check the `builder` step, we will see that it depends on `dependency_resolver` (`FROM` statement). So, it will run in this order:

`dependency_resolver` -> `builder` -> application

**Then what’s the `tester` step doing there? Is there a way to reach it?**

You can specify a target by using `--target`: `docker build --target tester -t my-application .`.

This is also [compatible with Docker Compose](https://docs.docker.com/compose/compose-file/compose-file-v3/#target).

## Conclusion

We saw how to use only Docker to build and run applications and commands, removing the need for previous knowledge in some tool or programming language. Also, worth saying that even though we used Docker for these examples, this would also work with other container runtimes like Podman. 

I hope you find this post helpful and spread the word about Docker.

{{< signature "yk, il" >}}
