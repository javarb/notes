# SOFTWARE ENGINEERING IN JAVA

## Session 17 (18/12/2018)

- resolving merge conflicts
- reseting commit
- rebase / merge explanation
https://www.atlassian.com/git/tutorials/merging-vs-rebasing
- Project creation
- see the amount of branches and the differences between the master

### Notes


for frontend-API Roger explained to me the use od rebase and the difeference with merge, also why he used an empty branch to put an initial commit in the beggining of the history in order to after merge to compare from master towards this empty branch in order to see all the changes made and can do comments with the caveat that could make reviees because himself create that branch and PR.

At the end that branch wasn't neccesary, because the changes asked in that branch PR, I applied those changes in the frontend-bs4 branch, so after all I merged this last to master (only different to the empty branch for 1 commit the merge commit). And the empty branch can be deleted (I think I did):

[jaar@port-staff calculator-frontend]$ git status
On branch frontend-bs4
Your branch is up to date with 'origin/frontend-bs4'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html
        modified:   public/scripts/calculator.js
        modified:   public/stylesheets/calculator.css

no changes added to commit (use "git add" and/or "git commit -a")
[jaar@port-staff calculator-frontend]$ git branch
* frontend-bs4
  master
[jaar@port-staff calculator-frontend]$ git branch -a
* frontend-bs4
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/delete-me-after-review
  remotes/origin/frontend-bs4
  remotes/origin/master
[jaar@port-staff calculator-frontend]$ git add . ; git commit -m 'Apply sugesstions in PR #2 #3'; git push
[frontend-bs4 182e403] Apply sugesstions in PR #2 #3
 3 files changed, 10 insertions(+), 56 deletions(-)
Enumerating objects: 15, done.
Counting objects: 100% (15/15), done.
Delta compression using up to 4 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (8/8), 650 bytes | 650.00 KiB/s, done.
Total 8 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To github.com:javarb/calculator-frontend.git
   081423d..182e403  frontend-bs4 -> frontend-bs4
[jaar@port-staff calculator-frontend]$




for api


[jaar@port-staff api]$ git log
commit 2ebf8f787a2bae16f20e97ff4c663fbb6eecdc09 (HEAD -> bugsnag-integration, origin/bugsnag-integration)
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Mon Dec 3 16:47:42 2018 -0500

    Removing BugSnag test

commit c00c06b022cff888cd320e19e322597e8bb116bd
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Sun Dec 2 13:59:46 2018 -0500

    Bugsnag integration

commit f00216f2d95cc4c5d5ee40747efa3b724a3e0f2f (origin/api-calculator, api-calculator)
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Nov 27 16:18:33 2018 -0500

    Minor fix

commit 1027d1fdeea545fab2bf9d80ed8bd3505805badd
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Mon Nov 26 09:26:20 2018 -0500

    Add CORS support

commit 3d7577c2074e3b8cab78143c7a4443989fbf8070
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Nov 13 16:19:47 2018 -0500

    Add enum evaluation into switch

commit f2c21a47989ff0ef95d014ce33f7e6992e54d69b
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Nov 13 09:29:11 2018 -0500
[jaar@port-staff api]$ git status
On branch bugsnag-integration
Your branch is up to date with 'origin/bugsnag-integration'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   build.gradle
        modified:   src/main/java/co/org/osso/api/CalculatorController.java
        modified:   src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java

no changes added to commit (use "git add" and/or "git commit -a")
[jaar@port-staff api]$ git diff
diff --git a/build.gradle b/build.gradle
index 87c18ed..9d011ed 100644
--- a/build.gradle
+++ b/build.gradle
@@ -28,9 +28,9 @@ dependencies {
        compile('org.springframework.boot:spring-boot-starter-actuator')
        compile('org.springframework.boot:spring-boot-starter-data-mongodb')
        compile('org.springframework.boot:spring-boot-starter-web')
+       compile 'com.bugsnag:bugsnag-spring:3.+'
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
-       compile 'com.bugsnag:bugsnag-spring:3.+'
-
+       testCompile('org.apache.httpcomponents:httpclient:4.5.5')
 }
