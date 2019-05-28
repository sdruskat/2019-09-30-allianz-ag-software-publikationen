---
title:  'Die Hard 1.1024.0: <br/> Backward compatibility of a search engine with persistant IDs'
subtitle: 'deRSE19 - Conference for Research Software Engineers in Germany, 2019-06-04'
author: 
    - 'Thomas Krause (Humboldt-Universität zu Berlin)'
    - 'Stephan Druskat (Friedrich-Schiller-Universität Jena, Deutsches Zentrum für Luft- und Raumfahrt)'
theme: 'humboldt'
center: 'false'
slideNumber: 'true'
bibliography: 'literature.bib'
link-citations: no
mathjaxurl: "MathJax-release-2.7.4-electron/MathJax.js"
---

# Background

## The Hexatomic project

"A minimal infrastructure for the **sustainable** provision of extensible *multi-layer annotation software for linguistic corpora*"

- Funded under the call "Research Software Sustainability" issued by DFG under grant number GA 1288/11-1 
- Runs from October 2018 until September 2021.

. . .

- Thomas Krause: computer scientist who slipped into linguistics
- Stephan Druskat: English major who turned into software developer
- Both: Research Software Engineers

## ANNIS and its query language

A web browser-based search and visualization architecture for complex
multilayer *linguistic corpora* with diverse types of *annotation*.

::: {.center .col-container}

::: col
![](image/annis3_full.png){width=100%}
:::

::: col

- Annotations are structured information added to text 
- Used by expert users (linguists) to find and analyze linguistic phenomena
- ANNIS allows finding annotations and *combinations* of annotations with its domain specific query language AQL
- Each query returns a set of results, which can be analysed further
- Part of a collection of tools for linguists: corpus-tools.org
:::


:::


## Semantic Versioning

- Popularized by semver.org [@Preston-Werner]
- Explicit statement about compatibility between versions of API
- *MAJOR*.*MINOR*.*PATCH*
  - Only bug fixes when *PATCH* changes, API does not change
  - Additions to API marked as increase of *MINOR*
  - Removal and non-backward compatible changes needs an increase in *MAJOR*

. . .


Some open questions:

- What is part of the API in a complex piece of software with multiple components? 
  - REST-API?
  - Query language?
  - Data exchange format?
  - User Interface?

. . . 

- **Do we want to backward-compatible forever? Is there a “1.0 release anxiety”?**


## Persistent Identifiers (PIDs)



[![DOI](image/doi-annis.svg)](https://doi.org/10.5281/zenodo.1161400)



- In general: resolving an identifier to a resource (digital or or not)
- **Should never change**: you can print it in a book!
- Several systems exist, like e.g. DOI, handle.net, ...

. . . 

Some open questions:

- If a digital resource moves, who updates the reference?
- Who provides and pays the infrastructure?


# Achieving backward compatibility in ANNIS 4.x

## What is the digital object defined by ANNIS citation links?

- ANNIS allows generating short links to query results and single matches, e.g.
[https://korpling.org/annis3/?id=813c3146-2d10-4d0c-8a1f-1b5efc3c051a](https://korpling.org/annis3/?id=813c3146-2d10-4d0c-8a1f-1b5efc3c051a)
![](image/ridges.png)
- Glorified URL shortener: expands to a longer URL encoding the match and the actual query, e.g. https://korpling.org/annis3/#_q=bm9ybT0vZ8O2bm50Lw&_c=UklER0VTX[...]
-  Query is executed each time the link is opened, no result identifers are saved

## Backward compatibility

Problem:

- ANNIS 3: AQL queries are mapped to SQL queries and executed by PostgreSQL
- ANNIS 4: custom in-memory graph-based search engine written in Rust, which directly executes AQL [@Krause2019]

All old reference links should still work.

. . . 

Users printed these links in books.

. . .

Solution 1: keep the old software running forever (parallel to the new one)

. . . 

**Solution 2: Make sure that each query that has been referenced produces the same result in ANNIS 4 as in ANNIS 3 **

. . . 

- Execute each referenced query on both ANNIS 3 and 4
- Compare the results
- If successful: Migrate the links to the new ANNIS 4 installation


## Query language incompatibility is a feature

- New version will remove some query language functions and fix bugs in the query execution
- Backward compatibility means replicating these bugs

. . . 

:::  center

Remember me?

![](image/Internet_Explorer_6_Windows_XP.png)

:::

- We need a quirks mode like e.g.
  - Internet Explorer
  - Rust Editions ([https://doc.rust-lang.org/book/appendix-05-editions.html](https://doc.rust-lang.org/book/appendix-05-editions.html))


# Problems when changing the implementation for a query language

## Formalized semantics of the data model and the query language

XXX

## Not implemented functions of the query language

XXX

## Identifiers might change

XXX 


## Regular Expressions

XXX

## String ordering/collation

XXX

# Conclusion

## Conclusion

XXX

# Appendix

## References
