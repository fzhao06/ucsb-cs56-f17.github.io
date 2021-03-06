---
layout: lab
num: lab08
ready: true
desc: "Recursive Descent Parsing"
assigned: 2017-11-28 09:30:00.00-8
due: 2017-12-10 17:00:00.00-8

parsing_starter_01: "https://github.com/UCSB-CS56-F17/parsing-starter-01"
parsing_starter_02: "https://github.com/UCSB-CS56-F17/parsing-starter-02"
parsing_starter_03: "https://github.com/UCSB-CS56-F17/parsing-starter-03"
parsing_starter_04: "https://github.com/UCSB-CS56-F17/parsing-starter-04"

parsing_starter_01_git: "https://github.com/UCSB-CS56-F17/parsing-starter-01"
parsing_starter_02_git: "https://github.com/UCSB-CS56-F17/parsing-starter-02"
parsing_starter_03_git: "https://github.com/UCSB-CS56-F17/parsing-starter-03"
parsing_starter_04_git: "https://github.com/UCSB-CS56-F17/parsing-starter-04"

parsing_starter_javadoc: "https://ucsb-cs56-f17.github.io/parsing-starter-javadoc/docs/apidocs/"

tutorial_repo: "https://ucsb-cs56-pconrad.github.io/tutorials/parsing/"
submit_cs_link: "https://submit.cs.ucsb.edu/form/project/914/submission"
submit_cs_join_groups: "https://submit.cs.ucsb.edu/p/914/group"
course_github_organization: UCSB-CS56-F17
---

<style>
 div.tip {
   
   margin-left:auto; 
   margin-right:auto; 
   width:80%; 
   border: 10px inset red; 
   padding: 0.5em;
   margin-top: 1em;
   margin-bottom: 1em;
 }
</style>

<div style="display:none">
http://ucsb-cs56-f17.github.io/lab/lab08/
</div>

# Notes

* This lab may be done individually or in pairs
* This lab does not require much actual coding, but it does require a lot of reading of both text and code in order to understand what code to write.  
* This lab is in three phases, and it will help if you leave yourself at least three work sessions to do it (don't try to do it all on the last day before it's due.)
* The final deadline, 5pm on Friday of dead week, is STRICT, out of a concern for having the work leaking into final exam preparation, and a need to wrap up other grading before the final exam.
* The submit.cs link is coming soon---we are refactoring it to be more generous with extra credit.

# Summary 

In this assignment, you will add some features to an existing parser
and interpreter of arithmetic expressions.

You should start by reading the [CS56 Parsing
Tutorial]({{page.tutorial_repo}}).  It contains important background
information about parsing, grammars, tokens, etc.

<div class="tip" markdown="1">

The remainder of this writeup assumes that you have thoroughly read and understood the information in the [CS56 Parsing Tutorial]({{page.tutorial_repo}}).  

*If you have not, it will not make any sense to you.*

</div>


# What You'll Implement #

The starter code you are given implements an intepreter for integer expressions involving `+`, `-`, `*`, `/`, parentheses, and unary minus (minus sign in front of an expression.)

Your task is to update all three components of the starter code&mdash;the tokenizer, parser, and interpreter&mdash;to handle the following new features:

- Six comparison operators, (`==`, `!=`, `<`, `<=`, `>`, `>=`) returning 0 for false, and 1 for true
- An exponent operator, `**` (i.e. `3**2` evalutes to $$ 3^2 = 9 $$ and `2**3` evaluates to $$ 2^3 = 8 $$.

The exponent operator associates to the right rather than the left:

* `2**3**2` should be intepreted as `2**(3**2)`, i.e. $$ 2^9 = 512 $$
* `2**3**2` should be NOT intepreted as `(2**3)**2`, i.e. $$ 8^2 = 64 $$

This is not the same as addition and multiplication, which associate to the left.  Fortunately, this detail has already been taken
care of for you by careful design of the grammar.  Provided you implement the grammar correctly, there won't be any problem with 
implementing the correct "associativity" of the operators.


# A different way of using git and github

We've already seen at least two different ways of using git and github in this course to work with some starter code:
* Starting from a repo that contains only a README.md file, cloning it, copying some files in, and then doing a
   `git add...`, `git commit...`, `git push...` 
* Forking an existing repo and making a pull request.

This assignment won't use either of this. Instead, you'll do these steps:

* create an initially empty repo on github
* separately, create an  initially empty repo on your CSIL account (or your own machine)&mdash;we'll
   call this your "local" repo).
