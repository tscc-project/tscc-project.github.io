# tscc website handover

## Repository and source authority

This repository uses the same deliberate two-branch Nift publishing model as the
Nift website. The `stage` branch owns canonical source: `content/`, `templates/`,
`.nift/`, documentation, and this handover. The `main` branch owns only the built
website at repository root. On `stage`, `public/` is an embedded checkout of this
repository's `main` branch and is recorded as a Git link. It is intentionally not
a conventional submodule and there is no `.gitmodules` file.

This handover belongs at the root of `stage`. Do not add it to the generated
`main` branch unless publication policy explicitly changes.

Edit source on `stage` and rebuild with Nift. Do not hand-edit generated HTML as
canonical content, and never run the source build from the outer repository while
it is on `main`. Local builds/inspection are normal; commits, pushes, public
deployment, release/version claims, and publication require explicit approval.

For a normal publication checkpoint:

1. Check out `stage` in the outer repository and `main` in `public/`.
2. Edit only canonical source and documentation outside `public/`.
3. Run the intended Nift binary from the outer `stage` checkout.
4. Inspect and test the generated changes under `public/`.
5. Commit canonical source changes on `stage`.
6. Commit generated website changes inside `public/` on `main`.
7. Stage and commit the updated `public` Git-link pointer on `stage`.
8. Push both branches only when publication is authorized.

The source commit may precede the generated commit during local work, but a
published `stage` checkpoint must ultimately point at the matching published
`main` commit. Keep the two histories intelligible and do not mix source files
back into the deployment branch.

## Truthfulness burden

This site must explain the compiler that actually exists, not the compiler the
project may eventually become. “TypeScript compiler” can imply drop-in `tsc`
compatibility. Current product wording is experimental TypeScript-to-JavaScript
compiler; tscc 0.15.0 has substantial parsing/transforms/project/module support but
a bounded semantic overlay, binder, durable primitive type store and expression/
assignment checker rather than a general TypeScript type system.

Every capability claim should map to appropriate evidence—not parser acceptance
alone. Where useful distinguish supported, partial, experimental, planned, and
unsupported behavior, but only create a support matrix if checkpoint workflow can
keep it current.

## Current evidence and claims

The site currently advertises 553 independent cases (529 pass, zero fail, 24
semantic skips) and dated five-run local medians for startup, 100/500 basic files,
and 100-file feature-heavy/advanced fixtures. The August 2026 snapshot uses
TypeScript 7.0.2 and must be treated as checkpoint evidence rather than a stable
cross-machine speed claim.

Benchmark comparisons must separate `tscc`, `tsc --noCheck`, and full `tsc` and
state corpus, versions, configuration, machine, runs, cold/warm behavior, and
compiler scope. A no-check transpiler comparison is not a universal equivalent-work
claim while tscc lacks comprehensive semantic checking.

## Tested examples

Prefer website examples that are regression fixtures or are easily validated by
the current candidate:

```text
example.ts/tsx
→ candidate tscc
→ emitted JS/JSX
→ Node or downstream syntax validation
```

Do not advertise a feature merely because a parser branch exists. Runtime-bearing
features should have runtime evidence; malformed forms should fail controllably;
scope/evaluation-sensitive transforms need appropriate tests.

## Development workflow

After a validated compiler checkpoint:

1. Determine whether language, CLI/config, module/project, maturity, limitation,
   benchmark, or architecture claims changed.
2. Search all source content for affected claims/counts/examples/versions.
3. Verify important examples with the exact candidate tscc and reference tools.
4. Update support/limitations after implementation evidence is settled.
5. Build the website with the intended Nift binary.
6. Inspect generated diff, links/assets, responsive/accessibility behavior, and
   version/download references.
7. Review this handover and living website/product roadmap.

Internal refactors with no observable effect normally need no public copy change.

The coordinated compiler campaign is now public development context. Keep the
site synchronized with accepted checkpoint state without presenting planned
JS++ integration as a current runtime dependency. CP1 settles test-only
integration first and protects normal tscc builds from accidental JS++ linkage.

