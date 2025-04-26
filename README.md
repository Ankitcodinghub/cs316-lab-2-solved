# cs316-lab-2-solved
**TO GET THIS SOLUTION VISIT:** [CS316 Lab 2 Solved](https://www.ankitcodinghub.com/product/cs316-compilers-lab-solved-7/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;126891&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;1&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (1 vote)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS316  Lab 2 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (1 vote)    </div>
    </div>
1 Introduction

Your goal in this step is to generate the parser for your programming language’s grammar. By the end of this step your compiler should be able to take a source file as the input and parse the content of that file returning “Accepted” if the source file’s content is correct according to the grammar or “Not Accepted” if it is not.

Now the scanner created earlier will be modified to feed the parser. Instead of printing the tokens, the scanner has to return what token is recognized in each step.

2 Background

The job of a parser is to convert a stream of tokens (as identified by the scanner) into a parse tree: a representation of the structure of the program. So, for example, a parser will convert:

A := B + 4 ;

into a tree that looks something like:

One important thing to note is that the leaves of the tree are the tokens of of the program. If you read the leaves of the tree left to right (ignoring lambdas, since lambdas just represent the empty string), you get:

IDENTIFIER ASSIGN_OP IDENTIFIER PLUS_OP INTLITERAL SEMICOLON Which is exactly the tokenization of the input program!

2.1 Context-free grammars

To figure out how each construct in a program (an expression, an if statement, etc.) is decomposed into smaller pieces and, ultimately, tokens, we use a set of rules called a context-free grammar. These rules tell us how constructs (which we call “non-terminals”) can be decomposed and written in terms of other constructs and tokens (which we call “terminals”).

2.2 Micro

The context-free grammar that defines the structure of Micro (the name of your programming language) is:

/∗ Program ∗/

program −&gt; PROGRAM id BEGIN pgm_body END

id −&gt; IDENTIFIER

pgm_body −&gt; decl func_declarations

decl −&gt; string_decl decl | var_decl decl | empty

/∗ Global String Declaration ∗/

string_decl −&gt; STRING id := str ;

str −&gt; STRINGLITERAL

/∗ Variable Declaration ∗/

var_decl −&gt; var_type id_list ; var_type −&gt; FLOAT | INT any_type −&gt; var_type | VOID

id_list −&gt; id id_tail id_tail −&gt; , id id_tail | empty

/∗ Function Paramater List ∗/ param_decl_list −&gt; param_decl param_decl_tail | empty param_decl −&gt; var_type id

param_decl_tail −&gt; , param_decl param_decl_tail | empty

/∗ Function Declarations ∗/

func_declarations −&gt; func_decl func_declarations | empty

func_decl −&gt; FUNCTION any_type id ( param_decl_list ) BEGIN func_body END

func_body −&gt; decl stmt_list

/∗ Statement List ∗/

stmt_list −&gt; stmt stmt_list | empty

stmt −&gt; base_stmt | if_stmt | while_stmt

base_stmt −&gt; assign_stmt | read_stmt | write_stmt | return_stmt

/∗ Basic Statements ∗/

assign_stmt −&gt; assign_expr ;

assign_expr −&gt; id := expr

read_stmt −&gt; READ ( id_list ) ;

write_stmt −&gt; WRITE ( id_list ) ;

return_stmt −&gt; RETURN expr ;

/∗ Expressions ∗/

expr −&gt; expr_prefix factor

expr_prefix −&gt; expr_prefix factor addop | empty

factor −&gt; factor_prefix postfix_expr

factor_prefix −&gt; factor_prefix postfix_expr mulop | empty

postfix_expr −&gt; primary | call_expr

call_expr −&gt; id ( expr_list )

expr_list −&gt; expr expr_list_tail | empty

expr_list_tail −&gt; , expr expr_list_tail | empty

primary −&gt; ( expr ) | id | INTLITERAL | FLOATLITERAL

addop −&gt; + | −

mulop −&gt; ∗ | /

/∗ Complex Statements and Condition ∗/

if_stmt −&gt; IF ( cond ) decl stmt_list else_part ENDIF

else_part −&gt; ELSE decl stmt_list | empty

cond −&gt; expr compop expr

compop −&gt; &lt; | &gt; | = | != | &lt;= | &gt;=

while_stmt −&gt; WHILE ( cond ) decl aug_stmt_list ENDWHILE

aug_stmt_list −&gt; aug_stmt aug_stmt_list | empty

aug_stmt −&gt; base_stmt | aug_if_stmt | while_stmt | CONTINUE; | BREAK;

aug_if_stmt −&gt; IF ( cond ) decl aug_stmt_list aug_else_part ENDIF

aug_else_part −&gt; ELSE decl aug_stmt_list | empty

So this grammar tells us, for example, that an if_stmt looks like the keyword IF followed by an open parenthesis, followed by a cond expression followed by some decl (declarations) followed by a stmt_list followed by an else_part followed by the keyword ENDIF.

An input program matches the grammar (we say “is accepted by” the grammar) if you can use the rules of the grammar (starting from program) to generate the set of tokens that are in the input file. If there is no way to use the rules to generate the input file, then the program does not match the grammar, and hence is not a syntactically valid program.

3 Building a Parser

There are many tools that make it relatively easy to build a parser for a context free grammar (in class, we will talk about how these tools work): all you need to do is provide the context-free grammar and some actions to take when various constructs are recognized. The tools we recommend using are:

• Bison (this is a tool that is meant to work with scanners built using Flex). Note that integrating a flex scanner with bison requires a little bit of work. The process works in several steps that seem interlocking:

1. Define your token names as well as your grammar in your bison input file (called something like microParser.y)

2. Run bison -d -o microParser.cpp on microParser.ypp, it will create two output files: microParser.tab.cpp (which is your parser) and microParser.tab.hpp (which is a header file that defines the token names)

4. Run Flex on microLexer.l to produce lex.yy.cpp

5. In another file, main.c/cpp, write a main function (this file will also need to include microParser.tab.hpp).

Your main function should open the input file and store the file handle in a variable called yyin. Calling yyparse() will then run your parser on the file associated with yyin.

6. Compile together all of microParser.cpp, lex.yy.cpp, and your main.c/cpp function to build your compiler.

• ANTLR (this is the same tool that can also build lexers). You should define your grammar in the same .g4 file in which you defined your lexer.

1. Running ANTLR on that .g4 file will produce both a Lexer class and a Parser class.

3. You can then call a function with the same name as your top-level construct (probably program) on that parser to parse your input.

4 What you need to do

You must build upon your scanner’s implementation done for PA1.

The grammar for Micro is given above. All you need to do is have your parser parse the given input file and print Accepted if the input file correctly matches the grammar, and Not Accepted if it doesn’t (i.e., the input file cannot be produced using the grammar rules).

In Bison’s parser, you can define a function called yyerror (look at the documentation for the appropriate signature) that is called if the parser encounters an error.

In ANTLR, this is a little more complicated. You will need to create a new “error strategy” class (extend DefaultErrorStrategy) that overrides the function reportError. You can then set this as the error handler for your parser by calling setErrorHandler on your parser before starting to parse.

Sample inputs and outputs are provided to you along with the starter files that you need to get started on this assignment.

5 What you need to submit

• Place all the necessary code for your compiler (including the .l file) that you wrote yourself. You do not need to include the ANTLR jar files if you are using ANTLR.

• A Makefile with the following targets:

1. compiler: this target will build your compiler

2. clean: this target will remove any intermediate files that were created to build the compiler

3. dev: this target will print the same information that you printed in previous PA.

• A shell script (this must be written in bash) called runme that runs your compiler (scanner+parser). This script should take in two arguments: first, the input program file to be compiled and second, the filename where you want to put the compiler’s/parser’s output. You can assume that we will have run make compiler before running this script.

• You should tag your programming assignment submission as cs316pa2submission

Do not submit any binaries and do not delete/rename any of the files provided to you as part of the starter set. Your git repo should only contain source files; no products of compilation.