* In your local repo You'll then manually
   create a remote called `origin` linking your local repo with the one on github.
* You'll then also create remotes for repos that represent several steps in the process of completing the lab.

All of this is explained in detail below.

# How the grammar will change

As a reminder from the [CS56 Parsing Tutorial]({{page.tutorial_repo}}), the starter code handles the following grammar:

```
expression ::= additive-expression
additive-expression ::= multiplicative-expression ( ( '+' | '-' ) multiplicative-expression ) *
multiplicative-expression ::= primary ( ( '*' | '/' ) primary ) *
primary ::= '(' expression ')' | INTEGER | '-' primary
```

Instead, you'll modify it to implement this grammar:

```
expression ::= comparison-expression
comparison-op ::= '==' | '!=' | '<' | '<=' | '>' | '>='
comparison-expression ::= additive-expression ( comparison-op additive-expression ) *
additive-expression ::= multiplicative-expression ( ( '+' | '-' ) multiplicative-expression ) *
multiplicative-expression ::= exponent-expression ( ( '*' | '/' ) exponent-expression ) *
exponent-expression ::= primary '**' exponent-expression | primary
primary ::= '(' expression ')' | INTEGER | '-' primary
```

You'll need to refer back to this "before and after" grammar frequently during the lab.

# The starter code for the repos

The starter code for this assignment is in four repos, as explained in the table below:
<style>
div.repo-table * td:first-child a {
   white-space: pre;
}
div.repo-table * td {
  padding: 8px;
  max-width: 36em;
}
</style>

<div class="repo-table">

| Link to Repo |  What it contains  |  How you'll use it |
|--------------|--------------------|--------------------|
| [parsing-starter-01]({{ page.parsing_starter_01 }}) | A working interpreter for integer expressions involving `+`,`-`,`*`,`/` and `()` | You will start with an empty repo called `lab08_yourgithub`. <br> You'll add a remote for this repo, pull it into yours to get started on the assignment. |
| [parsing-starter-02]({{page.parsing_starter_02}}) | `parsing-starter-01` plus: <br>&nbsp;(1) stubs for factory methods to create new tokens for `<=`, `<`, `>`, `>=`, `==`, `!=`, and `**`, <br>&nbsp;(2) JUnit tests to see if you can tokenize those operators. | You'll add a remote for this repo, pull it into yours to add tests for the tokenizing phase to your code base. |
| [parsing-starter-03]({{page.parsing_starter_03}}) | `parsing-starter-02` plus:<br>&nbsp;(1) stubs for factory methods to create AST Nodes for `<=`, `<`, `>`, `>=`, `==`, `!=`, and `**`, <br>&nbsp;(2) JUnit tests to see if you can parse expressions involving these operators. |  You'll add a remote for this repo, pull it into yours to add tests for the tokenizing phase to your code base. |
| [parsing-starter-04]({{page.parsing_starter_04}}) | `parsing-starter-03` plus: <br> tests for the interpreter phase of the assignment. |  You'll add a remote for this repo, pull it into yours to add tests for the tokenizing phase to your code base. |

Javadoc for the starter code is available at <{{page.parsing_starter_javadoc}}>. The javadoc was
generated from the `parsing-starter-04` code.

</div>


# Initial setup of your github repo

