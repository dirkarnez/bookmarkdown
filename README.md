bookmarkdown
============
WIP
### Reference
- https://github.com/mar9000/antmark
- [ANTLR Tutorial => Lexer rules in v4](https://riptutorial.com/antlr/topic/3271/lexer-rules-in-v4)

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

text: TEXT;
block: NEWLINE* heading listing;

heading: text NEWLINE EQUALLINE NEWLINE;
listing: SHARP+ SPACE text NEWLINE listingItem+;
listingItem: HYPHEN SPACE text NEWLINE;
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

TEXT: SChar+;
EQUALLINE: EQUAL+;
fragment SChar
    : ~["\\\r\n];
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