diff --git a/src/main/java/co/org/osso/api/CalculatorController.java b/src/main/java/co/org/osso/api/CalculatorController.java
index 6c53162..a2e2218 100644
--- a/src/main/java/co/org/osso/api/CalculatorController.java
+++ b/src/main/java/co/org/osso/api/CalculatorController.java
@@ -28,6 +28,7 @@ public class CalculatorController {
     }

     @GetMapping("/factorial/{number}")
+    // JSON that contains a biginteger
     public BigInteger getFactorial(@PathVariable("number") int number){
         return calculator.getFactorial(number);
     }
+++ b/src/main/java/co/org/osso/api/CalculatorController.java
@@ -28,6 +28,7 @@ public class CalculatorController {
     }

     @GetMapping("/factorial/{number}")
+    // JSON that contains a biginteger
     public BigInteger getFactorial(@PathVariable("number") int number){
         return calculator.getFactorial(number);
     }
diff --git a/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java b/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
index fa172d1..a0fdd36 100644
--- a/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
+++ b/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
@@ -1,16 +1,41 @@
 package co.org.osso.api;

+import com.fasterxml.jackson.core.JsonProcessingException;
+import com.fasterxml.jackson.databind.DeserializationFeature;
+import com.fasterxml.jackson.databind.ObjectMapper;
+import org.apache.http.HttpResponse;
+import org.apache.http.auth.AuthScope;
+import org.apache.http.auth.UsernamePasswordCredentials;
+import org.apache.http.client.CredentialsProvider;
+import org.apache.http.client.methods.HttpPost;
+import org.apache.http.client.methods.HttpUriRequest;
+import org.apache.http.entity.StringEntity;
+import org.apache.http.impl.client.BasicCredentialsProvider;
+import org.apache.http.impl.client.CloseableHttpClient;
+import org.apache.http.impl.client.HttpClientBuilder;
+import org.apache.http.util.EntityUtils;
 import org.junit.Assert;
 import org.junit.Test;
+import org.junit.runner.RunWith;
+import org.springframework.boot.test.context.SpringBootTest;
+import org.springframework.boot.web.server.LocalServerPort;
+import org.springframework.test.context.junit4.SpringRunner;

+import java.io.IOException;
+import java.io.UnsupportedEncodingException;
 import java.math.BigInteger;
 import java.util.Arrays;
 import java.util.List;

+@RunWith(SpringRunner.class)
+@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
 public class ApiApplicationCalculatorTests {

     Calculator target = new Calculator();

+    @LocalServerPort
+    int port;
+
     @Test
     public void checkCalculatorFibonacci(){
         List<Integer> expected = Arrays.asList(1,1,2,3,5);
@@ -59,4 +84,62 @@ public class ApiApplicationCalculatorTests {
             Assert.assertTrue(re.getMessage().contains("Error:"));
         }
     }
+
+    // look at databasic, this is the same mapper
+    private ObjectMapper mapper() {
+        final ObjectMapper mapper = new ObjectMapper();
+        mapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
+        return mapper;
+    }
+
+    private String serialise(final Object object) throws JsonProcessingException {
+        return mapper().writeValueAsString(object);
+    }
+
+    // HttpUriRequest is an interface parent of HttpPost
+    // If I inline http method, what is there, comes to here
+    HttpResponse send(final HttpUriRequest req) throws IOException {
+        return http().execute(req);
+    }
+
+    HttpPost post(final String path, Object payload) throws JsonProcessingException, UnsupportedEncodingException {
+        String uri = uri(path);
+        final HttpPost req = new HttpPost(uri);
+        req.setEntity(new StringEntity(serialise(payload)));
+        req.setHeader("Accept", "application/json");
+        req.setHeader("Content-type", "application/json");
+        return req;
+    }
+
+    private CloseableHttpClient http() {
+        return HttpClientBuilder.create()
+                .build();
+    }
+
+    private String uri(final String path) {
+        return baseUrl() + path;
+    }
+
+    private String baseUrl() {
+        return "http://localhost:" + port + "/";
+    }
+
+    @Test
+    public void testPost() throws Exception{
+        Book book = new Book();
+        book.setTitle("one");
+        book.setYear("2018");
+        HttpPost req = post("/api/book", book);
+        HttpResponse res = send(req);
+        Book bookResponse = deserialise(res, Book.class);
+        Assert.assertEquals("one", bookResponse.getTitle());
+        Assert.assertNotNull(bookResponse.getBookID());
+    }
+
+    // read about generic (try to understand this can be a little advanced)
+    <T> T deserialise(final HttpResponse res, final Class<T> type) throws IOException {
+        return mapper().readValue(EntityUtils.toString(res.getEntity()), type);
+    }
+
+
 }