CP2 adds a machine-checked feature matrix in the compiler repository. Public
support summaries must remain consistent with its eight dimensions and named
external evidence rather than collapsing parser acceptance into support.

CP3/TC1 adds durable per-file compiler ownership through emission. The public
architecture and roadmap pages describe this as an internal foundation, not a
new TypeScript compatibility claim. Keep that distinction intact.

CP19/TC8A likewise adds canonical object-shape infrastructure without changing
the source-language support boundary; CP20 owns bounded structural checking.

CP20 now supports only the documented flat structural slice. Keep the 501/0/24
count and the nested/indexed/freshness/class limitations visible.

## Product boundaries

tscc is a sibling of Nift and Minify++, not “Nift's compiler.” Do not force common
branding or imply architectural dependency. Preserve the current site design
unless redesign is requested.

## Living production-support roadmap

First establish the compiler's intended production compatibility target and
evidence-backed feature inventory. Then audit every site capability, example,
CLI/config statement, limitation, architecture description, benchmark, maturity
claim, and download/version reference. Production-candidate validation should
compile/run key examples and map every major support claim to the regression suite.

This roadmap and handover are living infrastructure. Reassess them at every
substantial compiler or website checkpoint; add, remove, reorder, or rewrite work
as evidence changes. Do not let a support matrix rot or preserve planned behavior
as though it were current.

Detailed tscc website history lives at
`docs/handover/PROJECT-HISTORY.md`, including compatibility wording,
support evidence, benchmark integrity, production-support gates, and the living
roadmap.

## Documentation URL layout

The homepage remains `/index.html` and the documentation landing page remains
`/docs.html`, matching nift.dev. All secondary documentation/evidence/design pages
live under `/docs/*.html`, even when a page does not use a docs-specific template.
Keep tracked names, `@pathto(...)` references, authored content paths, and generated
output aligned with this rule when adding or renaming pages.

## Desktop table-fit checkpoint (2026-08-18)

The benchmark table now uses a fixed, wrapping desktop layout so it remains inside normal viewport widths. Keep benchmark columns wrap-safe; horizontal overflow should not be required on ordinary desktop widths.

## Memory-safety living record checkpoint (2026-08-18)

- `docs/memory-safety` is the dedicated living compiler lifetime/leak record beside Battle Tested. Establish the baseline before the semantic checker and retained compiler graphs become substantially larger.
- The page currently describes planned work only. Future results must record the exact compiler commit/toolchain/workload and distinguish confirmed leaks from allocator/runtime high-water behavior.

## tscc memory-safety Checkpoint 5A (2026-08-18)

- Public memory documentation now records the first compiler-lifetime baseline: 80 sanitizer-backed in-process iterations, settled native RSS across repeated lifetime runs, and repeated 120-file project/module graph success/failure/recovery pressure at tscc commit `a05d3d8`.
- Checkpoint 5B remains independent Valgrind confirmation. Do not describe Checkpoint 5 as complete until that evidence is returned and reconciled.

## tscc memory-safety Checkpoint 5 complete (2026-08-18)

- External Checkpoint 5B passed at tscc commit `d96419e`: Valgrind 3.26.0 completed 40 maintained compiler-lifetime iterations with 0 errors, 0 bytes in use at exit, and all 25,003 allocations freed.
- Public Memory & Resource Safety and Battle Tested pages now describe the compiler-lifetime baseline as complete while keeping the claim scoped to the maintained workloads, not TypeScript completeness.
- Exact Valgrind evidence is retained in the tscc source tree. The wider campaign proceeds to cross-project integration.
## CP22 / TC8C (2026-08-30)

Public object support now includes nested shapes, chained reads and path-specific
diagnostics. Extra source properties are intentionally structurally compatible.
## CP24 expression identity (2026-08-30)

The checker now consumes CompilationUnit-owned expression nodes. Describe this
as architecture, not broader TypeScript expression compatibility.

