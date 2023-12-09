bookmarkdown
============
WIP
### Reference
- https://github.com/mar9000/antmark

### Grammar
Parser
```antlr
parser grammar ExprParser;
options { tokenVocab=ExprLexer; }

document: block+ NEWLINE* EOF?;

/**
 * A document is one or more block elements.
 * http://daringfireball.net/projects/markdown/syntax#block
 */
block: NEWLINE* heading listing;
text: NORMAL_CHAR | DIGIT;
heading: text+ NEWLINE EQUAL+ NEWLINE;
listing: SHARP+ SPACE text+ NEWLINE (HYPHEN SPACE text+ NEWLINE)+;
```
Lexer
```antlr
lexer grammar ExprLexer;

NORMAL_CHAR: [a-zA-Z];   // This never match a, b, ecc .
DIGIT: [0-9];

NEWLINE: '\r'? '\n';
EQUAL: '=';
SHARP: '#';
SPACE: ' ';
HYPHEN : '-';
```

### Reference
```antlr
primaryExpression
    : Identifier
    | Constant
    | StringLiteral+
    | '(' expression ')'
    | genericSelection
    | '__extension__'? '(' compoundStatement ')' // Blocks (GCC extension)
    | '__builtin_va_arg' '(' unaryExpression ',' typeName ')'
    | '__builtin_offsetof' '(' typeName ',' unaryExpression ')'
    ;


StringLiteral
    : EncodingPrefix? '"' SCharSequence? '"'
    ;

fragment SCharSequence
    : SChar+
    ;

fragment SChar
    : ~["\\\r\n]
    | EscapeSequence
    | '\\\n'   // Added line
    | '\\\r\n' // Added line
    ;
```
