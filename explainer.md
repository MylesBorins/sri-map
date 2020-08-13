## Explainer

Currently there is no way to enforce or check integrity of resources being imported as an ESModule.

There is an existing [SRI Standard](https://www.w3.org/TR/SRI/) at W3C which outlines [cryptographic hashing functions](https://www.w3.org/TR/SRI/#cryptographic-hash-functions), [an algorithm for response verification](https://www.w3.org/TR/SRI/#response-verification-algorithms), and defines [an integrity attribute](https://www.w3.org/TR/SRI/#the-integrity-attribute) which is utilized by various elements in HTML. There is an [MDN Article on SRI](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity) that does a great job of covering some of the higher level benefits as well as provides examples of SRI being used to verify resource in script tags.

There have been [a number](https://github.com/tc39/notes/blob/master/meetings/2017-05/may-23.md#16iib-module-import-options-discussion-potentially-for-stage-1) of [discussions](https://github.com/tc39/notes/blob/master/meetings/2020-02/february-6.md#module-attributes-status-update) at TC39 that have resulted in the committee holding the opinion that Integrity data belongs out of band. There are a number of reasons for this, module cycles and maintainability being the some of the easier to explain.

WICG is already incubating the Import Map proposal, but the explainer outlines that [integrity is currently out of scope](https://github.com/WICG/import-maps#supplying-out-of-band-metadata-for-each-module). There is a possibility that an integrity map and an import map could merge into a single manifest, but it would appear that it should be explored and spec'd on its own merits first.

As we see more adoption of modules in JavaScript and individuals consuming resources VIA HTTPS URLs I think having a mechanism for integrity checks with be extremely important, having a standard mechanism for this even more so.

### Examples

A straw proposal for syntax below
```json
{
  "https://example.com/example-framework.js": "sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/uxy9rx7HNQlGYl1kPzQho1wx4JwY8wC"
```

The left hand side is the resource, the right hand side the SRI. This would scale to various resource types, not limited to JavaScript. it could integrate into the existing integrity checks already in HTML for any resources in the map. I would imagine that it would likely support all the types of meta data currently support [by the integrity attribute](https://www.w3.org/TR/SRI/#the-integrity-attribute)
