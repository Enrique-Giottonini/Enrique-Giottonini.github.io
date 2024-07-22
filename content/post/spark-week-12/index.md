---
title: Encora Spark Week 12. A first contribution
date: 2024-07-22
math: true
diagram: true
---

<!-- APPRENTICE TECHNICAL LOG DOC

Eclipse Collections 1st Pull Request: Fix bold markup typos in reference guide #1652



Enrique Giottonini





OVERVIEW

As part of the Spark program's week 11 module, "Testing the open-source waters & fundamentals," I made a Pull Request (PR) to fix a simple typo issue in the Eclipse Collections project. My goal was to practice contributing to an open-source project for the first time.



Eclipse Collections is an alternative collections library for Java, hosted by the Eclipse Foundation, which oversees multiple open-source projects. I discovered this project through the https://goodfirstissue.dev repository, which curates "good first issue" labels from various GitHub projects, inviting newcomers to contribute.



The reason I chose to work in such a simple contribution is that my intention was solely to understand the process of pushing a pull request, getting it reviewed, and then merged.



The PR has been approved and can be found here, and it’s already merged into the main repository.





CONTEXT

I was reading the reference guide in ` eclipse-collections/docs/2-Collection_Containers.adoc` to get an understanding of the API and work on an issue. I found a low-hanging fruit, someone left a bold symbol markup typo:





I then ‘CTRL + F <<*>>’ in hopes of finding more typos of the same class, and I did find another one!



SOLUTION



I followed the Contributing Guide:



I signed an agreement

I forked the repository into my account.

I created a local clone of the repo from the command line

```

git clone https://github.com/Enrique-Giottonini/eclipse-collections.git`
	cd eclipse-collections

```

I configured the upstream remote (for pulling updates):

```

git remote add upstream https://github.com/eclipse/eclipse-collections.git

```

Sync my fork

```

git fetch –all

git pull upstream master –rebase

```

I removed the unnecessary ‘*’ in the table and added a ‘*’ to the word ‘groupBy’ using vim.

I committed the changes to fork; the signoff is the same account (using gh auth login) in which I signed the step one agreement.

```

git add .

git commit --message "My commit message as per guidelines" --signoff