## CP26 structured expressions (2026-08-30)

The durable expression model now owns explicit node kinds, operators and child
identity for the bounded grammar. The independent 505/0/24 contract is unchanged.

## CP28 reusable object declarations (2026-08-30)

Public object support now includes basic aliases/interfaces and compatible
interface merging. The 533-case contract is 509/0/24; keep indexed/call
signatures, inheritance, generics and classes explicitly unsupported.

## CP30 expression typing (2026-08-30)

The checker now consumes structured expression children directly rather than a
retained token-sequence compatibility view. This changes architecture only; the
533-case contract remains 509/0/24.

## CP31 callable type model (2026-08-30)

Callable aliases, annotated variables and function declarations now share
canonical signature identities. This is type-model infrastructure; do not claim
callable variables or contextual typing before CP32 evidence.

## CP32 callable expressions (2026-08-30)

Public counts are now 515/0/24 across 539 cases. Callable variables and bounded
contextual arrow/function expressions are supported in checked initializer
contexts. Do not imply overloads, generics, full inference or universal
expression-statement checking.

## CP33 whole-program calls (2026-08-30)

Callable argument and arity checks now apply outside initializer contexts,
including standalone, branch and throw uses. Public evidence is 519/0/24 across
543 cases; do not generalize this to complete statement operator checking.

## CP34 callable inference (2026-08-30)

Typed arrow and function expressions can now infer callable variable identities;
contextual optional/default/rest forms are supported. Public evidence is
525/0/24 across 549 cases. Inline callback arrows, overloads and generics remain
unsupported and must not be implied by the callable wording.

## CP35 nested contextual callbacks (2026-08-29)

Public evidence is 529/0/24 across 553 cases. Direct inline arrow and function
callbacks passed as call arguments receive contextual parameter and result types.
Keep the wording bounded to call arguments; do not claim universal recursive
expression ownership, overloads or generics.

## CP36 callable object members (2026-08-29)

Public evidence is 535/0/24 across 559 cases. Object method signatures,
function-valued properties and bounded interface inheritance share the canonical
callable/object model. Do not imply index/call signatures, generics or classes.

## CP37 nested expression ownership (2026-08-29)

Public evidence is 539/0/24 across 563 cases. Contextual callbacks are supported
through direct parentheses and structural object-property values. Do not claim
that every statement form yet owns durable expression children.

## CP38 index and callable object signatures (2026-08-29)

Public evidence is 545/0/24 across 569 cases. Bounded string/number index
signatures and single callable object signatures share canonical structural and
function types. Do not imply computed access, overload sets, mapped or generics.

## CP39 annotation parser decomposition (2026-08-30)

The annotation grammar now has a dedicated parser boundary with decomposed
productions. Public support remains 545/0/24 across 569 cases; this is an
architecture checkpoint and must not be presented as new language coverage.

## CP40 computed element access (2026-08-30)

Public evidence is 549/0/24 across 573 cases. The site may claim exact string
property and bounded string/number index-signature reads. Do not imply arrays,
tuples, symbols or indexed-write checking.

## CP41 durable statement expressions (2026-08-30)

Callable statement roots now have semantic-model ownership and the checker no
longer scans references to rediscover them. Public evidence remains 549/0/24
across 573 cases; do not imply a complete statement AST yet.

## CP42 canonical arrays and tuples (2026-08-30)

Public evidence is 555/0/24 across 579 cases. The site may claim bounded `T[]`
and fixed tuple annotations, contextual literals, numeric reads and length.
Readonly/optional/rest tuples, methods and indexed writes remain out of scope.

## Compiler preview contract gate (2026-08-30)

Roadmap and production-readiness pages now publish TCP0-TCP5 and the frozen
positive/negative project as the bounded preview finish line. Keep this wording
synchronized with `tscc/docs/COMPILER-PREVIEW.md`; it is not a drop-in `tsc`
compatibility claim.

TCP0 is public: machine-readable checked-versus-emitted classification, frozen
positive/negative projects and an explicit dependency-free production boundary.

