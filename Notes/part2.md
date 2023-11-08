# Part 2: Tokenization / Lexing

## What is it? 

Input/Program -> Compiler{ -> Tokenizer (Tokens)}

```
if (34 < 57) { 
    return 7;
  }
```


Code as a series of Tokens:
- IfToken
- LeftParentoken
- NumberToken(34)
- LessThanToken
- NumberToken(57)
- RightParenToken
- LeftCurlyToken
- ReturnToken
- NumberToken(7)
- SemicolonToken
- RightCurlyToken

### Expression Grammar

````
var is a Variable
type ::= `int` | `bool`
vardec ::= `(` `vardec` type var expression `)`
expression ::= num | `true` | `false` | var |  `(` op expression expression `)`

// Added Loop
loop ::= `(` `while` expression statement `)`
assign ::= `()` `=` var expression `)`
statement::= vardec | loop | assign
//End Loop

op ::= `x` | `-`|  `&&` | `||`
program ::= vardec*

// * means zero or more of the word
// Other form: program ::= epsilon (empty) | vardec program

````

Possible Tokens:

> Names are arbitrary

- IdentifierToken(String) 
- NumberToken(int)
- BoolToken
- LeftParenToken
- VardecToken
- RightParenToken
- TrueToken
- FalseToken
- WhileToken
- SingleEqualsToken
- PlusToken
- MinusToken
- LogicalAndToken
- LogicalOrToken
- LessThanToken

### Input to Tokens

```
 (vardec int x 7) 
```

Tokenized
```
  LeftParenToken
  VardecToken
  IntToken
  IdentifierToken("X")
  NumberToken(7)
  RightParenToken
```

````
//Java

public class MyClass {
  public static void main(String[] args){
    
  }
}

````

Tokenized:

Tokenizer looks a word by word basis, no context.

Context would be during parsing afaik

- PublicToken
- ClassToken
- IdentifierToke("MyClass")
- IdentifierToken("main")
- IdentifierToken("String")

 ## Tokenizer Testing

```

import static org.junit.Assert.assertEquals();
import static org.junit.Assert.assertArrayEquals();
import org.junit.Test;


public class TokenizerTest {
	@Test
	public void testIdentifierEquals() {
		assertEquals(new IdentifierToken("foo"), new IdentifierToken("foo"));
	}

	@Test
	public void testTokenizeIdentifier() {
		final Token[] tokens = Tokneizer.tokenize("bar");
		final Token[] expected = new Token[]{new IdentifierToken("bar")};
		assertArrayEquals(expected, tokens);
	}
	
	@Test
	public void testTokenizeWholeVardec() {
		final Token[] tokens = Tokneizer.tokenize("(vardec int x 7)");
		final Token[] expected = new Token[]{
		new LeftParenToken(),
		new VardecToken(),
		new IntToken,
		new IdentifierToken("x"),
		new NumberToken(7),
		new RightParenToken()
		};
		assertArrayEquals(expected, tokens);
	}
	


}
```