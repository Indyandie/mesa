# Markdown Table (Feedback)
> This PR is only used for discussion and should not be merged. Instead, comments within this PR should lead to new issues which are resolved by the repository owner. This isn't to discourage raising PR's directly against changes but just a faster way to give lots of initial feedback.

[fcb]: https://spec.commonmark.org/0.30/#fenced-code-blocks
This implementation is inspired by [Fenced Code Blocks][fcb], the [CSV format][rfc4180] guidelines, and, of course, existing Table extensions.

## Proposal

A __table fence__ is a sequence of 3 consecutive commas `,`. A __table__ begins with a __table fence__, preceded by no spaces.

[rfc4180]: https://datatracker.ietf.org/doc/html/rfc4180z
The contents of a __table__ follow the [CSV Format][rfc4180] guidelines the following differences:
- Trailing spaces are not considered part of a field and should be ignored.
- The first record is always the header line, the `<thead>`.

A comma `,` or pipe `|` character can be used to separate fields. To include a delimier (comma `,` or pipe `|`) as character in a field enclose the entire field in double-quotes `"`.

> Delimiters must be used consistently per row (record).

Inline markdown is supported on individual fields. This allows the possibility of block elements inside of cells enclosed with double-quotes.

The closing __table fence__ may be preceded by up to 3 spaces of indentation, and may be followed only by spaces or tabs, which are ignored.


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
delimiter | name | support
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
        <th>name</th>
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
        <th>name</th>
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

### Whitespace

Trailing whitespace are ignored.

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


It doesn't look great but i really like the functionality. Perhaps some sort of newline character could help the presentation.

#### Linebreaks

```
,,,
name       , block
list       , "- apple\n- bear\n- cat"
code block , "```shell\n# some code\n```"
headings   , "# Header\n## Another Header"
,,,
```

### Alignment 

For alignment I think it could support existing implementations.

```
,,,
Left            , Right                 , Center
:--             | --:                   | :-:
Stomp to the << , Stomp to the right >> , `2` hops this time, Left is default
,,,
```


The colon `:` character could be used on the header fields to define alignment. Here's what I'm thinking. 

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