TCP1 may be claimed as stable TSCC code families, deterministic ordering, pinned
non-pretty output and explicit CLI contract failures.

TCP2 may claim enforced ES2022/module/JSX boundaries, sorted project roots,
byte-identical repeated builds, visible unknown-option failure and both documented
emit policies. Multi-file rename is still not a filesystem transaction.

Post-TCP2 order is TCP3 semantic closure led by cross-module types, TCP4's
module-free JS++ intersection, then TCP5 evidence. Do not imply JS++ module
loading or promote unrelated broad language families.

TCP5 may claim a bounded Linux compiler preview candidate at 555/0/24 and 7/7
runtime intersection, with frozen/representative projects, ASan/UBSan, 400
mutations, a loose startup guardrail and reproducible archives. It must not claim
drop-in `tsc` compatibility; leak checking remains external under ptrace.

TCP3 is complete. The roadmap records relative named-import propagation of
cloned callable and structural types, including the unit-local type identity
boundary and frozen cross-module negative evidence.

TCP4 is complete at 7/7 independent intersection cases. The frozen source uses
typed objects, tuples and an ordinary function without modules; production TSCC
emit returns 42 under Node and JS++. Do not imply JS++ module support.

The next work is evidence-first. PC0V Valgrind confirmation will happen later on
Nick's machine; PC0P tracks platform packages; TCP6A introduces classified real-
project trials; EP6A belongs to JS++ conformance. Do not publish those as passed
until their evidence exists, and do not broaden website compatibility claims in
anticipation of them.

## Website preview refresh (2026-08-30)

The public site now consistently presents the TCP0-TCP5 bounded Linux compiler
preview candidate at 555/0/24 across 579 independent cases plus the 7/7 explicit-
expectation Node/JS++ runtime intersection. New maintained pages cover compiler
examples, diagnostic behavior and the exact preview contract.

Keep example prose precise about checked versus emitted-only behavior. In
particular, runtime transforms do not imply class/namespace semantic checking,
the JS++ intersection does not imply module support or a production dependency,
and preview qualification does not imply drop-in tsc compatibility. PC0V, PC0P
and TCP6A remain future evidence gates.

## AI assessment and development-process refresh (2026-08-30)

`docs/ai-opinion` now reassesses TSCC after TCP5 rather than preserving the old
primitive-checker view. Semantic checking is rated 4.3 (up from 1.4), while the
drop-in `tsc` score is 3.5 (down from 5.6) because package resolution, declaration
libraries, broader configuration and semantic completeness dominate arbitrary
project adoption. A separate 6.5 CI/release-readiness score keeps evidence
automation distinct from regression design.

`docs/ai-development` now treats multi-repository topology as part of the
evidence contract. The 2026-08-30 GitHub run checked out only TSCC while `make
test` expected `../tscc-regression-suite`, so Linux/macOS failed before compiler
testing and Windows `test-core` passed. Describe this as an evidence-orchestration
defect, not a compiler regression. Remove or update the dated incident discussion
after CI explicitly provisions a pinned suite and a clean rerun passes; do not
leave a resolved red-run assessment frozen forever.

The website now records compiler commit `bd7313c` as the concrete pinned repair
and labels its GitHub verification pending. Keep the CI/release score at 6.5
until the pushed Linux/macOS/Windows run is green, then replace the dated incident
state with the successful run evidence rather than deleting the reproducibility
lesson.

## CP75 compiler-state reconciliation (2026-09-14)

Website source has been reconciled with the compiler pause baseline at TSCC
`e4c45dc`. In particular, `content/docs/ai-opinion.html` no longer describes
generics, overloads, classes, package/declaration/config foundations, source maps
or incremental output as absent, and it records CP73 Valgrind closure plus the
CP75 pause recommendation. Roadmap/readiness/support/memory/battle-tested and AI
development pages carry current-status callouts. The frozen 579-case 555/0/24
preview contract remains historical evidence, not a TypeScript completeness
percentage.