[jaar@port-staff api]$ git brnach
git: 'brnach' is not a git command. See 'git --help'.

The most similar command is
        branch
[jaar@port-staff api]$ git branch
  api-basics
  api-calculator
  api-calculator-fix-bug
* bugsnag-integration
  master
[jaar@port-staff api]$ git add -p
diff --git a/build.gradle b/build.gradle
index 87c18ed..9d011ed 100644
--- a/build.gradle
+++ b/build.gradle
@@ -28,9 +28,9 @@ dependencies {
        compile('org.springframework.boot:spring-boot-starter-actuator')
        compile('org.springframework.boot:spring-boot-starter-data-mongodb')
        compile('org.springframework.boot:spring-boot-starter-web')
+       compile 'com.bugsnag:bugsnag-spring:3.+'
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
-       compile 'com.bugsnag:bugsnag-spring:3.+'
-
+       testCompile('org.apache.httpcomponents:httpclient:4.5.5')
 }
Stage this hunk [y,n,q,a,d,s,e,?]? y

diff --git a/src/main/java/co/org/osso/api/CalculatorController.java b/src/main/java/co/org/osso/api/CalculatorController.java
index 6c53162..a2e2218 100644
--- a/src/main/java/co/org/osso/api/CalculatorController.java
+++ b/src/main/java/co/org/osso/api/CalculatorController.java
@@ -28,6 +28,7 @@ public class CalculatorController {
     }

     @GetMapping("/factorial/{number}")
+    // JSON that contains a biginteger
     public BigInteger getFactorial(@PathVariable("number") int number){
         return calculator.getFactorial(number);
     }
Stage this hunk [y,n,q,a,d,e,?]? n

diff --git a/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java b/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
index fa172d1..a0fdd36 100644
--- a/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
+++ b/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
@@ -1,16 +1,41 @@
 package co.org.osso.api;

+import com.fasterxml.jackson.core.JsonProcessingException;
+import com.fasterxml.jackson.databind.DeserializationFeature;
+import com.fasterxml.jackson.databind.ObjectMapper;
+import org.apache.http.HttpResponse;
+import org.apache.http.auth.AuthScope;
+import org.apache.http.auth.UsernamePasswordCredentials;
+import org.apache.http.client.CredentialsProvider;
+import org.apache.http.client.methods.HttpPost;
+import org.apache.http.client.methods.HttpUriRequest;
+import org.apache.http.entity.StringEntity;
+import org.apache.http.impl.client.BasicCredentialsProvider;
+import org.apache.http.impl.client.CloseableHttpClient;
+import org.apache.http.impl.client.HttpClientBuilder;
+import org.apache.http.util.EntityUtils;
 import org.junit.Assert;
 import org.junit.Test;
+import org.junit.runner.RunWith;
+import org.springframework.boot.test.context.SpringBootTest;
+import org.springframework.boot.web.server.LocalServerPort;
+import org.springframework.test.context.junit4.SpringRunner;

