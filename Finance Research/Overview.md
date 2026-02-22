# Overview of Foundry for Finance (Research)

## Problem
We have a lot of financial documents (pension fund annual reports) to parse, and it will take a lot of time. 

## Operator
The resultant data will be used by a finance PhD student I support

## Result
Speed up research 

## Architecture
Media Set → Pipeline → Dataset (no need to elevate to Ontology here) → Workshop

## Design Decisions & Tradeoffs
 - Batch due to periodic static media set uploads
 - Page level splitting as this is the lowest level chunk with unlikely splits
 - No ontology elevation due to not needing action types

## Failure Modes / Production Considerations
 - Pipeline timeout at post 12 hours due to S3 key expiry, cannot use heavyweight llms to parse
 - Visualization parsing was referencing media reference of entire document, need to split with code prior
 - LLM parse scales poorly due to rate limits/using pages for chunks/lots of content
 - Some documents are pure image, meaning ocr works but not raw text, all text is print no handwriting so good there

Pre-deployment Considerations: 
 - Check trial run to make sure reasonable time (didn't do that with Opus 4.6 trial run and got a time out)
