# Multi-Tenant Document Isolation

Legal-document retrieval makes tenant isolation especially important.

## Resource ownership

At minimum, tenant ownership should be clear for:

- documents
- document chunks
- embeddings/index metadata
- conversations
- messages
- analyses
- citations

## Scoped retrieval

Conceptually:

```python
search(
    query_embedding,
    filters={
        "tenant_id": active_tenant,
        "document_id": {"in": allowed_documents}
    }
)
```

This example is illustrative, not production source code.

## Defense in depth

Isolation should be enforced at multiple layers where available:

1. authentication and membership
2. application authorization
3. relational query scoping
4. vector/search metadata filtering
5. storage access controls
6. cache-key scoping

The objective is to avoid any path where a valid user can cause another tenant's legal material to enter their model context.