+import java.io.IOException;
+import java.io.UnsupportedEncodingException;
 import java.math.BigInteger;
 import java.util.Arrays;
 import java.util.List;

+@RunWith(SpringRunner.class)
+@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
 public class ApiApplicationCalculatorTests {

     Calculator target = new Calculator();

+    @LocalServerPort
+    int port;
+
     @Test
     public void checkCalculatorFibonacci(){
         List<Integer> expected = Arrays.asList(1,1,2,3,5);
Stage this hunk [y,n,q,a,d,j,J,g,/,s,e,?]? n
@@ -59,4 +84,62 @@ public class ApiApplicationCalculatorTests {
             Assert.assertTrue(re.getMessage().contains("Error:"));
         }
     }
+
+    // look at databasic, this is the same mapper
+    private ObjectMapper mapper() {
+        final ObjectMapper mapper = new ObjectMapper();
+        mapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
+        return mapper;
+    }
+
+    private String serialise(final Object object) throws JsonProcessingException {
+        return mapper().writeValueAsString(object);
+    }
+
+    // HttpUriRequest is an interface parent of HttpPost
+    // If I inline http method, what is there, comes to here
+    HttpResponse send(final HttpUriRequest req) throws IOException {
+        return http().execute(req);
+    }
+
+    HttpPost post(final String path, Object payload) throws JsonProcessingException, UnsupportedEncodingException {
+        String uri = uri(path);
+        final HttpPost req = new HttpPost(uri);
+        req.setEntity(new StringEntity(serialise(payload)));
+        req.setHeader("Accept", "application/json");
+        req.setHeader("Content-type", "application/json");
+        return req;
+    }
+
+    private CloseableHttpClient http() {
+        return HttpClientBuilder.create()
+                .build();
+    }
+
+    private String uri(final String path) {
+        return baseUrl() + path;
+    }
+
+    private String baseUrl() {
+        return "http://localhost:" + port + "/";
+    }
+
+    @Test
+    public void testPost() throws Exception{
+        Book book = new Book();
+        book.setTitle("one");
+        book.setYear("2018");
+        HttpPost req = post("/api/book", book);
+        HttpResponse res = send(req);
+        Book bookResponse = deserialise(res, Book.class);
+        Assert.assertEquals("one", bookResponse.getTitle());
+        Assert.assertNotNull(bookResponse.getBookID());
+    }
+
+    // read about generic (try to understand this can be a little advanced)
+    <T> T deserialise(final HttpResponse res, final Class<T> type) throws IOException {
+        return mapper().readValue(EntityUtils.toString(res.getEntity()), type);
+    }
+
+
 }
Stage this hunk [y,n,q,a,d,K,g,/,e,?]? n

[jaar@port-staff api]$ git commit -m 'Minor change'; git push
[bugsnag-integration 3e3245d] Minor change
 1 file changed, 2 insertions(+), 2 deletions(-)
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 341 bytes | 341.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:javarb/api.git
   2ebf8f7..3e3245d  bugsnag-integration -> bugsnag-integration
[jaar@port-staff api]$ git branch

  api-basics
  api-calculator
  api-calculator-fix-bug
* bugsnag-integration
  master
[jaar@port-staff api]$
[jaar@port-staff api]$ git show
commit 3e3245de5df8c3bf21805709e5ff80be255e3344 (HEAD -> bugsnag-integration, origin/bugsnag-integration)
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Dec 18 11:54:18 2018 -0500

    Minor change

diff --git a/build.gradle b/build.gradle
index 87c18ed..9d011ed 100644
--- a/build.gradle
+++ b/build.gradle
@@ -28,9 +28,9 @@ dependencies {
        compile('org.springframework.boot:spring-boot-starter-actuator')
        compile('org.springframework.boot:spring-boot-starter-data-mongodb')
        compile('org.springframework.boot:spring-boot-starter-web')
+       compile 'com.bugsnag:bugsnag-spring:3.+'
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
-       compile 'com.bugsnag:bugsnag-spring:3.+'
-
+       testCompile('org.apache.httpcomponents:httpclient:4.5.5')
 }
