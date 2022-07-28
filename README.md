# Markdown Table

[fcb]: https://spec.commonmark.org/0.30/#fenced-code-blocks
This implementation is inspired by [Fenced Code Blocks][fcb], the [CSV format][rfc4180] guidelines, and of course, existing Table extensions.

## Proposal

A **table fence** is a sequence of 3 or more consecutive commas `,`. A **table** begins with a **table fence**, preceded by no spaces.

[rfc4180]: https://datatracker.ietf.org/doc/html/rfc4180z
The contents of a **table** follow the [CSV Format][rfc4180] guidelines with the following differences:
- Leading and trailing spaces are not considered part of a field and should be ignored.
- The first record is always the header line, the `<thead>`.

A comma `,` or pipe `|` character can be used to separate fields. To include a delimiter (comma `,` or pipe `|`) as a character in a field enclose the entire field in double-quotes `"`.

> Delimiters must be used consistently per row (record).

Inline markdown is supported on individual fields (cells). The CSV Format guidelines allow the possibility of supporting block elements inside of cells enclosed with double-quotes.

The closing **table fence** may be preceded by up to 3 spaces of indentation, and may be followed only by spaces or tabs, which are ignored.


### A basic table

```
,,,
1    , 2   , 3
one  , two , three
uno  , dos , tres
ichi , ni  , san
,,,
```

#### HTML

```html
<table>
  <thead>
    <tr>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>one</td>
      <td>two</td>
      <td>three</td>
    </tr>
    <tr>
      <td>uno</td>
      <td>dos</td>
      <td>tres</td>
    </tr>
    <tr>
      <td>ichi</td>
      <td>ni</td>
      <td>san</td>
    </tr>
  </tbody>
</table>
```

#### Preview

<table>
  <thead>
    <tr>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>one</td>
      <td>two</td>
      <td>three</td>
    </tr>
    <tr>
      <td>uno</td>
      <td>dos</td>
      <td>tres</td>
    </tr>
    <tr>
      <td>ichi</td>
      <td>ni</td>
      <td>san</td>
    </tr>
  </tbody>
</table>

### Using pipes `|`

```
,,,
delimiter | char | support
comma     | ","  | Yes
pipe      | "|"  | Yes
,,,
```

#### HTML

```html
<table>
  <thead>
    <th>
      <tr>
        <th>delimiter</th>
        <th>char</th>
        <th>pipe</th>
      </tr>
    </th>
  </thead>
  <tbody>
    <tr>
      <td>comma</td>
      <td>,</td>
      <td>Yes<td>
    </tr>
    <tr>
      <td>pipe</td>
      <td>|</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>
```

#### Preview

<table>
  <thead>
    <th>
      <tr>
        <th>delimiter</th>
        <th>char</th>
        <th>pipe</th>
      </tr>
    </th>
  </thead>
  <tbody>
    <tr>
      <td>comma</td>
      <td>,</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>pipe</td>
      <td>|</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

#### Mix and match delimiters

```
,,,
pipes1 | pipes2 | pipes3
comma1 , comma2 , comma2
comma1 , comma2 , comma2
comma1 , comma2 , comma2
comma1 , comma2 , comma2
comma1 , comma2 , comma2
,,,

,,,
comma1 , comma2 , comma2
pipes1 | pipes2 | pipes3
pipes1 | pipes2 | pipes3
pipes1 | pipes2 | pipes3
pipes1 | pipes2 | pipes3
pipes1 | pipes2 | pipes3
,,,

,,,
comma1 , comma2 , comma2
pipes1 | pipes2 | pipes3
comma1 , comma2 , comma2
pipes1 | pipes2 | pipes3
comma1 , comma2 , comma2
pipes1 | pipes2 | pipes3
```

### Whitespace

Leading and trailing whitespaces are ignored.

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

#### HTML

```html
<table>
  <thead>
    <tr>
      <th>pokemon</th>
      <th>type</th>
      <th>emoji</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>pikachu</td>
      <td>electric</td>
      <td>🐭 ⚡️</td>
    </tr>
    <tr>
      <td>charmander</td>
      <td>fire</td>
      <td>🦎 🔥</td>
    </tr>
    <tr>
      <td>onyx</td>
      <td>rock</td>
      <td>🐍 🪨</td>
    </tr>
  </tbody>
</table>
```

#### Preview

