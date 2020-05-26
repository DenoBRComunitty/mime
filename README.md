<!--
  -- This file is auto-generated from src/README_js.md. Changes should be made there.
  -->
# Mime

A comprehensive, compact MIME type module.

## Version 2 Notes

Version 2 is a breaking change from 1.x as the semver implies.  Specifically:

* `lookup()` renamed to `getType()`
* `extension()` renamed to `getExtension()`
* `charset()` and `load()` methods have been removed

If you prefer the legacy version of this module please `npm install mime@^1`.  Version 1 docs may be found [here](https://github.com/broofa/node-mime/tree/v1.4.0).

## Uso | Use

```javascript
import * as mime from 'https://raw.githubusercontent.com/DenoBRComunitty/mime/master/mod.js'

mime.getType('txt');                    // ⇨ 'text/plain'
mime.getExtension('text/plain');        // ⇨ 'txt'
```

### new Mime(typeMap, ... more maps)

A maioria dos usuários deste módulo não precisará criar instâncias do Mime diretamente.
No entanto, se você deseja criar mapeamentos personalizados, faça o seguinte

Most users of this module will not need to create Mime instances directly.
However if you would like to create custom mappings, you may do so as follows
...

```javascript
// Require Mime class
import { Mime } from 'https://raw.githubusercontent.com/DenoBRComunitty/mime/master/mod.js';

// Define mime type -> extensions map
const typeMap = {
  'text/abc': ['abc', 'alpha', 'bet'],
  'text/def': ['leppard']
};

// Create and use Mime instance
const myMime = new Mime(typeMap);
myMime.getType('abc');            // ⇨ 'text/abc'
myMime.getExtension('text/def');  // ⇨ 'leppard'
```


### mime.getType(pathOrExtension)

Obtenha o tipo mime para o caminho ou extensão especificado. Por exemplo.

Get mime type for the given path or extension.  E.g.

```javascript
mime.getType('js');             // ⇨ 'application/javascript'
mime.getType('json');           // ⇨ 'application/json'

mime.getType('txt');            // ⇨ 'text/plain'
mime.getType('dir/text.txt');   // ⇨ 'text/plain'
mime.getType('dir\\text.txt');  // ⇨ 'text/plain'
mime.getType('.text.txt');      // ⇨ 'text/plain'
mime.getType('.txt');           // ⇨ 'text/plain'
```
`null` é retornado nos casos em que uma extensão não é detectada ou reconhecida

`null` is returned in cases where an extension is not detected or recognized

```javascript
mime.getType('foo/txt');        // ⇨ null
mime.getType('bogus_type');     // ⇨ null
```

### mime.getExtension(type)
Obtenha extensão para o tipo mime especificado. Opções de charset (geralmente incluídas em
Cabeçalhos do tipo de conteúdo) são ignorados.

Get extension for the given mime type.  Charset options (often included in
Content-Type headers) are ignored.

```javascript
mime.getExtension('text/plain');               // ⇨ 'txt'
mime.getExtension('application/json');         // ⇨ 'json'
mime.getExtension('text/html; charset=utf8');  // ⇨ 'html'
```

### mime.define(typeMap[, force = false])
Defina [mais] mapeamentos de tipo.

`typeMap` é um mapa de type -> extensions, conforme documentado em `new Mime`, acima.

Por padrão, esse método gera um erro se você tentar mapear um tipo para um
extensão já atribuída a outro tipo. Passando `true`para o argumento `force` 
suprime esse comportamento (substituindo qualquer mapeamento anterior).

Define [more] type mappings.

`typeMap` is a map of type -> extensions, as documented in `new Mime`, above.

By default this method will throw an error if you try to map a type to an
extension that is already assigned to another type.  Passing `true` for the
`force` argument will suppress this behavior (overriding any previous mapping).

```javascript
mime.define({'text/x-abc': ['abc', 'abcd']});

mime.getType('abcd');            // ⇨ 'text/x-abc'
mime.getExtension('text/x-abc')  // ⇨ 'abc'
```

## DenoBR