[jaar@port-staff api]$ git checkout -b http-integration-tests
M       src/main/java/co/org/osso/api/CalculatorController.java
M       src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
Switched to a new branch 'http-integration-tests'
[jaar@port-staff api]$ git push
fatal: The current branch http-integration-tests has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin http-integration-tests

[jaar@port-staff api]$     git push --set-upstream origin http-integration-tests
Total 0 (delta 0), reused 0 (delta 0)
remote:
remote: Create a pull request for 'http-integration-tests' on GitHub by visiting:
remote:      https://github.com/javarb/api/pull/new/http-integration-tests
remote:
To github.com:javarb/api.git
 * [new branch]      http-integration-tests -> http-integration-tests
Branch 'http-integration-tests' set up to track remote branch 'http-integration-tests' from 'origin'.
[jaar@port-staff api]$ git checkout -
M       src/main/java/co/org/osso/api/CalculatorController.java
M       src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
Switched to branch 'bugsnag-integration'
Your branch is up to date with 'origin/bugsnag-integration'.
[jaar@port-staff api]$ git show
commit 3e3245de5df8c3bf21805709e5ff80be255e3344 (HEAD -> bugsnag-integration, origin/http-integration-tests, origin/bugsnag-integration, http-integration-tests)
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Dec 18 11:54:18 2018 -0500

    Minor change

diff --git a/build.gradle b/build.gradle
index 87c18ed..9d011ed 100644
--- a/build.gradle
+++ b/build.gradle
@@ -28,9 +28,9 @@ dependencies {
        compile('org.springframework.boot:spring-boot-starter-actuator')
        compile('org.springframework.boot:spring-boot-starter-data-mongodb')
        compile('org.springframework.boot:spring-boot-starter-web')
+       compile 'com.bugsnag:bugsnag-spring:3.+'
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
-       compile 'com.bugsnag:bugsnag-spring:3.+'
-
+       testCompile('org.apache.httpcomponents:httpclient:4.5.5')
 }
[jaar@port-staff api]$ git status
On branch bugsnag-integration
Your branch is up to date with 'origin/bugsnag-integration'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   src/main/java/co/org/osso/api/CalculatorController.java
        modified:   src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java

no changes added to commit (use "git add" and/or "git commit -a")
[jaar@port-staff api]$ git stash
Saved working directory and index state WIP on bugsnag-integration: 3e3245d Minor change
[jaar@port-staff api]$ git status
On branch bugsnag-integration
Your branch is up to date with 'origin/bugsnag-integration'.

nothing to commit, working tree clean
[jaar@port-staff api]$ git reset HEAD~
Unstaged changes after reset:
M       build.gradle
[jaar@port-staff api]$ git status
On branch bugsnag-integration
Your branch is behind 'origin/bugsnag-integration' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   build.gradle

no changes added to commit (use "git add" and/or "git commit -a")
[jaar@port-staff api]$ git log
commit 2ebf8f787a2bae16f20e97ff4c663fbb6eecdc09 (HEAD -> bugsnag-integration)
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Mon Dec 3 16:47:42 2018 -0500

    Removing BugSnag test

commit c00c06b022cff888cd320e19e322597e8bb116bd
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Sun Dec 2 13:59:46 2018 -0500

    Bugsnag integration

commit f00216f2d95cc4c5d5ee40747efa3b724a3e0f2f (origin/api-calculator, api-calculator)
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Nov 27 16:18:33 2018 -0500

    Minor fix

commit 1027d1fdeea545fab2bf9d80ed8bd3505805badd
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Mon Nov 26 09:26:20 2018 -0500

    Add CORS support