<table>
  <thead>
    <tr>
      <th>pokemon</th>
      <th>type</th>
      <th>emoji</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>pikachu</td>
      <td>electric</td>
      <td>🐭 ⚡️</td>
    </tr>
    <tr>
      <td>charmander</td>
      <td>fire</td>
      <td>🦎 🔥</td>
    </tr>
    <tr>
      <td>onyx</td>
      <td>rock</td>
      <td>🐍 🪨</td>
    </tr>
  </tbody>
</table>

### Inline markdown

```
,,,
inline
__bold__
_italic_
`code`
[link](https://spec.commonmark.org)
,,,
```

#### HTML

```html
<table>
  <thead>
    <tr>
      <th>inline</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>bold</strong></td>
    </tr>
    <tr>
      <td><em>italic</em></td>
    </tr>
    <tr>
      <td><code>code</code></td>
    </tr>
    <tr>
      <td><a href="https://spec.commonmark.org/">link</a></td>
    </tr>
  </tbody>
</table>
```

#### Preview

<table>
  <thead>
    <tr>
      <th>inline</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>bold</strong></td>
    </tr>
    <tr>
      <td><em>italic</em></td>
    </tr>
    <tr>
      <td><code>code</code></td>
    </tr>
    <tr>
      <td><a href="https://spec.commonmark.org/">link</a></td>
    </tr>
  </tbody>
</table>

### Blocks

Tables support block elements on individual cells by using double-quotes.

> This requires some discussion to vet the pros and cons.

```
name      , blocks
list      , "- a
- b
- c"
codeblock , "```
some code
```"
headings  , "# Header
## Another Header"
```

#### HTML

```html
<table>
  <thead>
    <tr>
      <th>name</th>
      <th>blocks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>list</strong></td>
      <td>
        <ul>
          <li>a</li>
          <li>b</li>
          <li>c</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><strong>fence code block</strong></td>
      <td>
        <pre><code>some code
        </code></pre>
      </td>
    </tr>
    <tr>
      <td><strong>headers</strong></td>
      <td>
        <h1>Header</h1>
        <h2>Another Header</h2>
      </td>
    </tr>
  </tbody>
</table>
```

#### Preview

<table>
  <thead>
    <tr>
      <th>name</th>
      <th>blocks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>list</strong></td>
      <td>
        <ul>
          <li>a</li>
          <li>b</li>
          <li>c</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><strong>fence code block</strong></td>
      <td>
        <pre><code>some code
        </code></pre>
      </td>
    </tr>
    <tr>
      <td><strong>headers</strong></td>
      <td>
        <h1>Header</h1>
        <h2>Another Header</h2>
      </td>
    </tr>
  </tbody>
</table>

#### Linebreaks

Use `\n` to create linebreaks within a cell.

> 🤔 Other options: `"ln"`, "br", "\n"

```
,,,
name       , block
list       , "- apple\n- bear\n- cat"
code block , "```shell\n# some code\n```"
headings   , "# Header\n## Another Header"
,,,
```

### Alignment 

Existing Table implementations use the colon `:` in the header fields to indicate alignment, which could work here as well.

```
,,,
Left            , Right                 , Center
:--             | --:                   | :-:
Stomp to the << , Stomp to the right >> , `2` hops this time, Left is default
,,,
```
> The colon would be treated as a regular character past the first row. 

```
,,,
:Left , Right: , :Center: , Default               , "Colon:"
<<--  , -->>   , "--|--"  , The default alignment , Colons `:` are ignored inside double-quotes
,,,
```

#### HTML

```html
<table>
  <thead>
    <tr>
      <th align="left">Left</th>
      <th align="right">Right</th>
      <th align="center">Center</th>
      <th>Default</th>
      <th>Colon:</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="left">&lt;&lt;--</td>
      <td align="right">--&gt;&gt;</td>
      <td align="center">--|--</td>
      <td>The default alignment</td>
      <td>Colons <code>:</code> are ignored inside double-quotes</td>
    </tr>
  </tbody>
</table>
```

#### Preview

<table>
  <thead>
    <tr>
      <th align="left">Left</th>
      <th align="right">Right</th>
      <th align="center">Center</th>
      <th>Default</th>
      <th>Colon:</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="left">&lt;&lt;--</td>
      <td align="right">--&gt;&gt;</td>
      <td align="center">--|--</td>
      <td>The default alignment</td>
      <td>Colons <code>:</code> are ignored inside double-quotes</td>
    </tr>
  </tbody>
</table>

