# STAC API - Catalogs Extension

- **Title:** Catalogs
- **Conformance Classes:**
  - https://api.stacspec.org/v1.0.0/core (required)
  - https://api.stacspec.org/v1.0.0-beta.1/catalogs (required)
- **Scope:** STAC API - Core
- **Extension Maturity Classification:** Proposal
- **Dependencies:**
  - [STAC API - Core](https://github.com/radiantearth/stac-api-spec/blob/main/core)
  - [STAC API - Collections](https://github.com/radiantearth/stac-api-spec/tree/main/ogcapi-features)
- **Owner**: @jonhealy1

## Link Relations

Proper linking is critical for clients to navigate the federation structure.

### 1. The Global Root (`/`)
This is the entry point.
- `rel="data"`: MUST point to the `/catalogs` endpoint (the registry).
- `rel="child"`: MUST point to specific sub-catalogs (e.g., `/catalogs/usgs`).
- `rel="service-desc"`: Points to the OpenAPI definition.

### 2. The Sub-Catalog (`/catalogs/{catalogId}`)
This resource acts as the **Landing Page** for the provider.
- `rel="self"`: MUST point to `/catalogs/{catalogId}`.
- `rel="parent"`: MUST point to the Global Root (`/`).
- `rel="root"`: SHOULD point to the Global Root (`/`) to maintain a single navigation tree.
- `rel="data"`: MUST point to `/catalogs/{catalogId}/collections`.

## Endpoints

This extension introduces a new root path `/catalogs` and nests standard STAC API endpoints under specific catalog IDs.

| Method | URI | Description |
| :--- | :--- | :--- |
| `GET` | `/catalogs` | **The Registry.** Lists all available sub-catalogs. |
| `GET` | `/catalogs/{catalogId}` | **Sub-Catalog Root.** Acts as the Landing Page for the provider. |
| `GET` | `/catalogs/{catalogId}/conformance` | Conformance classes specific to this sub-catalog. |
| `GET` | `/catalogs/{catalogId}/collections` | Lists collections belonging to this sub-catalog. |
| `GET` | `/catalogs/{catalogId}/collections/{collectionId}` | Gets a specific collection definition. |
| `GET` | `/catalogs/{catalogId}/collections/{collectionId}/items` | **Item Search.** Fetches items from this specific collection. |
| `GET` | `/catalogs/{catalogId}/collections/{collectionId}/items/{itemId}` | Gets a single specific item. |
