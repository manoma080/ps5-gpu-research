# Evidence and limits

## Evidence method

Controlled GPU and CTS findings use a bounded native application and a declared
oracle. Owner-reported interaction and sampled gameplay observations are labeled
separately; they do not replace exact numerical checks. The evidence chain records:

- source and dependency revisions;
- deterministic build and artifact identity;
- system software and test configuration;
- exact input dimensions or model profile;
- expected output and comparison method;
- bounded submission and completion;
- application teardown; and
- a claim no broader than the test.

## Confidence labels

| Label | Meaning |
| --- | --- |
| Hardware-proven | Exact frozen workload ran and matched its oracle |
| Controlled | Hardware-proven under deterministic input, not necessarily sustained product use |
| Source-derived | Supported by public/open-source code inspection but not direct console execution |
| Host-checked | Compilation, linking, host tests or archive verification passed; no console execution is implied |
| Owner-observed | Physical behavior reported by the owner; not a substitute for a complete numerical oracle or frame-time trace |
| Inferred | Multiple observations support the conclusion; discriminator remains |
| Pending | Implementation or required evidence is incomplete |

## Current claim matrix

| Claim | Grade | Proven boundary |
| --- | --- | --- |
| Target GPU executes Mesa-compiled graphics shaders | Hardware-proven | Vertex, fragment, and geometry stages with exact pixel oracles |
| Target GPU executes Mesa-compiled compute shaders | Hardware-proven | Buffer writes, reads, reductions, and large dispatches |
| Graphics and compute share compiler/memory/submission concepts | Hardware-proven architecture | Reused compiler backend, resource model, visibility, and completion principles |
| Mesa can derive OpenGL 4.6 Core and GLSL 4.60 | Hardware-proven | Native compatibility/application gate plus implemented Gallium caps and formats |
| OpenGL 4.6 public command surface exists | Static and build-proven | All 657 Core commands link through Make, pkg-config and CMake consumers |
| Major Core 4.6 feature families operate | Hardware-proven slices | Exact public-API and stress tests in the OpenGL validation record |
| Native four-sample storage images operate across programmable stages | Hardware-proven slices | Size, load/store, atomics, arrays, per-sample access and `imageSamples`; advertised maximum is four samples |
| Bounded private arrays use explicit GPU-visible storage | Hardware-proven slices | Scalar/vector widths through 64-bit and arrays through the recorded bounds; final hardware-scratch metadata is zero |
| Historical frozen Core 3.3 project campaign | Controlled | 37,404 Pass plus 2,140 reviewed NotSupported across four configurations; six disclosed CTS adaptations |
| OpenGL 4.6 engineering inventory | Controlled aggregate | 15,233 Pass, 4,480 reviewed NotSupported and one permitted compatibility warning across 19,714 accounted cases; not a certified or conformant implementation |
| Certified or conformant implementation | Not claimed | This is not a certified or conformant implementation |
| Later optimized SDK compatibility | Controlled sample | G7 SDK passes 204 selected executions; later binaries require their own scoped evidence |
| Small-scene graphics throughput | Controlled | 30-second windowed runs at ~119.88 FPS at 1080p–4K; not a general game or perfect-pacing result |
| Native 1440p120 and 4K120 output | Controlled plus console HDMI evidence | September 8 unchanged apps, exact pixels and matching 119.88 Hz negotiation; independent per-run TV refresh observations remain separate |
| SDL fixed high-resolution profiles | Controlled functional checks | 180 frames/two exact pixels per resolution, matching HDMI, normal-output restoration and clean teardown; not measured SDL FPS |
| 128-cube graphics throughput | Controlled | ~59.94 FPS ordinary and instanced at 1080p; small texture working set |
| Offscreen-copy improvement | Controlled plus host-checked | Matched 1080p case 14.10 to 19.98 FPS, with pixels/completion/teardown and scalar-equivalence checks |
| Bounded graphics stability | Controlled plus instrumented normal session | Ten-minute session and five native launch/exit cycles; CPU-owned heap only |
| Yamagi 4K gameplay | Owner-observed | Later optimized development candidate reported at 120 FPS throughout tested areas; bounded scenes and texture-quality limits |
| Yamagi resolution switching | Controlled timing and lifecycle | Six switches across 1080p/1440p/2160p; steady 120-frame windows measured separately from restart time; no new exact pixel oracle |
| Yamagi CI game download | Host-checked plus controlled native startup | All 77 files verified; exact CI executable's 4K menu median 119.880240 FPS over 12 windows; clean close/release; no separate manual CI gameplay run |
| Fresh SDK distribution build | Host-checked | Clean CI compilation, 657 exports, three relocated links and archive checksums; no console qualification |
| Quantized matrix operations match CPU references | Hardware-proven | Exact tested Q4/Q8 layouts and dimensions |
| Complete transformer layers execute on GPU | Hardware-proven | Normalization, attention, projections, activation, residual, and logits |
| Complete autoregressive models execute on GPU | Hardware-proven | Listed 135M through 9B-class profiles |
| Arbitrary GGUF models run without new code | Not claimed | Runtime is architecture/profile specific |
| Video codecs execute on shader compute units | Not claimed | Video decoding is a separate media path |
| General OpenCL/ROCm/CUDA compatibility | Not claimed | Purpose-built native runtime only |
| Equivalence across system software versions | Pending | Primary integrated evidence is one version |

