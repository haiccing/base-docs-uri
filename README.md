# base-docs-uri

How a URI is written in the base family: its names, relative to where it stands, and the data names inside it.

A URI names something in an mrepo, a node, a layer, a document. It is
written relative to where its writer stands, as `/`-separated parts,
each a name; inside it is an array of segments. A URI that selects is a
query, read by XPath. Validated once, at the boundary, into its
canonical form.

## Links

- [test](test/)
- [test-reports](test-reports/)
- [modules](modules/)

## Names

- **A part**: lowercase `a-z`, `0-9`, `-`. Any folder can become a
  branch and the other way round. `_` is reserved: see "Data names".
- **`avro` is reserved as a type's first part**: AVRO's own types,
  `avro/string` and the rest (`base-docs-avro`, "Names"); no
  organisation takes that name.
- **A file's part includes its extension**: a name, then optional
  `.`-separated extensions of the same characters (`request.md`). A leaf
  is an object, its storage format part of its name.
- **Every name is lowercase**, files included; uppercase names are
  external (`README.md`).
- **Case-insensitive coming in**: a URI is validated into its canonical,
  lowercase form; external content keeps its own case. Inside, paths
  match exactly.
- **No scheme, query or fragment**: `/`-separated parts only.
- **A name is never both a branch and a prefix.**

## Relative

- **No leading slash**: a URI is relative to where its writer stands. `.`
  is the position itself, and so is none given; `./x` is `x`.
- **A command's writer stands at `main`**, whoever writes it: `.` is
  `main`, `host` is `main/host`; a flag names another layer
  (`layer=runtime`). The outside reaches `main` and nothing else; the
  mrepo's own requests, a hook's line, are written the same way and are
  allowed any layer: one pattern (the human, 2026-11-26: "use one
  path").
- **No `..`**: a running mrepo sees only forward; outside it is reached
  through a mapping.

## Segments

Inside, in a request's form, a URI is a chain of parts, kept apart so no boundary is
parsed again: the layer first, then the local root positions gone
through, then the URI as written, the last (the
human, 2026-11-26: "it always starts with the mrepo layer to begin with.
That is then follow by URI local root positions, ending in a relative
end URI"): `["main", "host"]`, `["main", "."]`, `["main",
"swarms/swarm-1", "."]`, `["runtime", "hooks"]`. Each part a relative
URI. A request submitted to an mrepo forgets its path outside it:
forward visibility only. Read as one URI, for a query, its parts are
joined. Outside, a URI is one, as it is written.

## Selecting

A part may be `*`, and a part may carry filters, `[...]`: the URI then
selects, and is a query (the XPath documentation). A filter is kept as
written, checked for its brackets and quotes, and for the URI's own
rule: what is no quoted value in it is lowercase, as a name is. A filter
without a name filters the position itself, in front only:
`[state='started']`.

## Data names

The names of properties in records, values and headers, and of anything
that becomes an AVRO name.

- **lowerCamelCase**: `a-z`, `A-Z`, `0-9`, starting with a lowercase
  letter: `publicKey`, `readyMs`.
- **No two capitals in a row**: `dhtUrl`, not `dhtURL`.
- **Practically case-insensitive**: no two names that differ only in
  case.
- **One form in JSON, in memory and in AVRO**: a valid JSON key,
  JavaScript identifier, AVRO name and Kafka header key as it is.
- **In a URI, its URI form**: each capital becomes `-` and the letter in
  lowercase (`publicKey`, `public-key`); back, `-` and a letter become
  the capital. Exact both ways.
- **`_` is reserved**, in data names and URI parts alike: the one
  character left for an encoding, should one be needed.
- **Other mappings later**, at the boundary, for external names that
  break these rules.

## Types

The type system the data names serve, its data shapes, core types and
variants, schemas named by URI, fingerprints and registries:
`base-docs-avro`.