```

Repeated step five, with no merging conflicts

``` git push``` to my fork.

Used the GitHub GUI for making a PR from my fork.

Wait for review

I received an email when my contribution got accepted and then merged.

  -->

<!--
  Spark Music Advisor
A Java command line application to discover artists, albums, and categories; from Spotify trends.
Functional Requirements
Read two optional server points from command line arguments:
`-access`: provide an authorization server path, with a default value of https://accounts.spotify.com
`-resource`: should provide API server path, with a default value of https://api.spotify.com
Read an optional configuration from command line arguments:
`-page`: to paginate results with a default value of five
an `auth` command that will print the auth link and allow us to use other commands. Commands are unavailable if user access for the program is not successful.
a `featured` command that displays a list of Spotify-featured playlists with their links fetched from API, and paginated
a `new` command that displays a list of new albums with artists and links on Spotify; same reqs
a `categories` command that displays a list of all available categories on Spotify; same reqs
a `playlists C_NAME`, where C_NAME is the name of a category. The list contains playlists of this category and their links on Spotify; same reqs
an `exit` command that shuts down the application; same reqs
the auth session should be kept alive as long as the application is running
Engineering Requirements
Using Spotify API
Use http protocol
In the `auth` command before printing the auth link (from the previous stage), you should start an HTTP server that will listen for the incoming requests. When the user confirms or rejects the authorization, the server should return the following text to the browser:
"Got the code. Return back to your program." if the query contains the authorization code.
"Authorization code not found. Try again." otherwise.
After the code is received, the server must shut down and you should get `access_token` by making a POST request on ${authorization-server-path}/api/token
and then print the result body
Full documentation on how to work with api can be found at https://developer.spotify.com/documentation/web-api/reference/.
Object model: https://developer.spotify.com/documentation/web-api/reference/object-model/
To fetch resources use ${api-server-path}/v1/browse/{resource}
To get all categories, use https://api.spotify.com/v1/browse/categories
To get a playlist, use https://api.spotify.com/v1/browse/categories/{category_id}/playlists
To get new releases, use https://api.spotify.com/v1/browse/new-releases
To get featured playlists, use https://api.spotify.com/v1/browse/featured-playlists
Pay attention to playlists. Make sure that inside the request you send category id, not category name! Category names can contain spaces or other invalid URL symbols. So you should request category ids and names before the playlists request and find the id by category name. If the id format is correct but you cannot find it in the list of ids, print "Unknown category name.".
In case of invalid category id (contains invalid URL symbols) in playlist request or other API error, the program should output the error message from the Spotify response. For example, if you get the response {"error":{"status":404,"message":"Specified id doesn't exist"}}, you should print the following line: "Specified id doesn't exist"
Use MVC architectural pattern
(view) A CommandLineMusicAdvisor that implements a MusicAdvisorView interface
(controller) A SpotifyAPIController that implements a MusicAdvisorController interface
(model) beans
Use design patterns:
A Singleton for MusicAdvisorView implementation
A Singleton for MusicAPIController implementation
Possible decorator for MusicAdvisorView implementation? -->

tl;dr: I got my first pull request accepted into an open-source project, Eclipse Collections, by fixing a simple typo in the reference guide. I also finished a first implementation of the Music Advisor project, a Java CLI application that uses the Spotify API to recommend music to the user.

# **Index**

1. [**Anatomy of a first Pull Request**](#anatomy-of-a-first-pull-request)
2. [**Authorization Code Flow**](#authorization-code-flow)
3. [**Music Advisor Project**](#music-advisor-project)

# **1. Anatomy of a first Pull Request**

I was reading the reference guide in `eclipse-collections/docs/2-Collection_Containers.adoc` to get an understanding of the API and work on an issue. I found a low-hanging fruit, someone left a bold symbol markup typo:

![alt text](image.png)

I then ‘CTRL + F <<\*>>’ in hopes of finding more typos of the same class, and I did find another one!

![alt text](image-1.png)

To fix the issue, I followed the Contributing Guide:

1. I signed an agreement on the Eclipse Foundation website, they have an automated test to check if you have signed the agreement.
2. I forked the repository into my account.
3. I created a local clone of the fork repo from the command line:

```bash
git clone
cd eclipse-collections
```

4. I configured the upstream remote of the OG repo (for pulling updates):

```bash
git remote add upstream
```

5. I removed the unnecessary ‘_’ in the table and added a ‘_’ to the word ‘groupBy’ using vim.

```diff
- *peek(*int count*)*
+ *peek(int count)*
```

```diff
- *groupBy
+ *groupBy*
```

6. I committed the changes to fork; the signoff is the same account (using `gh auth login`) in which I signed the step one agreement.

```bash
git add .
git commit --message "Fix bold markup typos in reference guide" --signoff
```

7. Repeated step five, with no merging conflicts (obviously and thankfully).

```bash
git push
```

8. Used the GitHub GUI for making a PR from my fork.

9. Waited for review.

I received an email when my contribution got accepted and then merged which was a great feeling! Now the process is more clear to me, and I can start working on more complex issues.

# **2. Authorization Code Flow**

This week I got to learn about the Authorization Code Flow, which is a way to authorize a user to access a resource. The idea is that an user needed to authenticate with an spotify account, so I won't have to store the user's credentials in my application. The flow goes like this:

1. I created my credentials on the Spotify Developer Dashboard, which gave me a `client_id` and a `client_secret` that the client application uses to identify itself to the **authorization server** (Spotify Accounts Service).
2. The client application redirects the user to the **authorization server** with the `client_id`, `redirect_uri`, and `scope` (permissions) as query parameters. In my case, I just printed the auth link to the console.
3. The user logs in to Spotify and grants the client application permission to access the requested data.
4. The **authorization server** redirects the user back to the client application with an authorization code.
5. The client application sends a POST request to the **authorization server** with the `client_id`, `client_secret`, `grant_type`, `code`, and `redirect_uri` as form parameters.
6. The **authorization server** responds with an access token and a refresh token.
7. The client application can now use the access token to make requests to the Spotify API.

The flow can be represented as a sequence diagram:

```mermaid
sequenceDiagram
    participant Application
    participant SpotifyAccountsService
    participant User
    participant SpotifyAPI
    Application->>SpotifyAccountsService: GET /authorize?client_id=CLIENT_ID&redirect_uri=REDIRECT_URI&scope=SCOPE
    SpotifyAccountsService->>User: Redirect to login
    User->>SpotifyAccountsService: Logs in and authorizes access
    SpotifyAccountsService->>Application: Redirect to REDIRECT_URI with code=AUTHORIZATION_CODE&status=SUCCESS
    Application->>SpotifyAccountsService: POST /api/token with client_id, client_secret, grant_type, code, redirect_uri
    SpotifyAccountsService->>Application: Responds with access_token and refresh_token
    Application->>SpotifyAPI: GET /resource with access_token
    SpotifyAPI->>Application: Responds with data
