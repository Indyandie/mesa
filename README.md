# Markdown Table

This implementation was inspired by fenced `code block`, the [csv format][rfc4180] guidelines, and of course existing `table` extensions. 

## Proposal

A __table fence__ would be a sequence of at least 3 consecutive commas "`,`". A table begins with a __table fence__, preceded by no spaces.

[rfc4180]: https://datatracker.ietf.org/doc/html/rfc4180z
The contents of a table follow the [csv format][rfc4180] guidelines with some necessary differences. 
- Trailing spaces are not considered part of a field and should be ignored.
- The first record is always the header line, the `<thead>`.

A comma "`,`" or pipe "`|`" character can be used to separate values, a delimiter. To include a delimier (comma `,` or pipe `|`) as character in a field enclose the entire field in double-quotes `"`. 

> A delimiter must be used consistantly per row (record.)

Inline markdown is supported on individual fields. Block elements could potentially be supported inside of fields enclosed with double-quotes.

The closing table fence may be preceded by up to three spaces of indentation, and may be followed only by spaces or tabs, which are ignored.


### A basic table

```
,,,
1    , 2   , 3
one  , two , three
uno  , dos , tres
ichi , ni  , san
,,,
```

### Using pipes `|`

```
,,,
delimiter | name | support
comma     | ","  | Yes
pipe      | "|"  | Yes
,,,
```

### Whitespace

> Trailing whitespace is ignore

```
,,,
      pokemon, type           , emoji
pikachu   , electric , 🐭 ⚡️
  charmander,fire,🦎 🔥
onyx  ,            rock             , 🐍 🪨
,,,

Is the same as

,,,
pokemon    , type     , emoji
pikachu    , electric , 🐭 ⚡️
charmander , fire     , 🦎 🔥
onyx       , rock     , 🐍 🪨
,,,

,,,
pokemon,type,emoji
pikachu,electric,🐭 ⚡️
charmander,fire,🦎 🔥
onyx,rock,🐍 🪨
,,,
```

### Inline markdown

```
,,,
`code`      , __bold__
[link](url) , _italic_
,,,
```

### Blocks

Leveraging double-quotes tables could potentially support blocks on individual fields. I am not sure if this is good idea though.

```
name      , blocks
list      , "- a
- b
- c"
codeblock , "```
some code
```"
headings  , "# heading
## another heading"
```

It doesn't look great but i really like the functionality. Perhaps some sort of newline character could help the presentation.

```
,,,
name       , block
list       , "- apple\n- bear\n- cat"
code block , "```shell\n# some code\n```"
headings   , "# Heading\n## Another Heading"
,,,
```

### Alignment 

For alignment I think it could support existing implementations.

```
,,,
Left            , Right                 , Center
:--             , --:                   , :-:
Stomp to the << , Stomp to the right >> , `2` hops this time, Left is default
,,,
```

The colon `:` character could be used on the header fields to define alignment. Here's what I'm thinking. 

> The colon would be treated as a regular character past the first row. 

```
,,,
:Left , Right: , :Center: , Default         , "Colon:"
<<--  , -->>   , "--|--"  , Left is default , Colons `:` are ignored inside double-quotes
,,,
```
