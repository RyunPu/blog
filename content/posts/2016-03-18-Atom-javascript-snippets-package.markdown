---
layout: post
title:  "Atom javascript snippets package"
date:   2016-03-18
categories: ['editor']
tags: ['atom']
---

### [javascript-snippets](https://atom.io/packages/javascript-snippets)

JavaScript & NodeJS Snippets for Atom

### snippets

| Trigger | Name                                     | Body                                                                                                                                    |
|---------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| ac      | appendChild                              | $\{1:document\}\.appendChild\($\{2:elem\}\);                                                                                            |
| ae      | addEventListener                         | $\{1:document\}\.addEventListener\('$\{2:event\}', function\(e\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}\);                                   |
| afn     | anonymous function                       | function\($\{1:arguments\}\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}                                                                          |
| al      | alert                                    | alert\('$\{1:msg\}'\);                                                                                                                  |
| apply   | function apply                           | $\{1:methodName\}\.apply\($\{2:context\}, \[$\{3:arguments\}\]\)                                                                        |
| asd     | assert\.deepEqual                        | assert\.deepEqual\($\{1:actual\}, $\{2:expected\}\);                                                                                    |
| ase     | assert\.equal                            | assert\.equal\($\{1:actual\}, $\{2:expected\}\);                                                                                        |
| asn     | assert\.notEqual                         | assert\.notEqual\($\{1:actual\}, $\{2:expected\}\);                                                                                     |
| ca      | classList\.add                           | $\{1:document\}\.classList\.add\('$\{2:class\}'\);                                                                                      |
| call    | function call                            | $\{1:methodName\}\.call\($\{2:context\}, $\{3:arguments\}\)                                                                             |
| cd      | console\.dir                             | console\.dir\($\{1:obj\}\);                                                                                                             |
| cdf     | createDocumentFragment                   | $\{1:document\}\.createDocumentFragment\(\);                                                                                            |
| ce      | console\.error                           | console\.error\($\{1:obj\}\);                                                                                                           |
| cel     | createElement                            | $\{1:document\}\.createElement\($\{2:elem\}\);                                                                                          |
| ci      | console\.info                            | console\.info\($\{1:obj\}\);                                                                                                            |
| cl      | console\.log                             | console\.log\($\{1:obj\}\);                                                                                                             |
| co      | confirm                                  | confirm\('$\{1:msg\}'\);                                                                                                                |
| cr      | classList\.remove                        | $\{1:document\}\.classList\.remove\('$\{2:class\}'\);                                                                                   |
| ct      | classList\.toggle                        | $\{1:document\}\.classList\.toggle\('$\{2:class\}'\);                                                                                   |
| cw      | console\.warn                            | console\.warn\($\{1:obj\}\);                                                                                                            |
| de      | debugger                                 | debugger;                                                                                                                               |
| desc    | describe                                 | describe\('$\{1:description\}', function\(\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}\);                                                       |
| fe      | forEach                                  | $\{1:myArray\}\.forEach\(function\($\{2:elem\}\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}\);                                                   |
| fi      | for in                                   | for \($\{1:prop\} in $\{2:obj\}\) \{\\n\\tif \($\{2:obj\}\.hasOwnProperty\($\{1:prop\}\)\) \{\\n\\t\\t$\{0:// body\.\.\.\}\\n\\t\}\\n\} |
| fn      | function                                 | function $\{1:methodName\} \($\{2:arguments\}\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}                                                       |
| ga      | getAttribute                             | $\{1:document\}\.getAttribute\('$\{2:attr\}'\);                                                                                         |
| gc      | getElementsByClassName                   | $\{1:document\}\.getElementsByClassName\('$\{2:class\}'\);                                                                              |
| gi      | getElementById                           | $\{1:document\}\.getElementById\('$\{2:id\}'\);                                                                                         |
| gt      | getElementsByTagName                     | $\{1:document\}\.getElementsByTagName\('$\{2:tag\}'\);                                                                                  |
| ih      | innerHTML                                | $\{1:document\}\.innerHTML = '$\{2:elem\}';                                                                                             |
| iife    | immediately\-invoked function expression | \(function\($\{1:window\}, $\{2:document\}\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}\)\($\{1:window\}, $\{2:document\}\);                     |
| ita     | it asynchronous                          | it\('$\{1:description\}', function\(done\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}\);                                                         |
| itp     | it pending                               | it\('$\{1:description\}'\);                                                                                                             |
| its     | it synchronous                           | it\('$\{1:description\}', function\(\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}\);                                                             |
| jp      | JSON\.parse                              | JSON\.parse\($\{1:obj\}\);                                                                                                              |
| js      | JSON\.stringify                          | JSON\.stringify\($\{1:obj\}\);                                                                                                          |
| me      | module\.exports                          | module\.exports = $\{1:name\};                                                                                                          |
| ofn     | function as a property of an object      | $\{1:functionName\}: function\($\{2:arguments\}\) \{\\n\\t$\{3:// body\.\.\.\}\\n\}                                                     |
| pe      | process\.exit                            | process\.exit\($\{1:code\}\);                                                                                                           |
| pm      | prompt                                   | prompt\('$\{1:msg\}'\);                                                                                                                 |
| pr      | prototype                                | $\{1:ClassName\}\.prototype\.$\{2:methodName\} = function\($\{3:arguments\}\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}                         |
| qs      | querySelector                            | $\{1:document\}\.querySelector\('$\{2:selector\}'\);                                                                                    |
| qsa     | querySelectorAll                         | $\{1:document\}\.querySelectorAll\('$\{2:selector\}'\);                                                                                 |
| ra      | removeAttribute                          | $\{1:document\}\.removeAttribute\('$\{2:attr\}'\);                                                                                      |
| rc      | removeChild                              | $\{1:document\}\.removeChild\($\{2:elem\}\);                                                                                            |
| re      | require                                  | require\('$\{1:module\}'\);                                                                                                             |
| sa      | setAttribute                             | $\{1:document\}\.setAttribute\('$\{2:attr\}', $\{3:value\}\);                                                                           |
| si      | setInterval                              | setInterval\(function\(\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}, $\{1:delay\}\);                                                            |
| st      | setTimeout                               | setTimeout\(function\(\) \{\\n\\t$\{0:// body\.\.\.\}\\n\}, $\{1:delay\}\);                                                             |
| tc      | textContent                              | $\{1:document\}\.textContent = '$\{2:content\}';                                                                                        |
| us      | use strict                               | 'use strict';                                                                                                                           |