## OpenGL evidence summary

The OpenGL result is supported by:

- a layered Mesa/Gallium architecture;
- normal Mesa version derivation;
- all 657 OpenGL 4.6 Core command symbols in the SDK;
- exact buffer, texture, shader, draw, framebuffer, multisample, query,
  transform-feedback, and synchronization oracles;
- direct presentation with changing frame hashes;
- a completed historical 3.3 campaign and a separately accounted 4.6 engineering inventory;
- later optimized-candidate samples kept separate from that baseline;
- installed-SDK ImGui, NanoVG and Sokol checks;
- preserved functional failures that led to general fixes; and
- clean bounded lifecycle receipts.

The historical 3.3 campaign is complete within its declared scope. Its 39,544
accounted results are not 39,544 passes and do not qualify every later compiler,
runtime or application. This is not a certified or conformant implementation;
in the 4.6 inventory, reviewed `NotSupported` results remain distinct from passes. The remaining work
includes broader workload performance, resource/recovery stress and validation
of subsequent changes.

### Graphics evidence identities

The historical September 8 record summarizes a `ps5-opengl` source snapshot and
a reviewed game-port performance handoff. References below are project and
document identifiers. The counts below are the project's own test results; this is not a certified or conformant implementation.

| Record | Identity and source document | Scope |
| --- | --- | --- |
| Historical full campaign | `ps5-opengl` document `docs/validation.md` | Four complete configurations; 37,404 Pass and 2,140 reviewed NotSupported; 15 CTS cycles |
| Graphics performance progression | G5d, G6 and G7 candidates; `ps5-opengl` document `docs/performance.md` | Separately frozen high-refresh, close-path and 3D candidates; not one combined full-matrix result |
| Optimized sampled SDK | G7 runtime; `ps5-opengl` document `docs/sdk-bundle.md` | 204/204 selected executions and independent consumer checks; preserves its own bytes |
| Offscreen and sustained session | G9 and G10 instrumentation candidates; `ps5-opengl` document `docs/offscreen-stability.md` | Matched offscreen comparison, 600-second session, five launches/15 EGL sessions |
| Initial game-derived findings | Reviewed game-port performance handoff; game-specific G7 derivative | Allocation policy, scoped texture maintenance and bounded 1080p gameplay observations; not merged SDK acceptance |
| CI-built SDK | `ps5-opengl` document `docs/ci-releases.md` | Build/link/package verification only; these binaries were not run on the console |

Later display follow-up: `ps5-opengl` records G37–G40
in `docs/high-resolution-120-plan.md`. Subsequent documentation commits
are not rebuilds. The same 4K executable's HDMI1/HDMI4
comparison establishes a connection-path limitation for that setup; the native
1440p result follows a separately owner-selected resolution. It does not qualify
every TV input, cable, capture device, new SDK build or HDMI configuration.

The owner confirmed 4K120 for a preceding stream on HDMI4 and 1440p resolution
before its OpenGL test. Neither statement is recorded as independent TV refresh
verification of every later OpenGL/SDL run. The four bounded applications have
their own console negotiation, pixels, restoration and teardown evidence;
none inherits the historical full CTS campaign or changes the compute results.

The original CTS revision is `cf7edb26d3be2d8763595ed08fdc41f3c1b1966f`.
Six disclosed changes cover platform build/package routing, portable I/O and a
negative compute-shader version guard. The exhaustive swizzle and LOD-bias workloads remain unchanged. Do
not describe this runner as untouched upstream CTS or imply formal certification.

The game case and all graphics hardware records above are scoped to the recorded
console and system software version. Reusing a concept across graphics and compute does not
transfer either project's correctness or performance acceptance to the other.

### Yamagi 120 Hz follow-up scope

The September 11–12 follow-up separates the automated development run from the
exact CI-download startup check. The CI run
built the game using the frozen prebuilt SDK; it was not a
separate runtime-library rebuild. The downloaded game's native startup test
therefore qualifies those exact game bytes for that bounded scenario. It does
not transfer the development candidate's manual gameplay observations to the
CI executable, or qualify a rebuilt library merely because its source matches.

