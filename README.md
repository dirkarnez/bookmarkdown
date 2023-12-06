bookmarkdown
============
WIP
### Grammar
Parser
```antlr
parser grammar ExprParser;
options { tokenVocab=ExprLexer; }

document: block+ NEWLINE * EOF?;

/**
 * A document is one or more block elements.
 * http://daringfireball.net/projects/markdown/syntax#block
 */
block: NEWLINE*   // Blank lines at the begin of the document or extra blank lines between blocks are matched here.
       (heading
       )
     ;
     
heading: ID+ (NEWLINE);
```
Lexer
```antlr
lexer grammar ExprLexer;

ID: [a-zA-Z_][a-zA-Z_0-9]* ;
NEWLINE: '\r'? '\n';
```