commit 3d7577c2074e3b8cab78143c7a4443989fbf8070
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Nov 13 16:19:47 2018 -0500

    Add enum evaluation into switch

commit f2c21a47989ff0ef95d014ce33f7e6992e54d69b
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Nov 13 09:29:11 2018 -0500
[jaar@port-staff api]$ git diff
diff --git a/build.gradle b/build.gradle
index 87c18ed..9d011ed 100644
--- a/build.gradle
+++ b/build.gradle
@@ -28,9 +28,9 @@ dependencies {
        compile('org.springframework.boot:spring-boot-starter-actuator')
        compile('org.springframework.boot:spring-boot-starter-data-mongodb')
        compile('org.springframework.boot:spring-boot-starter-web')
+       compile 'com.bugsnag:bugsnag-spring:3.+'
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
-       compile 'com.bugsnag:bugsnag-spring:3.+'
-
+       testCompile('org.apache.httpcomponents:httpclient:4.5.5')
 }
[jaar@port-staff api]$ git add -p
diff --git a/build.gradle b/build.gradle
index 87c18ed..9d011ed 100644
--- a/build.gradle
+++ b/build.gradle
@@ -28,9 +28,9 @@ dependencies {
        compile('org.springframework.boot:spring-boot-starter-actuator')
        compile('org.springframework.boot:spring-boot-starter-data-mongodb')
        compile('org.springframework.boot:spring-boot-starter-web')
+       compile 'com.bugsnag:bugsnag-spring:3.+'
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
-       compile 'com.bugsnag:bugsnag-spring:3.+'
-
+       testCompile('org.apache.httpcomponents:httpclient:4.5.5')
 }
Stage this hunk [y,n,q,a,d,s,e,?]? s
Split into 2 hunks.
@@ -28,6 +28,7 @@
        compile('org.springframework.boot:spring-boot-starter-actuator')
        compile('org.springframework.boot:spring-boot-starter-data-mongodb')
        compile('org.springframework.boot:spring-boot-starter-web')
+       compile 'com.bugsnag:bugsnag-spring:3.+'
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]? y
@@ -31,6 +32,5 @@
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
-       compile 'com.bugsnag:bugsnag-spring:3.+'
-
+       testCompile('org.apache.httpcomponents:httpclient:4.5.5')
 }
Stage this hunk [y,n,q,a,d,K,g,/,e,?]? s^C
[jaar@port-staff api]$ git diff
diff --git a/build.gradle b/build.gradle
index 87c18ed..59083be 100644
--- a/build.gradle
+++ b/build.gradle
@@ -28,9 +28,8 @@ dependencies {
        compile('org.springframework.boot:spring-boot-starter-actuator')
        compile('org.springframework.boot:spring-boot-starter-data-mongodb')
        compile('org.springframework.boot:spring-boot-starter-web')
+       compile 'com.bugsnag:bugsnag-spring:3.+'
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
-       compile 'com.bugsnag:bugsnag-spring:3.+'
-
 }
[jaar@port-staff api]$ git add . ; git commit -m 'minor change'; git push
[bugsnag-integration 9c04af9] minor change
 1 file changed, 1 insertion(+), 2 deletions(-)
To github.com:javarb/api.git
 ! [rejected]        bugsnag-integration -> bugsnag-integration (non-fast-forward)
error: failed to push some refs to 'git@github.com:javarb/api.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
[jaar@port-staff api]$ git add . ; git commit -m 'minor change'; git push --force
On branch bugsnag-integration
Your branch and 'origin/bugsnag-integration' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

nothing to commit, working tree clean
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 298 bytes | 298.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:javarb/api.git
 + 3e3245d...9c04af9 bugsnag-integration -> bugsnag-integration (forced update)
