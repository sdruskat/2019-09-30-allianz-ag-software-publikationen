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

XXX

## Persistant Identifiers (PIDs)

XXX

# Achieving backward compatibility in ANNIS 4.x

## What is the digital object defined by ANNIS citation links?

XXX

## Testing each citation link

XXX

## Quirks Mode

XXX other examples of quirks mode (IE, Rust)

XXX classes of differences: not supported yet, actual error, old implementation was weird, will never be supported

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
