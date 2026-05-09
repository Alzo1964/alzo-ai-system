# Publishing Studio Integration

## Purpose

WordPress supports Publishing Studio by serving as the destination for approved public content, editorial pages, knowledge packaging, and audience-facing documentation.

## Workflow

1. Ideas and drafts begin in Publishing Studio or the ALZO backend.
2. Editorial review confirms voice, structure, metadata, and publication intent.
3. Approved content is sent to WordPress as a draft, scheduled post, page, or custom content type.
4. Final formatting and SEO review occur in WordPress.
5. Publication status and performance signals return to the ALZO backend.

## Content Types

Potential WordPress content models include:

- Articles and essays.
- Documentation pages.
- Resource libraries.
- Campaign support content.
- Public reports or summaries.

## Metadata

Publishing sync should preserve:

- Title, subtitle, slug, and excerpt.
- Author or studio attribution.
- Category, tag, and content pillar.
- Review status and publication date.
- Source reference or backend content ID.

## API Connection

The custom plugin should handle content sync through authenticated backend endpoints. WordPress should receive only approved content and should return publication events, URL data, and performance metadata.

## Governance

WordPress is the publishing surface, not the editorial source of truth. Durable planning, drafts, templates, and editorial operating context should remain in the ALZO system unless intentionally published.