[jaar@port-staff api]$ git diff
diff --git a/build.gradle b/build.gradle
index 59083be..9d011ed 100644
--- a/build.gradle
+++ b/build.gradle
@@ -32,4 +32,5 @@ dependencies {
        runtime('org.springframework.boot:spring-boot-devtools')
        testCompile('org.springframework.boot:spring-boot-starter-test')
        testCompile('de.flapdoodle.embed:de.flapdoodle.embed.mongo')
+       testCompile('org.apache.httpcomponents:httpclient:4.5.5')
 }
[jaar@port-staff api]$ git checkout -
error: Your local changes to the following files would be overwritten by checkout:
        build.gradle
Please commit your changes or stash them before you switch branches.
Aborting
[jaar@port-staff api]$ git reset --hard
HEAD is now at 9c04af9 minor change
[jaar@port-staff api]$ git log
commit 9c04af9ed94577a563ab314b8fd26063f74b46a9 (HEAD -> bugsnag-integration, origin/bugsnag-integration)
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Dec 18 15:00:55 2018 -0500

    minor change

commit 2ebf8f787a2bae16f20e97ff4c663fbb6eecdc09
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Mon Dec 3 16:47:42 2018 -0500

    Removing BugSnag test

commit c00c06b022cff888cd320e19e322597e8bb116bd
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Sun Dec 2 13:59:46 2018 -0500

    Bugsnag integration

commit f00216f2d95cc4c5d5ee40747efa3b724a3e0f2f (origin/api-calculator, api-calculator)
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Nov 27 16:18:33 2018 -0500

    Minor fix

commit 1027d1fdeea545fab2bf9d80ed8bd3505805badd
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Mon Nov 26 09:26:20 2018 -0500

    Add CORS support

commit 3d7577c2074e3b8cab78143c7a4443989fbf8070
Author: Javier Arboleda <reivaj49@gmail.com>
Date:   Tue Nov 13 16:19:47 2018 -0500
[jaar@port-staff api]$ git status
On branch bugsnag-integration
Your branch is up to date with 'origin/bugsnag-integration'.

nothing to commit, working tree clean
[jaar@port-staff api]$ git checkout -
Switched to branch 'http-integration-tests'
Your branch is up to date with 'origin/http-integration-tests'.
[jaar@port-staff api]$ git status
On branch http-integration-tests
Your branch is up to date with 'origin/http-integration-tests'.

nothing to commit, working tree clean
[jaar@port-staff api]$ git stash pop
On branch http-integration-tests
Your branch is up to date with 'origin/http-integration-tests'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   src/main/java/co/org/osso/api/CalculatorController.java
        modified:   src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (599d46570d4af1869dc965e21c00c08d06670899)
