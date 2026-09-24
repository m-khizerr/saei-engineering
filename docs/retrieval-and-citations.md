# Retrieval & Citation Design

## Retrieval stages

A mature retrieval pipeline can be modeled as:

```text
user query
   ↓
query preparation
   ↓
authorized candidate retrieval
   ↓
ranking / reranking
   ↓
deduplication
   ↓
context selection
   ↓
generation
```

Not every deployment needs every stage. The architecture allows retrieval quality to evolve independently from the chat interface.

## Metadata filters

Semantic similarity alone cannot enforce business rules.

A retrieval request may need filters such as:

```ts
{
  tenantId,
  allowedDocumentIds,
  sourceType,
  jurisdiction,
  language
}
```

depending on the product context.

## Citation provenance

A searchable chunk should retain a provenance chain:

```text
chunk
  ↓
document
  ↓
page / section
  ↓
original source
```

That relationship should survive index rebuilds wherever practical.

## Evaluating retrieval

Useful test cases ask:

- Did the relevant source appear in the candidates?
- Was it ranked high enough to enter model context?
- Were unauthorized documents excluded?
- Were duplicate chunks wasting context?
- Could the citation be resolved back to the original source?

This separates retrieval failures from generation failures.
