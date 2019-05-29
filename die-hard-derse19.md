---
title:  'Die Hard 1.1024.0: <br/> Backward compatibility of a search engine with persistent IDs'
subtitle: 'deRSE19 - Conference for Research Software Engineers in Germany, 2019-06-04'
author: 
    - 'Thomas Krause (Humboldt-Universität zu Berlin)'
    - 'Stephan Druskat (Friedrich Schiller University Jena, German Aerospace Center (DLR))'
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
- Runs from October 2018 until September 2021
[TODO check fades!]

. . .

- Thomas Krause: computer scientist who slipped into linguistics
- Stephan Druskat: English M.A. turned software developer & computer scientist
- Both: Research Software Engineers

## ANNIS and its query language

Web browser-based search and visualization architecture for *linguistic corpora* with diverse types of *annotation*. Part of the [corpus-tools.org](http://corpus-tools.org) collection of tools for linguists. [TODO ***WHAT HAVE I SAID ABOUT CITING SOFTWARE 💀🔥🤬***]

::: {.center .col-container}

::: col

![](image/annis3_full.png){width=100%}

:::

::: col

- Annotations are structured information added to text represented as a **graph with labels**
- Used by expert users (linguists) to **find and analyze linguistic phenomena**
- ANNIS allows finding annotations and *combinations* of annotations with its domain specific query language AQL:
  describes **nodes labels** and **joins them with operators**
- Each query returns a set of results for further automatic/manual analysis
:::


:::


## Semantic Versioning

- Popularized by [semver.org](https://semver.org/) [@Preston-Werner]
- Explicit statement about compatibility between versions of API
- *MAJOR*.*MINOR*.*PATCH*
  - Only bug fixes when *PATCH* changes, API does not change
  - Additions to API marked as increase of *MINOR*
  - Removal and non-backward compatible changes need an increase in *MAJOR*

. . .


Some open questions:

- What is part of the API in a complex piece of software with multiple components? 
  - REST API?
  - Query language?
  - Data exchange format?
  - User Interface?

. . . 

- **Do we want to backward-compatible forever? Is there a “1.0 release anxiety”?**


## Persistent Identifiers (PIDs)



[![DOI](image/doi-annis.svg)](https://doi.org/10.5281/zenodo.1161400)



- In general: resolving an identifier to a resource (digital or not)
- **Should never change**, i.e., you can print it in a book!
- Several systems exist, e.g. DOI, handle.net, ...

. . . 

Some open questions:

- If a digital resource moves, who updates the reference?
- Who provides and funds the infrastructure?


# Achieving backward compatibility in ANNIS 4

## What is the digital object defined by ANNIS citation links?

- ANNIS allows generating short links to query results and single matches, e.g.,
[https://korpling.org/annis3/?id=813c3146-2d10-4d0c-8a1f-1b5efc3c051a](https://korpling.org/annis3/?id=813c3146-2d10-4d0c-8a1f-1b5efc3c051a)
![](image/ridges.png)
- Glorified URL shortener: expands to a longer URL encoding the match and the actual query paramters, e.g., https://korpling.org/annis3/#_q=bm9ybT0vZ8O2bm50Lw&_c=UklER0VTX[...]
-  Query is executed each time the link is opened, no result identifiers are saved

## Backward compatibility

Problem:

- ANNIS 3: AQL queries are mapped to SQL queries and executed by PostgreSQL
- ANNIS 4: custom in-memory graph-based search engine written in Rust, which directly executes AQL [@Krause2019]

All old reference links should still work.

. . . 

Users literally printed these links in books.

. . .

Solution 1: Keep the old software running forever (in parallel to the new one)

. . . 

**Solution 2: Make sure that each query that has been referenced, produces the same result in ANNIS 4 as in ANNIS 3**

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

- We need a quirks mode emulating old behavior like, e.g.,
  - Internet Explorer
  - Rust Editions ([https://doc.rust-lang.org/book/appendix-05-editions.html](https://doc.rust-lang.org/book/appendix-05-editions.html))


# Selected problems from the migration process

## Formalized semantics of the data model and the query language

- In an ideal world a query language is formally defined like, e.g., Datalog [TODO what is Datalog]
- All you need to restore a digital object would be the data and any implementation conforming to the specification

. . . 

::: {.center .large}

Real world: SQL

:::

. . . 


- SQL versions have been standardized (..., SQL-93, SQL:1999, SQL:2003, ...)
- Various implementations (MySQL, PostgreSQL, Oracle, DB2, SQLite, ...) with different support for the standard and vendor extensions
- AQL has only two implementations, but the first implementation heavily relied on semantics of SQL and its [TODO their?] implementation in PostgreSQL
- Problems of changing AQL implementations are similar to those in **migrating an application from one SQL implementation to another**

## Un-implemented functions of the query language

- A query language can accumulate a large number of features over time:
  - AQL has a large number of binary operators that describe the relation between two nodes in the graph
- Not all of them are orthogonal to each other and therefore can be replaced [TODO can or cannot?]

. . .

- Move implementation of such features to a specific code path that separate the “real” query language from the ugly parts
- Check for actual used PIDs/reference links to make it transparent if a query language feature has been used, and therefore needs emulation

. . . 

- If too hard to implement:

::: center

![](image/unsupported-query.png){height=200px}
  
:::

## Identifiers might change

- Each node in the graph has a URI and an internal identfier
- Matches are lists of URIs and additional names for the label the match refers to
- A match [for a query] is only the same if all URIs are the same

. . .

People will use weird names

- Spaces, slashes, umlauts, ...
- Double percent-escaped characters

. . . 

- Everything Unicode has to offer

::: center

![](image/unicode.png){}

::: tiny
[https://github.com/minimaxir/big-list-of-naughty-strings](https://github.com/minimaxir/big-list-of-naughty-strings)
:::

:::

$\rightarrow$ Importing data via IDs -- and comparing them -- is hard 

## Regular Expressions

Regular expressions are an important part of AQL for matching node and edge labels

. . .

```sql
-- PostgreSQL
SELECT * FROM t WHERE a ~ 'val.*';
-- MySQL 
SELECT * FROM t WHERE a REGEXP 'val.*';
```
- Syntax varies from each implementation, even if „supporting POSIX“
- Regular expression engines often allow a search for non-regular expressions, such as backreferences and other extensions: some implementations trade features for speed (e.g RE2 from Google)
- “Power users“ will use all regular features available, even if never officially documented


## String ordering/collation

For query results, the order of the results is important, e.g. when refering to matches
$\rightarrow$ ANNIS 4 reference migration checks order of the matches as well


What is the result of the following SQL query?
```sql
SELECT '_' < '-';
```

. . .

- Depends on your localization! `LANG=C` != `LANG=en_US.UTF-8` != `LANG=de_DE.UTF-8`
- PostgreSQL allows to configure the collation for a column of a table explicitly
```sql
CREATE TABLE test1 (a text COLLATE "de_DE");
```

::: center
Anyone ever defined their tables this way *before* having collation issues?
:::

# Conclusion

## Conclusion

- ANNIS 4 is currently in public beta
- Users created 12.828 reference links so far on *our* public ANNIS 3 installation alone

. . .

::: center
All but 137 queries are known to give the same results in ANNIS 4 [TODO is this good or bad?]
:::

. . . 



- Issues remaining
  - Regular expressions
  - Unsupported binary operators (might not fix)
  - Actual bugs

. . .

- Having these reference links gives us a huge **real world test set**
- **Automatic migration** for persistent IDs
- **Transparency** for the **administrator** which queries she/he can migrate to a new instance
- **Transparency** for the **end-user** if a query is known not to work, no silent failure
- We will be able to **retire ANNIS 3** while keeping all these reference links valid

# Appendix

## References