1. Start by creating an EMPTY PRIVATE repo in the organization {{course_github_organization}}.

   The name should be `lab08_githubid` or for a pair, `lab08_githubid1_githubid2` (put the
   pair partner's github ids in lexicographic order)

   By EMPTY, we mean DO NOT add a README.md, .gitignore, or license file.  (You might not have done this
   before in this course.)

   You'll get a screen that looks like this after creating such a repo:

2. In the place where you would normally have cloned the repo, instead, make an empty directory with the
   same name as the repo, like this (here, `cgaucho` and `kdelplaya` are your githubids).

   ```
   mkdir lab08_cgaucho_kdelplaya
   ```

3. `cd` into that directory and use `git init` to turn it into a git repository, like this:

   ```
   cd lab08_cgaucho_kdelplaya
   git init
   ```

4. Now you will manually add a remote called `origin` that points back to your (currently)
   empty repo on github.com.  (When you clone, that happens automatically, but this time, we are
   doing it by hand so that you see how things work under the hood.)   Substitute the actual ssh
   url of your github repo in for the example below.     You can find this URL on the web page
   on github.com for your (currently empty) repo:

   ```
   git remote add origin git@github.com:UCSB-CS56-F17/lab08_cgaucho_kdelplayaa.git
   ```

5. Now, add additional remotes as follows.  These commands are to be typed exactly as shown below

   <div>
   <code>git remote add parsing-starter-01 {{page.parsing_starter_01}}</code><br>
   <code>git remote add parsing-starter-02 {{page.parsing_starter_02}}</code><br>
   <code>git remote add parsing-starter-03 {{page.parsing_starter_03}}</code><br>
   <code>git remote add parsing-starter-04 {{page.parsing_starter_04}}</code><br>
   </div>

6. Do the following command to pull the initial starter code into your empty repo:

   ```
   git pull parsing-starter-01 master
   ```

7. Do the following command to push that code back to your origin repo (the one you created
   for yourself on github.com, e.g. <https://github.com/ucsb-cs56-f17/lab08-cgaucho-kdelplayaa>.

   ```
   git push origin master
   ```

   Check on github.com that you see the code there.

   You are now ready for the step where you familiarize yourself with the starter code.


# General Comments

## Not a lot of code, but a lot of challenge

The bulk of the difficulty of this assignment is expected to be in determining exactly what in the existing interpreter must be modified, without dramatically changing how the interpreter works.   

The amount of new code you need to add is relatively small, and the code is relatively straightforward.  

However, figuring out exactly what code you need to add, and where to add it, may be moderately to very challenging.   <em>This is typical of a good bit of the coding that you do in real-world development projects</em>.




# Comparison operators

All six of the comparison operators compare the integer values on the left and right.  They will each return a true or false value, with true represented as the integer `1`, and false represented as the integer `0`.    Accordingly, there is still only one *type* in the system, namely *integer*.

In the tokenizer, adding these operators will entail handling `==`, `!=`, `<`, `<=`, `>`, and `>=` as fundamentally new tokens.  You'll need to defined new classes for these tokens that extend the [`Token`]({{page.javadoc_prefix}}edu/ucsb/cs56/pconrad/parsing/tokenizer/Token.html){: data-ajax="false" } class defined in `src/edu/ucsb/cs56/pconrad/parsing/tokenizer/Token.java`.   As models, you might look at the classes that currently extend that class.  You can figure out what those are from looking at the javadoc for [`class edu.ucsb.cs56.pconrad.parsing.tokenizer.Token`]({{page.javadoc_prefix}}edu/ucsb/cs56/pconrad/parsing/tokenizer/Token.html){: data-ajax="false" } and looking at the list of "Direct Known Subclasses".

You get to make some design decisions.  One of them is this:

* You can decide to either add six entirely new Token classes, e.g. `EqualsToken`, `NotEqualsToken`, etc.
* Or, you could implement just one class, e.g. `ComparisonOperatorToken`, or `CompOpToken`, or whatever you want to call it, that in some way handles the variation among the six different operators (in the same way that there is only one class for `IntToken`, even though with 32 bits, there are in fact over four billion different possible integer tokens.

In order to leave that decision up to you, the tests are decoupled from the actual implementation of the specific concrete classes that extend `Token` by means of a Factory object.   The `TokenFactory` is an interface that specifies the names of methods to produce every kind of token that is needed in a test case.      There is a `DefaultTokenFactory` class where you specify the concrete classes that actually correspond to the various tokens.    

# Updating the Parser

As a reminder, the code you started with implements this grammar, based on one found on the Wikipedia page for [Operator Precedence Parser](https://en.wikipedia.org/wiki/Operator-precedence_parser) (retrieved 06/13/2017):

```
expression ::= additive-expression
additive-expression ::= multiplicative-expression ( ( '+' | '-' ) multiplicative-expression ) *
multiplicative-expression ::= primary ( ( '*' | '/' ) primary ) *
primary ::= '(' expression ')' | INTEGER | '-' primary
```

Instead, you'll be implementing this grammar that has two additional levels:

```
expression ::= comparison-expression
comparison-op ::= '==' | '!=' | '<' | '<=' | '>' | '>='
comparison-expression ::= additive-expression ( comparison-op additive-expression ) *
additive-expression ::= multiplicative-expression ( ( '+' | '-' ) multiplicative-expression ) *
multiplicative-expression ::= exponent-expression ( ( '*' | '/' ) exponent-expression ) *
exponent-expression ::= primary '**' exponent-expression | primary
primary ::= '(' expression ')' | INTEGER | '-' primary
```

* `comparison-expression` for handling comparison operators
* `exponent-expression` for handling exponentiation operators

This involves not only modifying the parsing code that implements the productions, but adding new kinds of AST nodes as well.


# Modifying the interpreter

The interpreter will also need to be modified to handle the seven new operators (six comparison operators, and exponent operator).

Expressions involving comparison operators will be evaluated and will return either `1` for true, or `0` for false.   This means that there is a new type of entity that can be part of the Abstract Syntax Trees (ASTs).  You'll need to understand the code that implements the ASTs, and determine what needs to be changed to allow for this new structure.   

You'll do something similar for the exponent operator.

The `main` function defined in `src/edu/ucsb/cs56/pconrad/parsing/Main.java` provides a "Read/Eval/Print" loop (REPL) for the combined tokenizer/parser/interpreter.    This is sometimes also called a "Command Line Interface", though we don't really have any commands, except for "q" for quit.  This should work properly with the new operations you have added, and you **should not** modify `main` in any way.

# Understanding the Starter Code

The starter code you are given is fairly complex.    The [CS56 Parsing Tutorial]({{page.tutorial_repo}}) has lots of information to help you.  We are not going to repeat that information here&mdash;we are only going to suggest&mdash;again&mdash;that you thoroughy read that tutorial.


# What to do if you get thrown into vim

When pulling code from another repo, git will sometimes throw you into vim in order to write a commit message.
You'll need to know how to save (write) and exit (quit) in order to proceed.  Here's how:

<div class="tip" markdown="1">

# How to save your work and exit from vim

You might also get thrown into vim here or at some future point in the
course of this lab.  To get out, use `<ESC>:wq` (that's hit the esc
key, then type colon, then wq).

</div>


# Things to try with the initial starter code

Once you've done the `git pull parsing-starter-01 master` to bring in the starter code:

1. Try doing an `ant test` on the starter code.  The code should compile, and the tests should pass.
2. Try running the code with `ant jar && java -jar build/jar/CS56Parser.jar`.  You should get a prompt for a "read-eval-print" loop 
    where you can type in expressions, and the parser will evaluate them.

# Proceeding to the first phase of coding: the tokenizer

You are now ready to pull in the tests for the additional features, i.e. the addition of the relational operators and the exponentiation operator.   We have organized the tests so that they incrementally build on top of each other, allowing you to first get your tokenizer working, then your parser, and finally your evaluator.

To bring the tests for the tokenizer into your repository, run the following commands:

```
git pull parsing-starter-02 master
git push origin master
```

<div class="tip" markdown="1">

When you do the `git pull starter update_tokenizer`, you might get thrown into vim with the message at the top 
of the screen `Merge branch ...` etc. 

This is an automatic commit message, because pulling in the starter code is doing a commit.

To finish the commit, use this sequence of keys to save and quit from vim: `<ESC>:wq` (that's hit the esc key, then type colon,
then wq). 

</div>

## Suggested order of work for tokenizer phase

If you run `ant test`, you should see that some tests now do not pass.

Start by implementing the `makeEqualsToken` and the `makeNotEquals`
methods in `DefaultTokenFactory`
(`src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/DefaultTokenFactory.java`),
which are now required by the updated `TokenFactory` interface
(`src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/TokenFactory.java`).
This will require you to add tokens for `==` and `!=`.  There are a
variety of ways to accomplish this; the only constraint is that these
new tokens must implement the `Token` interface
(`src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/Token.java`).

Then continue with implementations of the other four comparison
operator tokens, and the exponent operator token.  This is necessary
just to get the code to compile.

Then, to get the tests to pass, modify the `Tokenizer.java` to add in
the new states and transitions needed to recognize the new tokens you
have added.


The bulk of the work will be in recognizing the new tokens.  This will
likely entail adding in new states to the `Tokenizer`.  If you do end
up adding new states, you may want to draw out the state machine
representing what you are handling first, in order to make sure your
fundamental design is correct.  Ideally, you should avoid adding in a
state unless you are absolutely sure it needs to be there; extra
states mean extra code, which means more room for bugs to come into
play.



# Working on the parser

Once you have your tokenizer compiling and passing all the tests, you're ready to start on the parser.  You can bring in tests for the parser like so:

```
git pull parsing-starter-03 master
git push origin master
```

You should follow the same development procedures to update the parser as you did with the tokenizer.

## Steps to get the parser tests to pass

You will first need to get `DefaultASTFactory` (`src/main/java/edu/ucsb/cs56/pconrad/parsing/syntax/DefaultASTFactory.java`) compiling by providing implementations for the `makeEqualsNode` and `makeNotEqualsNode` methods, which are now required by the updated `ASTFactory` interface (`src/main/java/edu/ucsb/cs56/pconrad/parsing/syntax/ASTFactory.java`).  This will require editing or adding files to the code in `syntax`.

Continue with the four other comparison operators, and the exponent operator.

If you add in whole AST nodes, they must implement the `AST` interface (`src/main/java/edu/ucsb/cs56/pconrad/parsing/syntax/AST.java`).

Then, focus on the code in `Parser.java` and making it correspond to the new productions in the grammar.  

Depending on how you approach the problem, you may (or may not) find it necessary to modify the `OperatorScaffold`, since it currently is based on an assumption that every operator will be a single character, which is no longer true.     There are ways of writing the code that require this file to change, and other ways that don't.  Which approach you take is up to you.


# Working on the evaluator

Once the tokenizer is compiling and passing all the tests, you can start on the evaluator, which is the last component you'll need to implement.  Tests for the evaluator can be brought in like so:

```
git pull parsing-starter-03 master
git push origin master
```

Depending on your design, it is likely that actually updating the evaluator to handle the new types of ASTs will be a relatively small change.    The changes are likely to be either exclusively (or mostly) in the file `Evaluator.java`.

When all tests are passing, you are almost ready to try submission on submit.cs.

## Submitting ##

<div class="tip" markdown="1">
# The submit.cs link is coming soon

I'm refactoring the submit.cs tests to try to help you get more partial credit.

The previous version was pretty much "all or nothing", which isn't as helpful as I'd like it to be for folks that manage to get at least part of the assignment complete.  I'd like the new version to be able to give partial credit in cases where the code at least successfully passes, for example, some or all of the tokenizer tests.   
</div>

You'll submit via submit.cs here: {{ page.submit_cs_link }}

In contrast to some of your previous submissions, you should **not** make a publicly accessible Javadoc for your code.
A large portion of the work for this lab is in how you structure your classes and methods, which usually will be included with the Javadoc.  The javadoc is therefore in the `.gitignore`.

Instead, if you want to view your javadoc, you can view your javadoc by looking at the files you generate in a browser.   

# Restrictions #

To ensure that your code will compile and pass the tests on submit.cs, you should avoid modifying the following files:

- `src/main/java/edu/ucsb/cs56/pconrad/parsing/Main.java`
- `src/main/java/edu/ucsb/cs56/pconrad/parsing/InterpreterInterface.java`
- `src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/TokenFactory.java`
- `src/main/java/edu/ucsb/cs56/pconrad/parsing/syntax/ASTFactory.java`
- Any of the files under `src/test/java/`

The above restrictions are not arbitrary.  If any changes are made to
the above files, it very likely indicates that your code will fail to
pass the tests on submit.cs.    This is also somewhat realistic of a
production setting, where certain implementation details are fixed.

Other than the above restrictions, you may make any modifications necessary to make the tests pass.
This includes adding in new files and modifying existing files.

# General Suggestions #

As previously stated, you should first focus on getting the tests for
the tokenizer to pass, then the tests for the parser to pass, and
finally the tests for the evaluator to pass.

While it's possible to pull in all the tests at once, you'll be making
much more work for yourself if you do this; in this case, effectively,
you won't be able to properly test anything until **all** code has
been written.

Additionally, because each component builds on the other (i.e., the
parser needs the tokenizer, and the evaluator needs the parser), this
becomes a practical problem if we apply end-to-end testing.

For example, your evaluator and parser might work just fine, but if
your tokenizer is broken, we cannot run `Main`, so we can't actually
test the tokenizer and the parser easily.

It is expected that some edits will need to span multiple components.

For example, if an AST node were removed, then this would require
modifications to both the parser and the evaluator, as both deal with
AST nodes (the parser produces them while the evaluator uses them).
That said, if edits in one component require many edits in other
components, you might want to stop and rethink your design.  This
isn't necessarily wrong, and you are free to make such edits, but you
might be making a lot more work for yourself than necessary.

While the provided code has been heavily tested internally, it is not
guaranteed to be bug-free.  Additionally, it is not guaranteed to be
entirely clean; you might take issue with some of the design choices
made.  While your focus should be on getting everything up and
running, if cleaning up the code will make your life easier, then feel
free to do so.

You will likely spend much more time *thinking* about the code you
want to write as opposed to *actually writing* code.  This may feel
frustrating, especially if you're used to measuring process by the
number of lines of code you've written.  **This is normal.** In
professional development settings, developers often average only about
[8-10 lines of code written per
day](http://codebetter.com/patricksmacchia/2012/01/23/mythical-man-month-10-lines-per-developer-day/).
Most time is spent figuring out what needs to be written.


# Suggestions for Devising Your Own Tests #

As previously stated, while the provided code has been heavily tested internally, the provided test suite
may not test every contingency.

For the tokenizer, there need to be tests which cover every kind of token which can be created.
Because whitespace is treated specially, you should also have tests ensuring that extra whitespace in different spots (e.g., before a number) does not negatively impact the result.

For the parser, there need to be tests which collectively cover every
alternative of every production at least once.  For example, you
should have a test for each operator.  As another example, for
productions involving a repeat like `e*`, you should have a case for
zero, one, and two instances of `e`.

For the evaluator, there should be tests for every kind of operator, including special cases like division by zero.

Whenever you're in doubt, write a test.  This means that if you see
code you're not confident about, you should immediately write a test
to try to expose a bug in it.


<div class="tip" markdown="1">
## Some Hints:

Consider the following cases:

* What should happen if there is whitespace or something unexpected in the middle of a `==` or `!=` token, e.g. if the input is `2=3` or `2! =3` ?
* What should happen if the input ends in the middle of a `==` or `!=` token, e.g. `2+3=` or `4/5!` ?

</div>

# Submission

Please submit your work two ways:

* Please make a submission on submit.cs at: <{{page.submit_cs_link}}>
    *   If working in a pair: Please register your pair on submit.cs using the "Join Groups" feature.
* Submission via submit.cs is sufficient; you do not need to submit on Gauchospace, or in any other way.


Be sure that <b>if you are working in a pair</b>, that you have added your group via the "Join Groups" feature <{{page.submit_cs_join_groups}}> 

----

Credits: This lab primarily written by Kyle Dewey, with edits by Phill Conrad.  Additional helpful suggestions from Hiranya Jayathilaka, and others.


<div style="display:none">
http://ucsb-cs56-f17.github.io/lab/lab08/
</div>


# Appendix: Dealing with  merge conflicts 

You may get merge conflicts with you pull from parsing-starter-02

```
169-231-160-151:lab08_cgaucho_kdelplaya pconrad$ git pull parsing-starter-02 master
remote: Counting objects: 465, done.
remote: Compressing objects: 100% (141/141), done.
remote: Total 465 (delta 299), reused 403 (delta 239), pack-reused 0
Receiving objects: 100% (465/465), 71.26 KiB | 503.00 KiB/s, done.
Resolving deltas: 100% (299/299), completed with 84 local objects.
From https://github.com/UCSB-CS56-F17/parsing-starter-02
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> parsing-starter-02/master
Auto-merging src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/TokenFactory.java
Auto-merging src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/DefaultTokenFactory.java
CONFLICT (content): Merge conflict in src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/DefaultTokenFactory.java
Automatic merge failed; fix conflicts and then commit the result.
169-231-160-151:lab08_cgaucho_kdelplaya pconrad$ 
```

Here's what you do to fix this:

1.  Type `git status`

   This will show you, in case the output has gotten lost on your screen, which files have merge conflicts.
   
   169-231-160-151:lab08_cgaucho_kdelplaya pconrad$ git status

```
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:

	modified:   README.md
	modified:   docs/index.md
	modified:   src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/TokenFactory.java
	new file:   src/test/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/TokenizerAddonsTest.java

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/DefaultTokenFactory.java

169-231-160-151:lab08_cgaucho_kdelplaya pconrad$ 
```
   
   We see that we need to edit `DefaultTokenFactory.java`.

2.  Edit the file(s) that need to be merged.  Look for the `<<<<<` `====`, `>>>>>` lines that mark the "before and after" sections.   Decide what lines to keep, and what to delete, and then delete the  `<<<<<` `====`, `>>>>>` markers.

3.  Do `git status` again.  The important part of the output is this.  If you don't see this output, then you may still
have other merge conflicts to fix.

```
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)
```

But if you do that get that, it's time to do `git commit` to finish the merge.

Here's the full output.

```
169-231-160-151:lab08_cgaucho_kdelplaya pconrad$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

	modified:   README.md
	modified:   docs/index.md
	modified:   src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/DefaultTokenFactory.java
	modified:   src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/TokenFactory.java
	new file:   src/test/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/TokenizerAddonsTest.java

169-231-160-151:lab08_cgaucho_kdelplaya pconrad$ 
```

4.  Final step: `git commit...` and `git push origin master`

```
169-231-160-151:lab08_cgaucho_kdelplaya pconrad$ git commit -m "fix merge confict for bringing in parsing-starter-02"
[master a2add75] fix merge confict for bringing in parsing-starter-02
169-231-160-151:lab08_cgaucho_kdelplaya pconrad$ git push origin master
Counting objects: 432, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (83/83), done.
Writing objects: 100% (432/432), 63.26 KiB | 63.26 MiB/s, done.
Total 432 (delta 267), reused 418 (delta 261)
remote: Resolving deltas: 100% (267/267), completed with 53 local objects.
To github.com:UCSB-CS56-F17/lab08_cgaucho_kdelplaya.git
   3c3de76..a2add75  master -> master
169-231-160-151:lab08_cgaucho_kdelplaya pconrad$ 
```

# ADDITIONAL HINTS (Friday, December 8, 11:15am)

## Tokenizing Steps:

1. Realize that the error output you get will be a bit misleading at first.

   Consider this test:

   ```
     @Test
     public void testGtExpression() {
	assertArrayEquals(new Token[] { tf.makeIntToken("12"),
					tf.makeGreaterThanToken(),
					tf.makeIntToken("13") },
	    Tokenizer.tokenizeToArray("12 > 13"));
    }
   ```

   And consider the stub code that makes this compile:

   ```
     public Token makeGreaterThanToken() { return new ErrorToken("stub"); }

   ```

   That results in the following test failure output:

   ```
    Testcase: testGtExpression(edu.ucsb.cs56.pconrad.parsing.tokenizer.TokenizerAddonsTest):	FAILED
    arrays first differed at element [1]; expected:<ErrorToken(stub)> but was:<ErrorToken(>)>
    junit.framework.AssertionFailedError: arrays first differed at element [1]; expected:<ErrorToken(stub)> but was:<ErrorToken(>)>
    	at edu.ucsb.cs56.pconrad.parsing.tokenizer.TokenizerAddonsTest.testGtExpression(TokenizerAddonsTest.java:119)    
   ```

   But, note that we are not really "expecting" an `<ErrorToken(stub)>` at all!  What we are expecting is
   something like a `<GreaterThanToken>`, or a `<RelOpToken('<')>`, or something of this nature.   The
   exact details of the concrete implementation are up to you&mdash;that's why we are using the Factory Design
   Pattern.

   In any case, clearly the first job is to replace all of these stubs in `DefaultTokenFactory.java` with actual
   concrete methods that do the right thing.  That means you have to decide what classes you are going to implement
   for the tokens for these operators:

   * `<`, `<=`, `>`, `>=`, `==`, `!=` and `**`
   

   The code that forms the basis of what you'll be modifying is in the directory:

   * `src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/`

   Sample files you can use as examples include these: `PlusToken.java`, `MinusToken.java`, etc.

   Once you've created those, you can replace the stub methods in `DefaultTokenFactory.java` with calls to
   code to create the correct tokens.

   Then, you should at least get sensible error messages such as:

   ```
   arrays first differed at element [1]; expected:<GTToken(>)> but was:<ErrorToken(>)>
   junit.framework.AssertionFailedError: arrays first differed at element [1]; expected:<GTToken(>)> but was:<ErrorToken(>)>
   	at edu.ucsb.cs56.pconrad.parsing.tokenizer.TokenizerAddonsTest.testGtExpression(TokenizerAddonsTest.java:119)     
   ```

   Then, it's time to fix the tokenizer so that it does the right thing.

2. The next step involves designing a finite state automaton to parse the new tokens.

   For the `**` token, you'll want a transition from the existing state for the `*` operator to another state for the `**`
   operator.

   In `src/main/java/edu/ucsb/cs56/pconrad/parsing/tokenizer/Tokenizer.java` we see that the state
   that accepts the TimesToken() is state `4`, and we see that `7` is the last state that is currently
   used.

   ```java
      fsa.addState(4, s -> new TimesToken() );
   ```

   So, we can create a new state 8:
   
   ```java
      fsa.addState(8, s -> new ExponentToken() );
   ```

   And add a transition from state 4 to state 8 for input of `*` (the second `*`):
   
   ```
     fsa.addTransition('*',4,8);
   ```
   ```

   For the `<` and `<=` tokens, for example, you'll need:
     * a transition from state `0` on input `<` to a new state where you'll return a `<` token if the valid input ends there,
     * and a transition from *that* state to yet another state where you'll return a `<=` token if the valid input ends there.

   Those two states might be numbered 9 and 10.   It's up to you what specific numbers
   you assign to the states; it shouldn't matter as long as you tokenize everything correctly.

   Continue in this way for the four other relational operators.
   
   

## Parsing Steps:

1. Replace the stubs in the DefaultASTFactory with actual nodes that implement something like
   the +, *, -, and / operators.

2. In Parser.java, you need to modify the various routines as needed to implement the changes
   to the grammar.

   For example, while the old start production was:

   ```
   expression ::= additive-expression
   ```

   Resulting in code:

   ```
    private ParseResult<AST> parseExpression(final int pos) throws ParserException {
        return parseAdditiveExpression(pos);
    }
   ```

   The new start production is:

   ```plaintext
   expression ::= comparision-expression
   ```

   Which means that code needs to change to:


   ```java
    private ParseResult<AST> parseExpression(final int pos) throws ParserException {
        return parseComparisonExpression(pos);
    }
   ```

   Of course, the trouble is, there is no such method `parseComparisonExpression` yet.

   You have to write one.   You'll need to look at the other methods and how they correspond
   to the grammar productions to figure out what that method should look like.

   You'll also need to account for another change in the grammar.  The old production for
   `multiplicative-expression` had `primary` on the right hand side:

   ```plaintext
   multiplicative-expression ::= primary ( ( '*' | '/' ) primary ) *
   ```

   And the code that went along with that looks like this:

   ```java
   private class ParseMultiplicative extends ParseAdditiveOrMultiplicative {
        public ParseResult<AST> parseBase(final int pos) throws ParserException {
            return parsePrimary(pos);
        }
        public ParseResult<Operator> parseOp(final int pos) throws ParserException {
            return parseTimesDiv(pos);
        }
    }
   ```

   Now, instead of parsePrimary there, you'll need `parseExponentExpression`, another method
   that doesn't exist yet.

   The production for `exponent-expression` is recursive:

   ```
   exponent-expression ::= primary '**' exponent-expression | primary
   ```

   To implement a `parseExponentExpression` that corresponds to this production,
   here's what you need to do.  You can use `parsePrimary` as your model.

   * Call `parsePrimary`, and save the `ParseResult<AST>` that results as a variable of type `ParseResult<AST>` called `left`
   * Then see if the next token is `**`.
   * If it isn't, just return `left` as result of the function.
   * If it is, then call parseExponentExpression recursively, and save the resulting `ParseResult<AST>`
        as `right`.
   * Finally, return a `ParseResult<AST>` for an exponent operator
     that combines the left and right as the children.  The code for `ParseAdditiveOrMultiplicative.java` contains a hint on how to go about combining the left and right operands together with a binary operator, though that code is in a slightly different context, so you'll have to understand how to adapt it for your purposes.
   
# Evaluator steps:

Look in Evaluator.java.   The changes you need to make will be pretty obvious if you just read the code.  This is, honestly, the easiest part.  Just be sure to consider the special cases for the exponent operator, and the fact that you need to represent true as 1, and false as 0 (unlike C/C++, Java might not automatically convert `boolean` to `int` without some hints from you, the programmer).