```

I implemented the `auth` command in the Music Advisor project, which starts an HTTP server that listens for incoming requests. When the user confirms or rejects the authorization, the server returns the following text to the browser:

- "Got the code. Return back to your program." if the query contains the authorization
- "Authorization code not found. Try again." otherwise.

After the code is received, the server shuts down and I get the `access_token` by making a POST request on `${authorization-server-path}/api/token`, with the `access_token` the program can now make requests to the Spotify API for getting for example "featured playlists", or "new releases".

This is not the first time I've worked with OAuth2, but it's the first time I've implemented the Authorization Code Flow, and it was a great learning experience to know how it works behind the scenes.

# **3. Music Advisor Project**

I've been working on the Music Advisor project, a Java CLI application that uses the Spotify API to recommend music to the user. The project has the following functional requirements:

- Read two optional server points from command line arguments:
  - `-access`: provide an authorization server path, with a default value of https://accounts.spotify.com
  - `-resource`: should provide API server path, with a default value of https://api.spotify.com
- Read an optional configuration from command line arguments:
  - `-page`: to paginate results with a default value of five
- An `auth` command that will print the auth link and allow us to use other commands. Commands are unavailable if user access for the program is not successful.
- A `featured` command that displays a list of Spotify-featured playlists with their links fetched from API, and paginated
- A `new` command that displays a list of new albums with artists and links on Spotify; same reqs
- A `categories` command that displays a list of all available categories on Spotify; same reqs
- A `playlists C_NAME`, where C_NAME is the name of a category. The list contains playlists of this category and their links on Spotify; same reqs
- An `exit` command that shuts down the application; same reqs

For this project I learned and used the MVC architectural pattern. It was hard at first, but it made click when I started seeing the model as the "state" of my application. The bedrock of my implementation is the `/model/Session.java` class, which holds the state of the application as follows:

```java
package advisor.model;

import lombok.Getter;
import lombok.Setter;

@Getter
public class Session {
    private boolean isActive = true;
    private boolean isAuthenticated = false;
    @Setter private String authorizationCode;
    @Setter private String accessToken;
    @Setter private Pageable<Playlist> playlistCache;
    @Setter private Pageable<Album> albumCache;
    @Setter private Pageable<Category> categoriesCache;
    @Setter private String lastCommand;
    public void setValidAuthentication() {
        isAuthenticated = true;
    }
    public void endSession() {
        isActive = false;
    }
}
```

And the `/controller/SessionController.java` class, especially the `run` method, which is the entry point of the application:

```java
    public void run() {
        while (session.isActive() && inputScanner.hasNextLine()) {
            String commandQuery = inputScanner.nextLine();
            List<String> tokens = new ArrayList<>(List.of(commandQuery.split(" ")));
            if (tokens.isEmpty() || !VALID_COMMANDS.contains(tokens.get(0))) {
                view.displayUsage();
                continue;
            }

            String command = tokens.remove(0);
            if (command.equals("exit")) {
                view.exit();
                session.endSession();
            }

            if (!session.isAuthenticated() && !command.equals("auth")) {
                view.requestUserAuthorization();
                continue;
            }

            if (command.equals("auth") && !session.isAuthenticated())  {
                auth();
                continue;
            }

            if (command.equals("prev") || command.equals("next")) {
                changePage(command);
                continue;
            }
            fetchResults(command, tokens);
        }
    }
```

I liked how the MVC ended up, I can see how I could add a GUI to the application and the model would remain the same. I also liked how the `Session` class ended up, it's like a "state" of the application, and I can see how I could add more features to the application and the `Session` class would remain the same.

The most challenging part of the project was to implement pagination, because I didn't where to keep the flow state of the application. I ended up creating a `Pageable` class that holds the current page, the total pages, and the items of the page. I also had to implement a `prev` and `next` command to navigate through the pages, and a cache for each type of resource (playlists, albums, and categories).

I'm looking forward to refactoring the project using a command line framework like "picocli" or "Spring Shell/CLI", because I think it would make the code more readable and maintainable. Also I had troubles with implementing the my own server and client for the Authorization Code Flow, especially with managing Threads and waiting for the authorization code, I would like to explore something like "Spring Web" for that or "Micronaut" to follow best practices and avoid reinventing the wheel.

My main takeaways from this project is that "over abstraction" is something that Java lures you into, and is something to keep an eye on. I also learned that it turns out that the business logic code is significantly smaller that the "plumbing" code (like the HTTP server, the HTTP client, the pagination, the cache, etc), and that's why I think a framework would help me to focus on the business logic and not on the plumbing.
