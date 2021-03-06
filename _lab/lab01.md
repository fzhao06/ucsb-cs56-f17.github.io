---
layout: lab
num: lab01
ready: true
desc: "Tools for java development"
assigned: 2017-10-03 14:00:00.00-7
due: 2017-10-10 23:59:00.00-7
submit_cs: https://submit.cs.ucsb.edu/form/project/834/submission
org: ucsb-cs56-f17
herokuapp: https://ucsb-cs56-f17-signup.herokuapp.com
gauchospace_link: https://gauchospace.ucsb.edu/courses/mod/assign/view.php?id=928343
---

If you find typos or problems with the lab instructions, please report them on Piazza

Overview of this lab
====================

0. Login at github.com.  Click on the drop down menu at left where your username appears, and ensure that <tt>{{page.org}}</tt> appears    among your organizations in the drop down menu.  If not:
   - Be sure that you've registered for the course at <{{page.herokuapp}}>
   - Be sure that you've accepted the invitation to the organization <tt>{{page.org}}</tt> by visiting <https://github.com/{{page.org}}>


1. Now, create a *private* repo for {{page.num}} under the UCSB-CS56-F17 organization on <github.com>
    - It should be called <b>{{page.num}}-yourgithubid</b>
    - It should be <b>private</b>, not public.
    - The owner should be the <b>UCSB-CS56-F17</b> organization as the owner, not your own github id.
    - Add a .gitignore for Java and a README.md file
    - detailed instructions [here](https://ucsb-cs56-pconrad.github.io/topics/github_com_create_private_repo_under_org/)

2.  Configure your CSIL account for git
    - detailed instructions [here](https://ucsb-cs56-pconrad.github.io/topics/csil_git_configuration/)
    - <span style="color:red; font-weight:bold">and here!!!</span> [Configuring your ssh key for Github.com](https://ucsb-cs56-pconrad.github.io/topics/github_ssh_keys/)
    
3.  At the shell prompt on any of the csil machines, type the following command:
    ```
    ssh-keygen -f ~/.ssh/known_hosts -R csil.cs.ucsb.edu
    ```
    
    - You need to do this because CSIL had new hardware installed over the summer, which caused the host key to change. 
    - If you get a "no such file or directory" error, then you can skip this step
4.  Review a few basic facts about git, github.com and github.ucsb.edu
    - detailed information [here](https://ucsb-cs56-pconrad.github.io/topics/git_overview/)

5.  Clone your `{{page.num}}-yourgithubid` repo into your CSIL account.
    - If you know how to do that, great.
    - If not, there are detailed instructions [here](https://ucsb-cs56-pconrad.github.io/topics/git_cloning_your_first_repo/)
    
6.  Read through the [Rational Tutorial](https://ucsb-cs56-pconrad.github.io/tutorials/rational/).
    - For any of the repos, you can fork the repo into your own github.com account.  Here's how:
    - Go to the repo page, e.g.  <https://github.com/UCSB-CS56-pconrad/cs56-rational-ex01>
    - Click the "fork" button at the top right of the page
    - If asked where to fork it, choose your own github.com account
    - Congratulations: you now have a forked copy of the cs56-rational-ex01
    - What do you do with it? Read on...
    
7.  Clone the `cs56-rational-ex01` repo that you forked to your cs56 account (or your
    personal computer).
    - You can review the [cloning your first repo](https://ucsb-cs56-pconrad.github.io/topics/git_cloning_your_first_repo/) tutorial if you need a reminder as to how to do this.
    
8.  Work through the [the first eight parts (ex01-ex08) of the Rational Tutorial](https://ucsb-cs56-pconrad.github.io/tutorials/rational/) so that you learn some of the basic material about how to work with Java:
    - `java`, `javac`, `ant`
    - `build.xml` files
    - JUnit testing
    
    You do not need to continue on to parts 09 and further at this time.  Those parts pertain to labs that
    will come later in the quarter.
    
9.  You are now ready to work on your own lab.
    - Copy the files from the <https://github.com/UCSB-CS56-pconrad/cs56-rational-ex08> repo into the top level directory of
      your own {{page.num}} repo.
    - This means all of the files, including the directories.  You may need `cp -r` for the directories.  If you need a refresher on unix commands, ask a mentor, TA, or instructor for help.
    - Commit an initial version of those files.
    - For that, you'll need the basic git workflow, explained [here](https://ucsb-cs56-pconrad.github.io/topics/git_basic_workflow/)
    - Once you have an initial version of the files, you are ready to start work.
    - Note that to commit the `lib` subdirectory, you may need the `-f` flag, as in `git add -f lib/*.jar`
    - The full set of commands will look something like this:
```
[17:05:12 holt@Metis cs56]$ ls
cs56-rational-ex01 lab01-kevinburk
[17:05:14 holt@Metis cs56]$ git clone https://github.com/UCSB-CS56-pconrad/cs56-rational-ex08
Cloning into 'cs56-rational-ex08'...
remote: Counting objects: 343, done.
remote: Total 343 (delta 0), reused 0 (delta 0), pack-reused 343
Receiving objects: 100% (343/343), 280.52 KiB | 2.30 MiB/s, done.
Resolving deltas: 100% (229/229), done.
[17:05:29 holt@Metis cs56]$ cp -r cs56-rational-ex08/* lab01-kevinburk/
[17:05:42 holt@Metis cs56]$ cd lab01-kevinburk/
[17:06:14 holt@Metis lab01-kevinburk]$ ll
total 32
-rw-r--r--   1 holt  staff  1067 Oct  4 17:05 LICENSE
-rw-r--r--   1 holt  staff    98 Oct  4 17:05 README.md
-rw-r--r--   1 holt  staff  1881 Oct  4 17:05 build.xml
-rw-r--r--   1 holt  staff   598 Oct  4 17:05 index.html
drwxr-xr-x  19 holt  staff   646 Oct  4 17:05 javadoc
drwxr-xr-x   3 holt  staff   102 Oct  4 17:05 lib
drwxr-xr-x   5 holt  staff   170 Oct  4 17:05 src
[17:06:15 holt@Metis lab01-kevinburk]$ git add .
[17:06:21 holt@Metis lab01-kevinburk]$ git add -f lib
```
    
10. Follow the detailed instructions below to complete the assignment.

11. When you are finished, be sure you have done a "git push origin master" to push your changes to github.
    Then, you can download a .zip version of your assignment from github, rename it to `lab01.zip`, and 
    submit via submit.cs at this link: <{{page.submit_cs}}> 

12. Then, follow the additional instructions below to create javadoc for your project, publish it to a public 
    repo (per the instructions) and post the URLs of your solutions to Gauchospace.


Detailed Instructions 
=====================


* Start with the code in the <https://github.com/UCSB-CS56-pconrad/cs56-rational-ex08> repo. 
* Add both tests and correct implementations of these methods to the class.
* Note that for each method, you should add a reasonable number of tests.  The exact number is left to you to determine, but it should be no less than three for each method.


| method                                    | explanation                     |
|-------------------------------------------|---------------------------------|
| `public static int lcm(int a, int b)` | returns least common multiple of a and b. See [wikipedia discussion](https://en.wikipedia.org/wiki/Least_common_multiple#Computing_the_least_common_multiple) |
| `public Rational plus(Rational r)` | returns sum of this number plus r |
| `public static Rational sum(Rational a, Rational b)` | returns a+b |
| `public Rational minus(Rational r)` | returns this number minus r |
| `public static Rational difference(Rational a, Rational b)` | returns a-b |
| `public Rational reciprocalOf()`   | returns reciprocal (swap numerator and denominator).  If numerator if zero, throws an instance of [`java.lang.ArithmeticException`](https://docs.oracle.com/javase/8/docs/api/java/lang/ArithmeticException.html). To review exceptions, see [cs56-rational-ex07](https://github.com/UCSB-CS56-pconrad/cs56-rational-ex07) |
| `public Rational dividedBy(Rational r)` | returns this number divided by r |
| `public static Rational quotient(Rational a, Rational b`) | returns a divided by b |

Some hints to make things easier:

* (a - b) is equivalent to (a + (-1 * b))
* (a / b) is equivalent to (a * reciprocal(b))

Suggested test cases:
* What happens when you create the rational with `Rational(6,-3)` or `Rational(-6,3)`?
* What about the rational `Rational(3,-7)`, `Rational(-3, 7)`, or `Rational(-3,-7)`?

So, don't repeat yourself:
* Multiplication and gcd are already defined for you in the example code.
* You need lcm to find a common denominator to add two rationals, so define lcm before addition.
* The lcm can be defined in terms of gcd and absolute value&mdash;see [wikipedia discussion](https://en.wikipedia.org/wiki/Least_common_multiple#Computing_the_least_common_multiple). Absolute value is predefined `public int Math.abs(int a)`
* Define addition before subtraction, and then define subtraction in terms of addition and multiplication.
* Define reciprocal before division, then define division as multiplication by the reciprocal.

Signify that you are finished by committing code to a github repo that contains a modified version of ex08, with all of the
following:

* a `build.xml` file. You'll be making a few modifications to the `build.xml` to update the javadoc.
* a `src` subdirectory containing `Main.java`, `Rational.java`, and `RationalTest.java`
* a `lib` subdirectory contining the jar file for JUnit
* a `javadoc` subdirectory in which you have produced the javadoc by running `ant javadoc`

Note that you will not be able to publish your javadoc online with the github pages technique (i.e. pushing to a gh-pages branch), because this only works with public repos, not with private ones.   So, we've added some instructions below for publishing the javadoc to a separate public repo with the name `{{page.num}}-javadoc-yourgithubid`.

Publishing your javadoc online
==============================

1. Create a *public*_repo with the name `{{page.num}}-javadoc-yourgithubid` under the <https://github.com/{{page.org}}> organization with a `README.md` (it is not necessary to include a .gitignore).
2. cd into your ~/cs56 directory (or into whatever directory you cloned your `{{page.num}}-yourgithubid` repo).  You want to clone your `{{page.num}}-javadoc-yourgithubid` repo into the same directory so that they are siblings, side-by-side in the same directory.
3. We will now add some lines into your build.xml that copy the generated javadoc from your private repo to the public repo, 
   and we'll set the default branch of the public repo to be gh-pages.
   That process is explained in detail here: [Javadoc: publishing to github pages from private repo](https://ucsb-cs56-pconrad.github.io/topics/javadoc_publishing_to_github_pages_from_private_repo)
4. Once you've followed the instructions in the link at step 3, your javadoc should be available online at a URL similar to
   the following one (but with your githubid instead of `yourgithubid`).

```
    https://UCSB-CS56-F17.github.io/{{page.num}}-javadoc-yourgithubid/javadoc/index.html
```

If you run into difficulties, ask your mentor/TA/instructor if in class, or ask on Piazza if outside of class.

When you are finished
=====================

When you are finished, you'll have:

* the url of your completed repo (e.g. <https://github.com/{{page.org}}/{{page.num}}-yourgithubid> )
* the url of your javadoc (which will be in a separate public repo)
  * URL of that repo will be: <https://github.com/{{page.org}}/{{page.num}}-javadoc-yourgithubid>
  * When you push to your GitHub pages source branch, which should be `master` if you followed the [directions](https://ucsb-cs56-pconrad.github.io/topics/javadoc_publishing_to_github_pages_from_private_repo), that repo's content will be published at
    <https://{{page.org}}.github.io/{{page.num}}-javadoc-yourgithubid/javadoc/index.html>

Visit the [lab01 assignment on Gauchospace]({{page.gauchospace_link}}) to paste these URLs into the "online text" submission area for {{page.num}}.   Please make that your links are clickable&mdash;there are [instructions here on how to make links on Gauchospace clickable](https://ucsb-cs56-pconrad.github.io/topics/gauchospace_clickable_urls)

f you worked in a pair, please register your pair as a group in submit.cs for {{page.num}} before submitting. One partner’s submission on submit.cs counts for both of you.