The [benchmark record](benchmarks.md#public-120-hz-follow-up) reports each
observation's workload and timing boundary. Six successful resolution changes
do not establish recovery under device loss, memory exhaustion or suspend/resume.
The current game SDK has focused checks and bounded evidence on one
console; it does not inherit the historical full CTS campaign. The proposed
benchmark matrix remains pending and adds no completed hardware cases.

## Compute evidence summary

The compute result is supported by:

- distinct GPU-written storage-buffer values;
- exact large-buffer fill validation;
- exact CPU-populated operand readback;
- FP32 dot and matrix results;
- quantized large projections matching every CPU row;
- one real model tensor and one full decoder layer matching independent
  references;
- full-model greedy token IDs matching llama.cpp;
- bounded context and KV-cache tests;
- coherent native application responses; and
- model switching with explicit residency management.

Failed intermediate artifacts are not reused as positive evidence. Incorrect
output, timeout, GPU fault, process failure, soft lock, and kernel panic remain
separate classifications.

## System software scope

The integrated OpenGL Core candidate and AI runtime are primarily validated on
one system software version. This repository does not infer feature or
performance parity on any other version.

Interfaces and behavior can change between versions. Every future claim should
state its tested configuration and reuse identical frozen bytes when comparing versions.

## Reproducibility boundary

This high-level repository is not the implementation repository.

No result should be reconstructed from prose alone and called an independent
reproduction.

### Source builds versus hardware-qualified binaries

The September 8 CI run independently built the graphics SDK from the pinned public
dependencies on a clean GitHub-hosted runner. Host regressions, compiler checks,
all 344 Core exports, relocated Make/pkg-config/CMake consumer links and archive
checksums passed. The distribution includes sources, licenses and provenance.
This establishes a working source-to-SDK build path, not GPU execution, identical
bytes across toolchain updates or reproduction of an older console campaign.

Keep three identities distinct: source snapshot, compiled artifact and hardware
receipt. A newly compiled SDK does not inherit older acceptance because its source
is related. Likewise, the five-minute historical baseline, later high-refresh
microbenchmarks and ten-minute normal session are not one unchanged executable.

The fresh CI archive differs from the sampled hardware-tested SDK and is explicitly host-checked,
not console-validated.

## Pending work

1. Validate changed graphics paths with affected exact-oracle tests and frozen
   candidate identities; retain the historical complete matrix as a separate record.
2. Reduce offscreen layout-copy costs and test heavier scenes without assuming
   that windowed presentation throughput transfers to sampleable targets.
3. Review reusable game-runtime changes in PS5 OpenGL with affected correctness
   tests and the [proposed game-derived benchmark matrix](benchmarks.md#proposed-game-derived-benchmark-matrix).
   Compare individual changes before combined acceptance; extend normal sessions,
   GPU-memory accounting and recovery testing separately.
4. Expand compute correctness to additional model architectures without
   weakening exact reference checks.
5. Add multi-process or concurrent-queue tests only with an explicit safety
   and lifecycle design.
6. Repeat the final integrated workloads on additional system software versions using the same
   frozen artifacts.
7. Publish generative-audio findings only after complete, model-valid output
   and playback acceptance.

## Full-slice depth and stencil copies

September 25 follow-up. **Grade: controlled on the console, with host-checked
layout and rejection cases.** The native workload copies full matching
1920x1080 depth/stencil slices, then uses the results in subsequent rendering.
The depth and stencil checks each matched 4,096 expected pixels, with successful
cleanup. This is a correctness result, not a throughput benchmark.

Bulk plane copies are admitted only for the qualified matching layout: full
positive extents, matching dimensions and plane spans, compatible storage,
matching layer index, and no effective clipping or staging conversion. Other
cases retain the existing path. Equal dimensions alone do not establish that
two tiled slices are byte-compatible.

The host oracle checks complete buffers
and guards with independent layout expectations; removing the layer restriction
is caught by its mutation check. The native oracle checks the
copy indirectly through rendered output. Both are in the
[PS5 OpenGL](https://github.com/blackbearreloaded/ps5-opengl) repository. An application follow-up showed no
measured benefit in a scene using small/scaled copies rather than this full-slice
path. Neither arbitrary cross-layer copying nor a general FPS gain is claimed.

## Large CPU heap qualification

September 25 follow-up. **Grade: controlled on the console.** The native
allocator oracle used a 2 GiB memory region with CPU read/write
access. It verified mixed-size allocation patterns totaling 1,102 MiB, freed
them in mixed order, then allocated and verified a coalesced 1.5 GiB block.
Separate serial and eight-worker stress phases checked allocation contents and
cleanup. The heap oracle is in the [PS5 OpenGL](https://github.com/blackbearreloaded/ps5-opengl) repository.

The backing-region allocation and the heap allocator inside it are distinct
layers. These CPU heap checks do not establish GPU access, GPU cache coherence,
shader address compatibility, or performance for that region. A failed large
mapping attempt before heap creation was not evidence of heap corruption.

Worker stress used independently owned allocations; it does not establish all
cross-thread free patterns. Passing the oracle also does not explain or dismiss
unresolved application heap corruption. This is a bounded allocator result,
not a new allocator, a maximum-memory measurement, or a recommendation that
consumers reserve 2 GiB.