[jaar@port-staff api]$ git diff
diff --git a/src/main/java/co/org/osso/api/CalculatorController.java b/src/main/java/co/org/osso/api/CalculatorController.java
index 6c53162..a2e2218 100644
--- a/src/main/java/co/org/osso/api/CalculatorController.java
+++ b/src/main/java/co/org/osso/api/CalculatorController.java
@@ -28,6 +28,7 @@ public class CalculatorController {
diff --git a/src/main/java/co/org/osso/api/CalculatorController.java b/src/main/java/co/org/osso/api/CalculatorController.java
index 6c53162..a2e2218 100644
--- a/src/main/java/co/org/osso/api/CalculatorController.java
+++ b/src/main/java/co/org/osso/api/CalculatorController.java
@@ -28,6 +28,7 @@ public class CalculatorController {
     }

     @GetMapping("/factorial/{number}")
+    // JSON that contains a biginteger
     public BigInteger getFactorial(@PathVariable("number") int number){
         return calculator.getFactorial(number);
     }
diff --git a/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java b/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
index fa172d1..a0fdd36 100644
--- a/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
+++ b/src/test/java/co/org/osso/api/ApiApplicationCalculatorTests.java
@@ -1,16 +1,41 @@
 package co.org.osso.api;

+import com.fasterxml.jackson.core.JsonProcessingException;
+import com.fasterxml.jackson.databind.DeserializationFeature;
+import com.fasterxml.jackson.databind.ObjectMapper;
+import org.apache.http.HttpResponse;
+import org.apache.http.auth.AuthScope;
+import org.apache.http.auth.UsernamePasswordCredentials;
+import org.apache.http.client.CredentialsProvider;
+import org.apache.http.client.methods.HttpPost;
+import org.apache.http.client.methods.HttpUriRequest;
+import org.apache.http.entity.StringEntity;
+import org.apache.http.impl.client.BasicCredentialsProvider;
+import org.apache.http.impl.client.CloseableHttpClient;
+import org.apache.http.impl.client.HttpClientBuilder;
+import org.apache.http.util.EntityUtils;
[jaar@port-staff api]$ git add . ; git commit -m "Add HTTP verbs Integration test"; git push
[http-integration-tests c6fe812] Add HTTP verbs Integration test
 2 files changed, 84 insertions(+)
Enumerating objects: 31, done.
Counting objects: 100% (31/31), done.
Delta compression using up to 4 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (17/17), 2.53 KiB | 863.00 KiB/s, done.
Total 17 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To github.com:javarb/api.git
   3e3245d..c6fe812  http-integration-tests -> http-integration-tests
[jaar@port-staff api]$ git fetch
remote: Enumerating objects: 2, done.
remote: Counting objects: 100% (2/2), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (2/2), done.
From github.com:javarb/api
   f77c479..37c4a2d  master     -> origin/master
[jaar@port-staff api]$ git branch -a
  api-basics
  api-calculator
  api-calculator-fix-bug
  bugsnag-integration
* http-integration-tests
  master
  remotes/origin/api-basics
  remotes/origin/api-calculator
  remotes/origin/api-calculator-fix-bug
  remotes/origin/bugsnag-integration
  remotes/origin/http-integration-tests
  remotes/origin/master
[jaar@port-staff api]$ git fetch -p
From github.com:javarb/api
 - [deleted]         (none)     -> origin/api-basics
[jaar@port-staff api]$ git branch -a
  api-basics
  api-calculator
  api-calculator-fix-bug
  bugsnag-integration
* http-integration-tests
  master
  remotes/origin/api-calculator
  remotes/origin/api-calculator-fix-bug
  remotes/origin/bugsnag-integration
  remotes/origin/http-integration-tests
  remotes/origin/master
[jaar@port-staff api]$ git checkout api-calculator-fix-bug
Switched to branch 'api-calculator-fix-bug'
Your branch is up to date with 'origin/api-calculator-fix-bug'.
[jaar@port-staff api]$ git merge origin/master
Auto-merging src/main/java/co/org/osso/api/Calculator.java
CONFLICT (content): Merge conflict in src/main/java/co/org/osso/api/Calculator.java
Automatic merge failed; fix conflicts and then commit the result.
[jaar@port-staff api]$ git status
On branch api-calculator-fix-bug
Your branch is up to date with 'origin/api-calculator-fix-bug'.

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:

        modified:   build.gradle
        new file:   src/main/java/co/org/osso/api/BugsnagConfig.java
        modified:   src/main/java/co/org/osso/api/CalculatorController.java

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   src/main/java/co/org/osso/api/Calculator.java

[jaar@port-staff api]$ git add . ; git commit;
[api-calculator-fix-bug 9607af3] Merge remote-tracking branch 'origin/master' into api-calculator-fix-bug
[jaar@port-staff api]$ git push
Enumerating objects: 28, done.
Counting objects: 100% (28/28), done.
Delta compression using up to 4 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (10/10), 776 bytes | 388.00 KiB/s, done.
Total 10 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To github.com:javarb/api.git
   ed9586c..9607af3  api-calculator-fix-bug -> api-calculator-fix-bug
[jaar@port-staff api]$




### Resources

- [Apache Groovy Language][11]

[1]: https://martinfowler.com/books/dsl.html
