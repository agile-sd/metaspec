# MetaSpec

**A structured DSL between LLMs and your Rails code.**

> 🚧 **Coming soon.** MetaSpec is being extracted from an internal tool used in production at [AgileSD](https://agilesd.com) and prepared for its first public release. The repository is intentionally empty for now — star or watch to be notified when the first version drops.

---

## The idea

MetaSpec is a declarative DSL for describing Rails resources, paired with a deterministic generator that produces models, controllers, views, routes, and migrations from the spec.

It exists to solve a specific problem in AI-assisted Rails development: **LLMs work much better on a small, structured target than when asked to write Rails code directly.** Instead of asking Claude (or any LLM) to produce a controller, you ask it to produce a short MetaSpec. A deterministic generator then writes the actual code, following the conventions encoded in your team's templates.

The result: dramatically lower token cost, fewer hallucinations, and code that consistently matches your team's style — because the structural decisions live in templates, not in the model's guesses.

---

## What a MetaSpec looks like

```
Resource Invoice
  attributes:
    number: string(limit:50)
    date: datetime
    net_total: decimal(18,5,default:0)
    state: integer

  enums:
    state: progress, finished, noticed

  relationships:
    belongs_to: company, client
    has_many: items: {class_name: "InvoiceItem", dependent: :destroy}

  validations:
    presence: company, client

  callbacks:
    before_save: calculate_totals

  controller:
    actions: crud
    tabs: items
```

A spec like that expands into a complete Rails resource — model, controller, views, routes, and a migration — all matching the conventions defined in your templates.

---

## What's coming in the first release

- The MetaSpec parser
- The code-generation engine, built on top of Rails generators
- A starter set of ERB templates as a working reference
- Documentation for writing your own templates
- A Claude skill for inferring templates from an existing Rails project

The structured-DSL pattern is the contribution. The templates are how each team makes it their own.

---

## Background

MetaSpec was originally built inside Warp, an internal development tool at [AgileSD](https://agilesd.com), where it has been used to ship production Rails applications across telecommunications, healthcare, finance, commerce, agriculture, and logistics. We are extracting the code-generation core into this standalone gem because the pattern itself is generally useful — and because LLMs make it ten times more valuable than when we first built it.

---

## Stay in the loop

- ⭐ Star this repo to be notified of the first release
- Reach out: <josef.sauter@agilesd.com>

---

## License

To be confirmed at first release (likely MIT).
