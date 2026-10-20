# Video workflow results and decisions

## Video 0: course introduction

### Current production status

- Source: `video0.tex`
- Beamer frames: 8
- Overlay-aware pages: 27
- Reviewed narration: `scripts/video0.md`
- Production backend: remote Qwen3-TTS on Duke DCC CUDA
- Model: `Qwen/Qwen3-TTS-12Hz-1.7B-Base`
- Voice: Coben hp3 reference, x-vector cloning
- Service identity: `qwen3-tts-1.7b-base-coben-hp3-xvector-v1`
- Canonical output: `build/video0/video0_qwen3-clone-coben.mp4` (the filename
  describes the cloned voice; its production audio profile is remote)
- Canonical audio metadata: `build/video0/audio/qwen3-remote-coben/metadata.json`

The production video has 32 speech chunks across 27 pages, 547.04 seconds of
speech, and 585.89 seconds of timed PCM narration. The current H.264/AAC MP4 is
585.90 seconds at 30 fps and approximately 10.57 MiB.

`make video`, `make video-qwen`, `make qwen-video`, and `make video-qwen-remote` all produce the canonical file from remote audio. Local generation is isolated behind `make video-qwen-local` and writes a device-labeled debug output instead.

### Remote automation status

- Speech-cache preflight: implemented. A fully cached build does not start DCC or open a tunnel.
- Incremental generation: implemented at speech-chunk granularity.
- Automatic service lifecycle: implemented, including deployment, Slurm submission, readiness wait, authenticated tunnel, token retrieval, and cleanup.
- Failure reporting: implemented in local audio/DCC logs with Python tracebacks, scheduler state, the remote service tail, and server-side request timing.
- Storage: environment and caches under `/work/hp83/dcc-ai/`; durable model and voice assets under `/hpc/group/pfisterlab/hp83/dcc-ai/`.
- Default allocation: one scavenger RTX 5000 Ada, 4 CPUs, 32 GB, and a 2-hour limit. H200 resources are not needed.

### Remote versus local Qwen findings

The local and remote paths use the same 1.7B Qwen model, Qwen-TTS `0.1.1`, and Transformers `4.57.3`. They differ in execution stack:

- Local: PyTorch `2.12.1`, float32, MPS or CPU.
- DCC: PyTorch `2.13.0+cu130`, BF16, CUDA 13, SDPA.

The page-21 artifact was present in a local/MPS speech WAV and absent from the remote/CUDA WAV. Repeating the same local MPS request with the same model, text, prompt, and seed did not reproduce the same file: the original was 9.04 seconds and the rerun was 8.24 seconds with a different hash and opening envelope. A local CPU control had a clean opening like CUDA. This points to MPS numerical or sampling nondeterminism rather than a weaker model.

Decision: remote CUDA is the production backend. Local caches include the device name and cannot be reused by remote builds. MPS remains available only for debugging.

### Rendering and audio-concatenation correction

The earlier renderer created an AAC-bearing MP4 segment for every page. Two effects accumulated at boundaries:

1. Rounding every page independently to 30 fps shortened the timeline by about 210 ms by page 21.
2. Per-segment AAC encoder delay moved that page's valid audio roughly another 107 ms earlier.

The old canonical example therefore placed the beginning of page 21 about 317 ms ahead of its intended PCM position. The audio itself correlated with the source clip; the assembly pipeline had moved it.

The current renderer instead:

- allocates video frames from cumulative narration time, keeping every boundary within half a frame rather than accumulating error;
- creates video-only page segments;
- concatenates all timed page WAV data losslessly into `video-work/PROFILE/narration.wav`; and
- AAC-encodes that continuous PCM track exactly once during final muxing.

The corrected local test placed the page-21 prefix at 419.290 seconds, exactly
matching its PCM timeline. The pre-hp2 canonical remote video placed the
corresponding remote page-21 prefix at 421.120 seconds with correlation
`0.99989` to the remote source WAV.

### Performance measurements

A three-prompt benchmark used the same 1.7B model, reference, seed, and text:

| Metric | Local MPS | Warm DCC RTX 5000 Ada |
|---|---:|---:|
| Model/backend initialization | 10.13 s | already warm |
| Synthesis time | 65.10 s | 21.70 s |
| Generated speech | 18.16 s | 19.04 s |
| Weighted real-time factor | 3.59 | 1.14 |
| Generator end-to-end time | 76.38 s | 22.58 s |

Warm DCC inference was about three times faster. The measured cold service startup was about 79 seconds, including a 4-second Slurm wait, so local execution can still be faster for only a few short experimental clips. The DCC service wins when startup is amortized across a lecture or several jobs.

An incremental production run reused 28 chunks and synthesized four changed chunks. A separate fully cached Make test reused all test clips in 0.40 seconds without contacting DCC.

### Pronunciation and timing state

- Shared lexicon entries include `Pfister`, `ECE 586`, `ECE`, `AI`, `Qwen`, `PAF`, `EF`, `Socrates`, `ex falso quodlibet`, `Euclid`, `Cantor`, `Cauchy`, `orthogonal`, three verb-specific `graduates` phrases, and `NC`. `Orthogonality` is deliberately left in its standard spelling for Qwen.
- The default seed is `42`; the reviewed script uses page overrides including 43, 44, 45, and 47.
- Current timed narration contains 7.8 seconds of page lead, 27.6 seconds of page tail, and 3.45 seconds of explicit internal pauses.
- Timing-only changes rebuild timed WAVs and affected video state without regenerating speech.
- The voice reference is `coben_hold_tight_ch1_first29_hp3.wav`, a 29.49-second,
  mono, 16-bit, 44.1-kHz PCM recording. No exact transcript is available, so
  x-vector mode remains the production default.

### Content review carried forward

The slide and note review identified these authorial issues for future revision:

1. Correct and properly scale the matrix perturbation bound in Example Problem 1.
2. Distinguish metric-space distance from the more general notion of topology.
3. Add differentiability, or use subgradients, in the tangent-line bound for a convex function.
4. Make mathematical maturity an explicit learning goal and simplify the dense major-topics slide.
5. Replace several dated or informal phrases and fix the noted grammar and typography.

All 27 slide states were previously rendered and visually inspected. No clipped audience-facing content was found. Example Problem 2 reports a small vertical overflow, but its rendered content remains visible.

### Current operational decision

Use the remote-backed canonical video for production. Preserve backend-specific caches for correctness and debugging, but do not use local/MPS output as the canonical file. Revisit local generation only if PyTorch/Qwen adds a demonstrably stable MPS path or a targeted reproducibility fix is found.

## Videos 1--4: first production batch

### Completed outputs

All four videos were initially built on 2026-08-01 with remote Qwen3-TTS, the
Coben x-vector voice, and default seed 42. Video 3 was refreshed on 2026-08-06
and Video 1 was regenerated with the hp2 Coben reference on 2026-08-22; the
table reports the current outputs.

| Video | Frames | Overlay pages / clips | Speech | Timed narration | Canonical MP4 | Size |
|---|---:|---:|---:|---:|---:|---:|
| 1: Propositional Logic | 8 | 28 pages / 33 clips | 452.96 s | 487.66 s | 487.67 s | 8.51 MB |
| 2: Predicate Logic | 8 | 29 pages / 30 cues | 675.44 s | 710.29 s | 710.30 s | 12.98 MB |
| 3: Set Theory | 10 | 39 pages / 52 clips | 635.92 s | 686.22 s | 686.23 s | 13.16 MB |
| 4: Relations and Functions | 9 | 29 pages / 39 clips | 497.84 s | 538.04 s | 538.07 s | 10.79 MB |

The canonical files are:

- `build/video1/video1_qwen3-clone-coben.mp4`
- `build/video2/video2_qwen3-clone-coben.mp4`
- `build/video3/video3_qwen3-clone-coben.mp4`
- `build/video4/video4_qwen3-clone-coben.mp4`

### Script and overlay decisions

The reviewed scripts are `scripts/video1.md` through `scripts/video4.md`. Every
rendered overlay page has one narration beat. In video 2, each legacy `Read.`
command is expanded by first speaking the matched newly revealed slide text
and then retaining the additional explanation following `Read.` in the note.

The rendered PDFs are the authority for visual states, and the embedded
speaker notes are the sole authority for narration. The extractor now detects
internal overlays even when a frame has no explicit frame-level overlay range,
so it reports the validated counts of 28, 29, 39, and 29 pages. The production
scripts match those PDFs exactly.

Videos 3 and 4 were retranscribed after the video 2 correction. No mathematical
corrections or explanatory transitions were inserted into the spoken scripts.
A blanket `Read.` applies separately to each reveal, and a reveal with no note
cue falls back only to its displayed text. Existing mathematical or grammatical
concerns remain source-only `\gpt` comments for the author to resolve. Video 4
still contains the literal incomplete note text `Here...` on pages 20 and 23;
that phrase is preserved in the audio and flagged in `video4.tex` rather than
being completed speculatively. Its four-overlay “Applying Functions to Sets
(2)” frame has three cues, so page 25 reads only its fourth reveal.

### Pronunciation and timing

The shared lexicon was expanded for these lectures with `PAF`, `EF`,
`Socrates`, `ex falso quodlibet`, `Euclid`, `Cantor`, and `Cauchy`. The readable
spellings remain in Markdown; the phonetic substitutions appear only in the
Qwen request text. All 127 current clips in this batch use seed 42, and no per-page
reseeds have yet been selected.

Video 1 and video 2 each use a two-second slide-tail override after a reflection
question. All other transitions use the shared timing configuration: 0.2-second
overlay lead, 0.5-second new-slide lead, 0.65-second overlay tail, 1.4-second
slide tail, and 1.25-second final tail.

### Automated QA

- Production PDF pages and Markdown beats agree exactly for all four videos.
- No unexpanded `Read.` commands remain. Video 4 intentionally retains the two
  incomplete authored `Here...` cues described above.
- Every timed page WAV is mono, 16-bit, 24 kHz, with exact digital silence in
  its configured lead and tail regions.
- The final files are H.264 at 908 by 510 and 30 fps, with mono 24-kHz AAC.
- MP4 durations agree with cumulative PCM narration to within one video frame.
- Remote logs contain no failed requests, HTTP errors, or tracebacks.
- A cache-only verification after the video 2 narration correction reused all
  30 current video 2 speech chunks and all 29 timed page WAVs, skipped the DCC
  allocation entirely, and left its MP4 unchanged.
- After the latest builds, final AAC peak levels are -0.4 dBFS for video 3 and
  -0.2 dBFS for video 4. Their mean levels are -16.0 and -16.2 dBFS,
  respectively.

The automated checks establish synchronization and file integrity, but an
author listening pass remains the acceptance test for pronunciation, emphasis,
and occasional Qwen voice variation. A problematic page can be regenerated by
adding `[[seed N]]` immediately after its `Narration:` marker and rerunning the
normal video target; all unaffected speech remains cached.

## Institution and pronunciation update

The slide tree now has a shared `institution.tex` with `\univ`, `\mascot`, and
`\city`. All 49 existing author blocks use `\univ`; the university examples in
video 1 and the chapter-1 deck use `\univ` and `\city`. Narration for videos 0
and 1 uses `{{univ}}` and `{{city}}`, which the beat parser expands from the
same TeX file. Representative builds of video 5, `slides_ch1.tex`, and
`faq3.tex` confirmed that both direct and `macros.tex`-based inclusion paths
compile.

The Qwen pronunciation layer sends `or-THOG-uh-nul` for “orthogonal” and
leaves “orthogonality” in its standard spelling. Phrase-specific entries send the
verb in “graduates this term,” “graduates and passes,” and “graduates nor passes” as
`GRAD-joo-ates`, without changing noun or adjective uses of “graduate.” Video 0
was rebuilt with seven current-script chunks synthesized and 25 reused. Video
1 was brought fully current, then three narration typos found during generation
were corrected and regenerated. Its final cache contains all 29 current chunks,
and the remote service was stopped after completion.

## Video 2 source-owned speaker-note correction

`scripts/video2.md` was retranscribed from the embedded `\note{...}` blocks,
including the title-page note. `Read.` now expands only to the exact matched
reveal; every word before or after it comes directly from the note, in source
order. No explanatory prose or transitions were added. Source wording was
preserved even where an existing `\gpt` comment identifies a typo or
mathematical issue for later author editing.

The “Multiple Quantifiers” frame contains six authored note cues but only five
rendered visual overlays. Both source cues are retained as two speech chunks on
the final visual state, separated by 0.5 seconds. The diagnostic note extractor
now detects this mismatch, preserves the title note, distinguishes `\item`
from `\itemsep`, and labels all `Read` replacements as exact rather than
inviting natural-language rewriting.

The `Socrates` lexicon entry sends `SOCK-rah-teez` to Qwen. The latest
source-faithful remote rebuild has 29 pages and 30 authored speech cues, 711.60
seconds of speech, 746.45 seconds of timed narration, a 746.47-second video,
and a size of 15.57 MB. A final pass reused all 30 speech chunks without
requesting DCC.

## Videos 0--2 recompilation after availability-aware scheduling

On 2026-08-02, videos 0--2 were rebuilt sequentially. Video 0 reused all 32
speech chunks without requesting a GPU or rewriting an already-current MP4.
The live Slurm selector chose an RTX
5000 Ada in `gpu-common` for the remaining work; video 1 synthesized four
changed chunks and reused 25, while video 2 synthesized 18 changed chunks and
reused 12. A final cache preflight found zero missing chunks for all three
videos. PDF pages, metadata pages, and MP4 timing agree, and the service job was
cancelled after the batch.

## Video 0 provenance and splice audit

The cached result used during the 2026-08-02 batch was audited after the build
to determine whether it predated the remote-generation and audio-splicing
corrections. It did not, so no additional regeneration was needed.

- All 32 current speech chunks across 27 pages are referenced by metadata whose
  backend is `qwen3-remote-v1` and whose service identity is
  `qwen3-tts-1.7b-base-coben-xvector-v1`.
- The canonical `video0_qwen3-clone-coben.mp4` was assembled after the current
  remote metadata and continuous narration WAV. The `clone` output tag denotes
  the voice-cloning mode; it does not indicate local generation.
- Concatenating the PCM payloads of the 27 timed page WAVs reproduces
  `video-work/qwen3-remote-coben/narration.wav` byte for byte. Both have PCM
  SHA-256 `2cf16903c5a530e9804976f8ab26680199117a7439b8c4d9b08199e2c12f1b87`.
- The continuous WAV is 587.25 seconds. The canonical 30-fps MP4 is 587.2667
  seconds, and its decoded AAC track correlates with the complete narration WAV
  at `0.9998919` with zero measured sample offset. This is the expected result
  of one final AAC encode, not per-page AAC splicing.

The audit therefore confirms both corrected components requested for video 0:
remote CUDA speech generation and lossless full-WAV assembly before the single
final AAC encode.

## Speaker-note transcription rules

The source-faithful corrections made while preparing videos 2--4 are now
captured normatively in `SCRIPT_TRANSCRIPTION.md` and summarized in
`VIDEO_WORKFLOW.md`. In particular, a note item containing `Read.` directs the
producer to read the corresponding main reveal exactly and then speak all
additional note text unchanged. It is not a prompt to paraphrase the slide or
invent narration. The specification also covers the title note, numbered and
parenthetical read directions, persistent versus newly revealed material,
cue/overlay count mismatches, incomplete notes, faithful spoken mathematics,
and the narrow role of production-only pause, pronunciation, and seed markers.

## Video 3 script refresh

Video 3 was refreshed again on 2026-08-07 after an edit to `scripts/video3.md`.
The reviewed script maps 39 overlay pages across 10 frames and contains 52
speech chunks. The incremental build synthesized 2 changed chunks, reused 50,
rebuilt 2 timed page WAVs, and reused 37.

The availability-aware controller selected an immediately available RTX 2080 in
`gpu-common` using FP16. Both synthesis requests completed without an HTTP
error, traceback, or timeout. The current script produces 635.92 seconds of
speech and 686.22 seconds of timed narration; the audio phase completed in 97
seconds. Automatic cleanup stopped the tunnel and cancelled the service job
after synthesis.

The final render rebuilt 2 video segments and reused 37. The 39 page WAVs
concatenate byte-for-byte into the 686.22-second continuous narration WAV,
whose PCM SHA-256 is
`31ab1ea80cb19a955cbde185f87e639cb432d9d702eabae48f18ab7231b8ab03`.
The canonical H.264/AAC output is 686.23 seconds, 908 by 510 at 30 fps, with
mono 24-kHz audio, a maximum volume of -0.3 dB, mean volume of -16.1 dB, and a
size of 13.16 MB. A final cache preflight found all 52 chunks present and
required no DCC service.

## Video 4 remote refresh

Video 4 was refreshed on 2026-08-07 from the reviewed source-faithful script.
It has 29 overlay pages and 39 speech chunks. The incremental build synthesized
4 chunks, reused 35, rebuilt 2 timed page WAVs, and reused 27.

The availability-aware controller selected an immediately available RTX 5000
Ada in `gpu-common` using BF16. All requests completed without retries, HTTP
errors, tracebacks, or timeouts. The build produced 497.84 seconds of speech
and 538.04 seconds of timed narration in 39 seconds of audio work; automatic
cleanup stopped the tunnel and cancelled the service job afterward.

The 29 timed page WAVs concatenate byte-for-byte into the continuous narration
WAV, with PCM SHA-256
`9ad2ca5459a089876ef6514844d1782151fef60e46468ad664eed23aeb6274fe`.
The canonical H.264/AAC video is 538.07 seconds at 908 by 510 and 30 fps, with
mono 24-kHz audio, a maximum volume of -0.3 dB, mean volume of -16.2 dB, and a
size of 10.79 MB. A final cache preflight found all 39 speech chunks present and
required no DCC service.

## Video 5 first production cut

Video 5 was built on 2026-08-08 from the reviewed, source-faithful script. It
has 30 overlay pages across 9 frames and 34 speech chunks. Three unclosed
`\\note{...}` blocks in `video5.tex` were repaired so the review and
link-decoration-free production PDFs would compile; the authored narration
was not changed.

The first remote build synthesized all 34 chunks and rebuilt all 30 timed page
WAVs. The availability-aware controller selected an immediately available RTX
2080 in `gpu-common` using FP16. Every request returned successfully, without
retries, HTTP errors, tracebacks, or timeouts. The build produced 714.60 seconds
of speech and 751.36 seconds of timed narration. Automatic cleanup closed the
SSH tunnel and cancelled service job 51499873 after synthesis.

The 30 timed page WAV payloads concatenate byte-for-byte into the continuous
narration WAV, whose PCM SHA-256 is
`22a320ce8104a1ba0c9504e8c79dcf75885245a9d0c7733ce043affc9dd90140`.
The canonical H.264/AAC output is 751.3667 seconds at 908 by 510 and 30 fps,
with mono 24-kHz audio, a maximum AAC volume of -0.4 dB, a mean volume of
-16.5 dB, and a size of 15.39 MB. Its file SHA-256 is
`21f11584a663abe19852e8ccc85d2639fcfc4678c17613445b83cda7ed0693a5`.
A full FFmpeg decode completed without errors, and start, middle, and end frames
were visually inspected. A final cache preflight reused all 34 speech chunks
and all 30 timed page WAVs without requesting a DCC service.

The first cut intentionally preserves the authored page-28 narration. The
existing review comment in `video5.tex` flags its claims about complements of
open intervals and the Cantor set as mathematically garbled: every closed set
is trivially a union of closed sets, while the likely intended claim concerns
closed intervals. This wording should be corrected and page 28 regenerated
before final publication.

## Video 0 hp2 voice regeneration

Video 0 was regenerated on 2026-08-22 with the authorized
`coben_hold_tight_ch1_first29_hp2.wav` x-vector reference. The reference is a
29.49-second mono, 16-bit, 44.1-kHz PCM file with SHA-256
`e7e1abcc34ccad5eebb27121fcfa929d2a2200ed9d95a37fff1c13a0c53c7742`.
The local and durable DCC copies have identical hashes. The new production
service identity is `qwen3-tts-1.7b-base-coben-hp2-xvector-v1`, so none of the
old-voice speech cache was eligible for reuse.

Before regeneration, the current `qwen3-remote-coben` speech/timed cache,
continuous narration, audio/DCC logs, and canonical MP4 were copied to
`build/video0/backups/2026-08-22-pre-hp2/`. The verified backup contains 86
files and occupies 101 MB. Its prior canonical MP4, narration WAV, and metadata
SHA-256 values are respectively
`ba62e1a3a1e5c155170815a75ff823cbe2d08711c6b9fd0f6b748e97534e7a5b`,
`ed1b0b92f0e4cdb486710ffb9c1302d7baacd2bc2aca1fc3813a8613d7a57281`,
and `66f238fccefed81b28336640fe844ff595431d8b246181bab8146b720d982dff`.

The existing scratch environment had partial purge damage. Conda Doctor found
missing files in ten packages, including 2,707 ncurses files. It was preserved
as `/work/hp83/dcc-ai/envs/qwen3-tts-damaged-2026-08-22`, and the controller's
Slurm preparation path built a clean replacement. Conda Doctor reports no
missing package files in the replacement environment.

The clean remote run selected an RTX 5000 Ada in `gpu-common` using BF16. It
synthesized all 32 chunks and rebuilt all 27 timed pages without a failed
request, HTTP error, or retry. The hp2 output contains 534.32 seconds of speech
and 573.17 seconds of timed PCM narration. The 27 page WAV payloads concatenate
byte-for-byte into the continuous narration WAV, whose PCM SHA-256 is
`faba67949d883f06cf32748b90a74bdb3b0df0201f38321fabbf493e6f59aea3`.

The regenerated canonical MP4 is 573.20 seconds, 10.87 MB, H.264 at 908 by 510
and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`3dfb355eab6bc5767c05d44db4566b1e7971357993df4df0ca3e73758da721d8`.
A full FFmpeg decode completed without error, and representative start, middle,
and end frames were visually inspected. The video and audio stream durations
differ by 0.016 seconds, within one 30-fps frame. A final cache-only run reused
all 32 speech chunks and 27 timed page WAVs without requesting DCC.

The hp2 result is materially quieter than the prior production: the final AAC
has mean volume -25.9 dBFS and peak -3.6 dBFS, versus -16.3 dBFS mean and 0.0
dBFS peak for the backed-up PCM narration. No normalization was applied, so the
voice trial remains a direct result of the new reference and existing pipeline.

## Video 0 script and pronunciation refresh

Video 0 was incrementally rebuilt on 2026-08-22 after revisions to
`scripts/video0.md`. The `orthogonality` pronunciation request was simplified
from `or-thog-uh-NAL-uh-tee` to `or-thog-uh-nality` to avoid the previous
exaggerated, unstable output. Cache preflight identified eight missing chunks:
the revised script on pages 4, 7--9, 15, 22, and 25, plus page 16 for the new
pronunciation spelling.

The RTX 5000 Ada BF16 run synthesized those 8 chunks and reused the other 24.
It rebuilt 8 timed pages and reused 19; the video renderer rebuilt 12 segments
and reused 15. All synthesis requests returned successfully without retries,
HTTP errors, or tracebacks, and automatic cleanup stopped the service after the
run. The current output contains 539.60 seconds of speech and 578.45 seconds of
timed narration.

The 27 current page WAV payloads concatenate byte-for-byte into the continuous
narration WAV, whose PCM SHA-256 is
`864253f9559b8966157e586ac6bd72be105d210f7325010284b8f3974a0797e7`.
The current canonical MP4 is 578.4667 seconds, 10.94 MB, H.264 at 908 by 510
and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`d7307483e7d527d0ef630a588a67ba87e61f33e07a34e5fa47c7462dbbfa7629`.
A full FFmpeg decode completed without error; video and audio stream durations
differ by 0.0347 seconds, approximately one 30-fps frame. A final cache-only
run reused all 32 chunks and all 27 timed pages without requesting DCC.

The page-16 pronunciation audition clip is
`build/video0/review-clips/page16-orthogonality-hp2.wav`, SHA-256
`061b8e7072e6e6c9c95c832c33684afe0b3f0a60ae43ac3345e63d9b0788282b`.
The final AAC level remains -25.9 dBFS mean and -3.6 dBFS peak; no normalization
was introduced during this incremental refresh.

## Video 0 standard-spelling pronunciation regeneration

Video 0 was rebuilt again on 2026-08-22 after removing the `orthogonality`
lexicon override. Qwen therefore received the literal standard spelling
`orthogonality` on page 16. Cache preflight found four missing chunks: page 16
for this pronunciation retry and the still-pending authored script edits on
pages 17, 19, and 22. The selected RTX 2080 FP16 run synthesized those four
chunks, reused 28, rebuilt four timed pages, and reused 23. The renderer rebuilt
six video segments and reused 21. All requests returned HTTP 200 without
retries, timeouts, or tracebacks; automatic cleanup closed the tunnel and
cancelled service job 52997358.

The result contains 547.04 seconds of speech and 585.89 seconds of timed PCM
narration. Concatenating the 27 timed page WAV payloads reproduces the
continuous narration byte-for-byte; both have PCM SHA-256
`ffeae834bb2537fe58bd2229b3b4f9bc138e3392a243ea3a135b8f5b32b9f3b7`.
The canonical MP4 is 585.90 seconds, 11,087,050 bytes, H.264 at 908 by 510 and
30 fps, with mono 24-kHz AAC. Its SHA-256 is
`3103bd4f4c1dd849652848114f5a5f8d0fcc247929b270a5692503fbcf65b628`.
A full FFmpeg decode completed without error; its video and audio streams differ
by 1 ms. The AAC level is -26.0 dBFS mean and -3.6 dBFS peak.

A final cache-only run reused all 32 speech chunks and all 27 timed pages and
did not request a DCC allocation. Stable review copies of the four changed raw
speech clips are in `build/video0/review-clips/` with page-specific filenames.

## Video 1 hp2 voice regeneration

Video 1 was regenerated on 2026-08-22 with the Coben hp2 x-vector reference
and service identity `qwen3-tts-1.7b-base-coben-hp2-xvector-v1`. Before the
refresh, its former remote audio cache, timed WAVs, continuous narration WAV,
logs, and canonical MP4 were copied to
`build/video1/backups/2026-08-22-pre-hp2/`. The verified backup has 149 files,
occupies 96 MB, and preserves the prior canonical MP4, narration WAV, and
metadata SHA-256 values:
`53604817cf9eaf9c822c938c3178d8da0b523e248ea1077be62fc3612ff5c4e6`,
`3a602cb1bb665e3e489ccc41cc6e8208d0c845a17596fdbddea48a482ac124f9`, and
`c16d23c6a454ddc693ddbd653cbd2548a9344880ba8a235862cdd06916532a8f`.

The new service selected an RTX 5000 Ada in `gpu-common` with BF16 and SDPA.
It synthesized all 29 speech chunks and rebuilt all 28 timed pages; the video
renderer rebuilt all 28 video segments. All requests returned HTTP 200 without
retries, timeouts, or tracebacks, and automatic cleanup cancelled service job
53006348 after synthesis.

The hp2 result contains 450.72 seconds of speech and 484.62 seconds of timed
PCM narration. Concatenating all 28 timed page WAV payloads reproduces the
continuous narration byte-for-byte; both have PCM SHA-256
`5c9f0e3ad334def8d4064b3fc06e6aa446aedf2c948cba919ba802c8960bbcca`.
The canonical H.264/AAC MP4 is 484.6333 seconds at 908 by 510 and 30 fps, with
mono 24-kHz AAC, a mean volume of -25.8 dBFS, and a peak of -3.9 dBFS. Its
file SHA-256 is
`a6bb09c69e95ace5a1170604470860200bd8d55e96dcc281b3bfadbfb2dfd713`.
The video and audio streams differ by 25 ms, within one 30-fps frame; a full
FFmpeg decode completed without error. A final cache-only run reused all 29
speech chunks and all 28 timed pages without requesting a DCC allocation.

## Video 1 script refresh and Page 3 alternate take

Video 1 was rebuilt on 2026-08-22 after the current reviewed-script edits and
a new Page 3 alternate take. Page 3 retains the authored text, but uses the
page-local Qwen seed `43` rather than the default `42` to obtain a fresh take
of “recorded for a course at Duke University.” The current script also changed
pages 7, 9, 13--16, 20--22, 24, 26, and 27; its current `graduates` lexicon
entry also changed page 19. The remote run synthesized 14 clips and reused 15,
rebuilt 14 timed pages and reused 14, and rebuilt 21 video segments while
reusing seven. The RTX 5000 Ada BF16 requests completed without retries,
timeouts, or tracebacks, and cleanup cancelled service job 53007758.

The current result has 436.64 seconds of speech and 470.54 seconds of timed
PCM narration. The 28 page WAV payloads concatenate byte-for-byte to the
continuous narration WAV, with PCM SHA-256
`2e3d076838a558ff44d3aeb4ba7e24140864ce1fc57ead12faba9a35592cb19e`.
The canonical MP4 is 470.5667 seconds, 8,603,460 bytes, H.264 at 908 by 510
and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`2ee48cdac07e6b2434d1cc4d9055b0622e450e5ee6653e8975660ab22137059d`.
Its mean and peak AAC levels are -25.4 dBFS and -3.5 dBFS. A full FFmpeg decode
completed without error; the MP4 duration differs from the PCM narration by
27 ms, within one 30-fps frame. A final cache-only run reused all 29 clips and
all 28 timed pages without requesting DCC. Stable copies of the 14 regenerated clips are in
`build/video1/review-clips/`.

## Video 1 current-script regeneration

Video 1 was incrementally regenerated on 2026-08-22 from the next set of
authored script and pronunciation edits. The current build synthesized 11
speech clips, reused 18, rebuilt 11 timed pages, and reused 17; the renderer
rebuilt 12 video segments and reused 16. The availability-aware controller
selected an immediately available RTX 5000 Ada in `scavenger-gpu` with BF16.
All requests completed without retries, timeouts, or tracebacks, and automatic
cleanup cancelled service job 53020708.

The current result contains 439.04 seconds of speech and 472.94 seconds of
timed PCM narration. The 28 timed page WAVs concatenate byte-for-byte into the
continuous narration WAV, with PCM SHA-256
`7b817e96d813c2605fe08adbf736e1f04ed852b7c2c8e13c1b52474e8204777e`.
The canonical H.264/AAC MP4 is 472.9667 seconds, 8,644,316 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`c625457bad1eb881d13ca4bc8e520d7db7241f3e180a496f85f4e8d99b0ea6a1`.
Full FFmpeg decoding completed without error; a final cache-only run reused all
29 speech chunks and all 28 timed pages without requesting DCC.

## Video 1 split-cue regeneration

Video 1 was incrementally regenerated on 2026-08-22 from the latest authored
script and pronunciation edits. The current script has 33 speech chunks across
28 rendered overlay pages. The production run synthesized nine changed chunks,
reused 24, rebuilt five timed pages, and reused 23; the renderer rebuilt seven
video segments and reused 21. The availability-aware controller selected an RTX
5000 Ada in `scavenger-gpu` with BF16. All requests completed without retries,
timeouts, HTTP errors, or tracebacks, and automatic cleanup cancelled service
job 53036809.

The current result contains 453.12 seconds of speech and 487.82 seconds of
timed PCM narration. Concatenating the 28 timed page WAV payloads reproduces
the continuous narration WAV byte-for-byte; both have PCM SHA-256
`c463b57e6188bad81b267237464cbffa2bffd3a7fefb059badef4d731c5c284e`.
The canonical H.264/AAC MP4 is 487.8333 seconds, 8,873,695 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`9b086e85331668263b9a6e1e6ca262007ea9b1469ada13b235f9b142b9b8e5bb`.
Full FFmpeg decoding completed without error; the final AAC level is -25.6 dBFS
mean and -3.9 dBFS peak. A final cache-only run reused all 33 speech chunks and
all 28 timed pages without requesting DCC.

## Video 1 conditional and meta-statement refresh

Video 1 was incrementally regenerated on 2026-08-23 after the current edits to
the Page 20 conditional examples and two Page 26 meta-statement cues. The
remote production run synthesized five speech chunks, reused 28, rebuilt two
timed pages, and reused 26; the renderer rebuilt four video segments and reused
24. The controller selected an RTX 5000 Ada in `scavenger-gpu` with BF16, and
automatic cleanup cancelled service job 53039028. The successful remote run had
no request retries, timeouts, HTTP errors, or tracebacks.

The result contains 452.96 seconds of speech and 487.66 seconds of timed PCM
narration. The continuous narration WAV has SHA-256
`f097ef02f7bbc0b734e89fcfbbd8f070be84457780cbafadc2dc4363e3ec030f`.
The canonical H.264/AAC MP4 is 487.6667 seconds, 8,925,888 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`791ee51f6cd3983d18d618521e08c7d77e72bef99170367cabca874d5ce0fdfc`.
Full FFmpeg decoding completed without error; the audio and video streams differ
by 30 ms, within one 30-fps frame. The final AAC level is -25.7 dBFS mean and
-3.9 dBFS peak. A final cache-only verification reused all 33 speech chunks and
all 28 timed pages without requesting DCC. Stable review copies of the five
regenerated clips are in `build/video1/review-clips/latest-2026-08-23/`.

## Video 2 hp2 voice regeneration

Video 2 was regenerated on 2026-08-23 with the Coben hp2 x-vector reference
and service identity `qwen3-tts-1.7b-base-coben-hp2-xvector-v1`. Before the
refresh, the prior-voice remote audio cache, video-work state, logs, and
canonical MP4 were copied to `build/video2/backups/2026-08-23-pre-hp2/`. The
verified backup contains 223 files and occupies 222 MB; its preserved MP4,
narration WAV, and metadata SHA-256 values are respectively
`2b3dac998a2d7e7abfa64ff4f122465711fe04d2d14c52bb4e0b8d8b1ddf3860`,
`7eb33010103b9008cc498cc48327d6512c998a9766499388be71a032bf6557ff`, and
`5fc4af4e50e53431b4c9d52d9cade00c06a3e11cb7dccd93cdac72e3f1e16d43`.

All 30 current speech chunks were newly synthesized and all 29 timed pages and
video segments were rebuilt. The availability-aware controller selected an
immediately available RTX 2080 in `gpu-common` with FP16 and SDPA; all remote
requests succeeded without retries, timeouts, HTTP errors, or tracebacks, and
automatic cleanup cancelled service job 53127465.

The hp2 result contains 675.44 seconds of speech and 710.29 seconds of timed
PCM narration. The continuous narration WAV has SHA-256
`daf61065612a2c785512fc3e33343a39cfdf1076dcdb0f78c662d48ce6904ac6`.
The canonical H.264/AAC MP4 is 710.3000 seconds, 13,615,511 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`4e8e947873edd499f0f018e23ef30af563c8536bcaf35f013b3619bfcb77faf2`.
Full FFmpeg decoding completed without error; audio and video stream durations
differ by 28 ms, within one 30-fps frame. The final AAC level is -25.6 dBFS
mean and -3.5 dBFS peak. A final cache-only run reused all 30 clips and all 29
timed pages without requesting DCC.

## Video 2 hp3 voice regeneration

Video 2 was regenerated on 2026-08-24 with the Coben hp3 x-vector reference
`coben_hold_tight_ch1_first29_hp3.wav`. The 29.49-second mono, 16-bit,
44.1-kHz PCM reference was uploaded to
`/hpc/group/pfisterlab/hp83/dcc-ai/voices/` and verified there with SHA-256
`eee11132b2cb130a97ae3042419a510be6d948dec563641b89847eac3d662aa3`.
The service identity was bumped to
`qwen3-tts-1.7b-base-coben-hp3-xvector-v1`, so none of the hp2 speech cache
was eligible for reuse.

The first build exposed a malformed `[[pause 0,2]]` marker on Page 7 of
`scripts/video2.md`; it was corrected to `[[pause 0.2]]` before synthesis.
The clean run selected an RTX 5000 Ada in `gpu-common` with BF16 and SDPA,
synthesized all 31 chunks, and rebuilt all 29 timed pages without HTTP errors
or retries. It produced 698.3 seconds of speech and 733.4 seconds of timed
PCM narration. The continuous narration WAV has SHA-256
`f703ebed07d7a7cd8fd3b815cd900f343a68c680fdd9ff1c4eb8630f80a1b48e`.

The canonical H.264/AAC MP4 is 733.4000 seconds, 12,894,254 bytes, at 908 by
510 and 30 fps. Its SHA-256 is
`61eae84b33d25a9dc7641c96675203b90ce5d771b8e1075de023744f5c6df551`.
Automatic cleanup stopped the DCC service after synthesis.

## Video 10 first production cut

Video 10 was built on 2026-09-27 from the reviewed script with the Coben hp3
x-vector reference and service identity
`qwen3-tts-1.7b-base-coben-hp3-xvector-v1`. Because the queued DCC allocation
did not start in time, the 23 speech chunks were synthesized on a temporary
Vast.ai A10 instance using BF16 and SDPA. All synthesis requests succeeded,
and a final cache-only run reused all 23 speech chunks and all 23 timed pages
without requesting a DCC service.

The result contains 573.92 seconds of speech and 604.87 seconds of timed PCM
narration. The 23 timed page WAV payloads concatenate byte-for-byte into the
continuous narration WAV; both have PCM SHA-256
`a26febfac6d1444c503a3b6f68101af281c00763c3dba4b5e98d1e2786e18ded`.
The canonical H.264/AAC MP4 is 604.9000 seconds, 10,556,763 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`9db3a735e72a6e5538396dfa45737d783b248c835e5fb0f35cf32880e4191b48`.
Full FFmpeg decoding completed without error; the video and audio streams
differ by 15 ms, within one 30-fps frame. The final AAC level is -29.1 dBFS
mean and -5.8 dBFS peak. Representative start, middle, and end frames were
visually inspected.

## Video 10 script and slide refresh

Video 10 was rebuilt on 2026-09-27 after edits to the reviewed script and
slide source. The incremental Vast.ai A10 run synthesized 25 changed speech
chunks and reused 10, rebuilt 13 timed page WAVs and reused 10, and completed
the audio phase in 598.28 seconds without request errors or retries. A final
cache-only pass found all 35 speech chunks present and did not request a DCC
allocation. The renderer rebuilt 16 video segments and reused seven.

The refreshed result contains 578.56 seconds of speech and 613.11 seconds of
timed PCM narration. The 23 timed page WAV payloads concatenate byte-for-byte
into the continuous narration WAV; both have PCM SHA-256
`3426271cd5676c4845fa9445cceb0fb59a449b8182e79c4a2105d3055bd00893`.
The canonical H.264/AAC MP4 is 613.1333 seconds, 10,735,781 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`6f78d59ef9ab3c32c7119a1d444e20a1b4d837be4b74b79c200607bd52cdd3a7`.
Full FFmpeg decoding completed without error; video and audio stream durations
differ by 13 ms, within one 30-fps frame. The final AAC level is -29.0 dBFS
mean and -5.8 dBFS peak. Representative frames, including the edited vector
space, standard-basis, and invertibility slides, were visually inspected.

## Video 10 second script and slide refresh

Video 10 was rebuilt again on 2026-09-27 after the next script and slide
revision. The incremental Vast.ai A10 run synthesized 14 changed speech chunks
and reused 22, rebuilt 11 timed page WAVs and reused 12, and completed the
audio phase in 454.43 seconds without request errors or retries. A final
cache-only pass found all 36 speech chunks present and did not request a DCC
allocation. The renderer rebuilt 15 video segments and reused eight.

The refreshed result contains 584.72 seconds of speech and 620.17 seconds of
timed PCM narration. The 23 timed page WAV payloads concatenate byte-for-byte
into the continuous narration WAV; both have PCM SHA-256
`c8a7a8a6ae3c834674c5080ceac06d9f7fcdd27923a5e82efc4cc849ed068bfc`.
The canonical H.264/AAC MP4 is 620.2000 seconds, 10,862,945 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`a2a6dd206a6a029790f219f1f8ceface514cc264b689cad2d8ff94368d7b6b7e`.
Full FFmpeg decoding completed without error; the MP4 differs from the PCM
narration by 30 ms, within one 30-fps frame. The final AAC level is -28.6 dBFS
mean and -5.8 dBFS peak. Representative frames, including the edited vector
space, function-space, and standard-basis slides, were visually inspected.

## Video 10 third script refresh

Video 10 was rebuilt again on 2026-09-27 after the next narration revision.
A malformed `[[pause 0.3]` marker on page 11 was corrected to
`[[pause 0.3]]` before synthesis. The incremental Vast.ai A10 run synthesized
seven changed speech chunks and reused 30, rebuilt six timed page WAVs and
reused 17, and completed the audio phase in 232.74 seconds without request
errors or retries. A final cache-only pass found all 37 speech chunks present
and did not request a DCC allocation. The renderer rebuilt 10 video segments
and reused 13.

The refreshed result contains 579.52 seconds of speech and 615.27 seconds of
timed PCM narration. The 23 timed page WAV payloads concatenate byte-for-byte
into the continuous narration WAV; both have PCM SHA-256
`a0b73f89c415e4329ea4a9ccfd26a67b1ab78b4fad3e985f1f98558c71b770df`.
The canonical H.264/AAC MP4 is 615.3000 seconds, 10,829,640 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`7f1d4c7230801374ba20e21f35dd86e6a1572945d391bf61708eeff6616aeaa6`.
Full FFmpeg decoding completed without error; video and audio stream durations
differ by 4 ms. The final AAC level is -28.7 dBFS mean and -5.8 dBFS peak.
Representative start, end, and changed-page frames were visually inspected.

## Video 10 fourth script refresh

Video 10 was rebuilt again on 2026-09-27 after two further narration edits.
The incremental Vast.ai A10 run synthesized two changed speech chunks and
reused 35, rebuilt two timed page WAVs and reused 21, and completed the audio
phase in 83.55 seconds without request errors or retries. A final cache-only
pass found all 37 speech chunks present and did not request a DCC allocation.
The renderer rebuilt four video segments and reused 19.

The refreshed result contains 580.80 seconds of speech and 616.55 seconds of
timed PCM narration. The 23 timed page WAV payloads concatenate byte-for-byte
into the continuous narration WAV; both have PCM SHA-256
`b2254f01748d718562816a4b5c5f83243f7ce81cf469605ce71b14fc347d76eb`.
The canonical H.264/AAC MP4 is 616.5667 seconds, 10,830,136 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`5b5c1299b24949de9164d89a5e2ff18e601fdf2b531d09102b42f0a8422a923f`.
Full FFmpeg decoding completed without error; the MP4 differs from the PCM
narration by 17 ms, within one 30-fps frame. The final AAC level is -28.8 dBFS
mean and -5.8 dBFS peak. Representative start, end, and changed-page frames
were visually inspected.

## Video 12 first production cut

Video 12 was built on 2026-10-13 after the current script, slide, and
pronunciation edits. The pending DCC allocation had an estimated wait of about
three days, so the 14 missing speech chunks were synthesized on a temporary
Vast.ai RTX 5090 instance using BF16 and SDPA. Before private input was
uploaded, the host passed a CUDA smoke test with NVIDIA driver 595.71.05,
PyTorch 2.9.1+cu128, and CUDA 12.8. A real authenticated synthesis request also
passed before the queued DCC fallback was cancelled.

The incremental run synthesized 14 speech chunks, reused 14, rebuilt 11 timed
page WAVs, reused 13, and completed the audio phase in 200.20 seconds without
request errors or retries. The renderer rebuilt 13 video segments and reused
11. A final cache-only pass found all 28 speech chunks present and reused all
24 timed pages without requesting a DCC service.

The result contains 460.4 seconds of speech and 490.1 seconds of timed mono,
16-bit, 24-kHz PCM narration. The 24 timed page WAV payloads concatenate
byte-for-byte into the continuous narration WAV; both have PCM SHA-256
`db29a24e3bf89fd2820fbe3459291b21865603ced5badcb4e3297208bb7616fb`.
The canonical H.264/AAC MP4 is 490.1667 seconds, 8,682,673 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`21eeca84c435ea030bc4d3de7963223c0fe4bc717e342d685be1dc6664cd6ef5`.
Full FFmpeg decoding completed without error; video and audio stream durations
differ by 12 ms, within one 30-fps frame. The final AAC level is -29.2 dBFS
mean and -7.9 dBFS peak. Representative start, middle, and end frames were
visually inspected.

## Video 12 first script refresh

Video 12 was rebuilt again on 2026-10-13 after the next narration and slide
revision. The incremental Vast.ai RTX 5090 run synthesized five changed speech
chunks, reused 23, rebuilt four timed page WAVs, reused 20, and completed the
audio phase in 94.80 seconds without request errors or retries. The renderer
rebuilt seven video segments and reused 17. A final cache-only pass found all
28 speech chunks present and reused all 24 timed pages without requesting a
DCC service.

The refreshed result contains 461.0 seconds of speech and 490.8 seconds of
timed mono, 16-bit, 24-kHz PCM narration. The 24 timed page WAV payloads
concatenate byte-for-byte into the continuous narration WAV; both have PCM
SHA-256
`291236e33f9ac4fe0593d492721e7241391c97c2be85dcf6e8b5ec90f3ec6fc5`.
The canonical H.264/AAC MP4 is 490.8000 seconds, 8,711,255 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`248353dc35f491a223db1760edbaf1e4be26b65e5e0bbabb3653c14f85d07ad9`.
Full FFmpeg decoding completed without error; video and audio stream durations
differ by 5 ms. The final AAC level is -29.2 dBFS mean and -7.9 dBFS peak.
Representative start, middle, and end frames were visually inspected.

## Video 13 first production cut

Video 13 was built on 2026-10-17 from the reviewed transcript and slide edits,
including the function-space qualification, the explicit finite-p sequence
spaces, the shorter convergence-proof narration with two 0.4-second pauses,
and the nonclosed-span example using the standard basis and infinite support.
The DCC controller's earliest estimated start was 2026-10-18 at 11:31:58 EDT,
so no new DCC job was submitted. Synthesis used a temporary Vast.ai RTX 5090
with NVIDIA driver 610.43.03, PyTorch 2.9.1+cu128, CUDA 12.8, BF16, and SDPA.
The public model revision was pinned to
`fd4b254389122332181a7c3db7f27e918eec64e3`; the Coben hp3 x-vector reference
and service identity `qwen3-tts-1.7b-base-coben-hp3-xvector-v1` were retained.

All 30 speech chunks were newly generated. After the first cached chunk, the
client was deliberately interrupted to reduce the server CPU thread count
from 64 to four. This did not materially improve the approximately 1.8x
real-time synthesis rate on the AMD EPYC 7532 host. The resumed run synthesized
29 chunks, reused the first chunk, rebuilt all 27 timed pages, and finished in
1159.03 seconds. Completed requests succeeded without HTTP errors. The final
cache-only Make run reused all 30 speech chunks and all 27 timed pages without
requesting DCC. The renderer built all 27 video segments.

The result contains 654.80 seconds of speech and 689.30 seconds of timed mono,
16-bit, 24-kHz PCM narration. The 27 timed page WAV payloads concatenate
byte-for-byte into the continuous narration WAV; both have PCM SHA-256
`c6f821ae2e990e46eb062464449015a43052ce5ebe8526f48c7f2b2d5fe2346d`.
The canonical H.264/AAC MP4 is 689.3000 seconds, 11,776,777 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`648214eb47dc16458c10ee606191401ca7309507e8d0bab59b23605163952514`.
Full FFmpeg decoding completed without error, and the reported audio and
video stream durations match. The final AAC level is -29.0 dBFS mean and
-7.6 dBFS peak. Representative start, middle, and end frames were visually
inspected. Source, transcript, and lexicon hashes remained unchanged during
the run. Essential host logs and resolved dependencies were retrieved locally.
Vast.ai instance 56484303 was destroyed after validation; the final account
inventory was empty. Estimated rental cost was approximately $0.50.

## Video 13 Banach pronunciation and script refresh

Video 13 was rebuilt on 2026-10-18 with the shared `Banach` synthesis spelling
`bah-knock` and the instructor's current script edits. A non-submitting DCC
plan estimated its earliest GPU start at 2026-10-19 10:06:46 EDT, so no new
DCC job was submitted. The slide compiler exposed an undefined `\cdor`,
corrected to `\cdot`. Production-only transcript fixes converted `[[0.4]]`
to `[[pause 0.4]]` and the raw norm notation to spoken mathematics; other
authored wording was retained.

The selected Vast.ai machine 147982 has an RTX 5090 and i9-13900KF, was
verified, and reported 99.70986% reliability. Machine-specific written reviews
were not available from the CLI/public searches; generic benchmark history
was inspected, then actual Qwen throughput was tested before production.
Instance 56635818 passed the CUDA test before uploading the authorized private
reference. It used NVIDIA driver 595.91.07, PyTorch 2.9.1+cu128, CUDA 12.8,
BF16/SDPA, the same pinned public model revision and Coben hp3 service identity
as the first cut, and four PyTorch CPU threads. The initial short request took
1.99 seconds for 2.64 seconds of speech; the title took 9.39 seconds for
13.52 seconds of speech (0.69 server-side real-time factor), approximately
2.6 times faster than the previous host's approximately 1.8 factor.

The incremental run synthesized 35 chunks, reused eight, rebuilt 21 timed
pages, reused six, and finished in 416.54 seconds without request failures or
retries. The final cache-only Make pass reused all 43 chunks and all 27 timed
pages without contacting DCC. The renderer rebuilt 20 video segments and
reused seven. All 12 chunks containing Banach have the new synthesis spelling.

The result contains 679.12 seconds of speech and 717.92 seconds of timed mono,
16-bit, 24-kHz PCM narration. The 27 timed page WAV payloads concatenate
byte-for-byte into the continuous narration WAV; both have PCM SHA-256
`63141577b978e40a2f0bd61fc2ba0c2eb9a953f970a9af2c3aa598d257bbf8cf`.
The canonical H.264/AAC MP4 is 717.9333 seconds, 12,114,496 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`448fcdc48c798b0f681eb8cf52af0bf0e1413e97b515b5df9e62d64c8a5d5f84`.
Full FFmpeg decoding passed. Audio and video stream durations differ by
24.3 ms, within one frame; the MP4 differs from PCM narration by 13.3 ms.
Final AAC levels are -29.0 dBFS mean and -6.8 dBFS peak. Representative
start, middle, end, corrected-norm, and Banach-definition frames were visually
inspected. These are technical/visual checks, not a subjective listening review.
The TeX, script, and lexicon hashes remained unchanged during synthesis and
encoding. Validation details, logs, resolved dependencies, and reuse notes are
saved under `build/video13/vast-20261018/`.

Per the instructor's request, instance 56635818 is retained for reuse rather
than destroyed, with its pinned setup and authorized reference on disk.
Compute was stopped after validation. The selected running rate was about
$0.95/hour; retained 50-GB storage is $0.013889/hour, approximately $0.333/day.

## Video 13 approved Banach/Schauder refresh

Video 13 was rebuilt again on 2026-10-18 after the instructor auditioned and
approved `shau-der` for Schauder and `bahnawk` for Banach. The current authored
script edits were retained. Cache planning identified 26 changed chunks and
17 unchanged chunks. The approved page-18 test's speech fingerprint matched
the production settings and was copied into the production speech cache;
the remaining 25 changed chunks were synthesized on Vast.ai instance 56642480.

This verified RTX 5090/Ryzen 9950X machine (45386) reported 99.92029%
reliability at selection. The pinned environment used NVIDIA driver 595.91.07,
PyTorch 2.9.1+cu128, CUDA 12.8, BF16/SDPA, and four PyTorch CPU threads.
The saved environment restarted without reinstalling packages or downloading
the model. Coben hp3 x-vector identity and the pinned public model revision
were unchanged. The approved sample generated 11.68 seconds of audio in
5.24 seconds server-side (0.45 real-time factor).

Production audio completed in 236.04 seconds, with 25 chunks synthesized and
18 reused (17 unchanged plus the approved test), 22 timed pages rebuilt and
five reused, without request failures or retries. The final cache-only Make
pass reused all 43 speech chunks and all 27 timed pages, skipping DCC.
The renderer rebuilt 24 video segments and reused three. Metadata checks
confirmed all 13 Banach occurrences use `bahnawk` and all four Schauder
occurrences use `shau-der`.

The result contains 664.56 seconds of speech and 703.36 seconds of timed mono,
16-bit, 24-kHz PCM narration. The 27 timed page WAV payloads concatenate
byte-for-byte into the continuous narration WAV; both have PCM SHA-256
`a3c8f5dd1f98b0bca9e83b7992228078b37340f85c4a09050429d2dbfc3b19ff`.
The canonical H.264/AAC MP4 is 703.3667 seconds, 11,818,509 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`63f436845010f19583fd3f35b634f584175e8d7088c887414a4d22bff49b9b2f`.
Full FFmpeg decoding passed. Video and audio stream durations differ by
6.7 ms, within one frame. Final AAC levels are -28.9 dBFS mean and -6.9 dBFS
peak. Representative start, middle, and end video frames were visually
inspected. All changed speech WAVs passed PCM format and payload-length checks.
The source, transcript, and lexicon hashes remained unchanged during production.

Planning, generation logs, validation, frame checks, and page-ordered changed
clip links are saved under `build/video13/vast-bahnawk-production-20261018/`.
The instructor received direct chat links to all 26 changed chunks, including
the approved test. Both retained instances are preserved rather than destroyed;
compute was stopped after validation. Combined retained storage is approximately
$1.333/day ($1/day for 56642480 and $0.333/day for 56635818).

## Video 13 current-script and Riemann refresh

Video 13 was rebuilt on 2026-10-18 after the instructor confirmed the current
script was ready. The script, TeX, pronunciation lexicon, audio configuration,
and matching slide PDF were snapshotted under
`build/video13/vast-final-current-20261018/` for a stable build. The final
lexicon uses `bahnawk` for Banach, `shau-der` for Schauder, and the instructor's
latest choice `ree-men` for Riemann. Frozen input hashes remained unchanged
during production, and the corresponding live source files still matched
after encoding.

The snapshot contains 49 speech chunks across 27 pages. Twelve missing chunks
were synthesized and 37 cached chunks reused on the saved RTX 5090/i9-13900KF
instance 56635818, using its existing pinned Qwen environment and Coben hp3
x-vector reference. No reinstall, model download, new rental, or DCC allocation
was needed. Audio completed in 129.62 seconds without request failures, with
seven timed pages rebuilt and 20 reused. The final Make pass found all 49
speech chunks cached, reused all 27 timed pages, and skipped DCC. The renderer
rebuilt 12 video segments and reused 15.

Fourteen speech chunks differ from the previous validated MP4: twelve generated
in this run and two already cached from the preceding editing session. Their
page-ordered chat links are also recorded in `validation.json`. Metadata checks
verified all 13 Banach occurrences, four Schauder occurrences, and one Riemann
occurrence use the selected spellings. Changed WAVs passed PCM format and
payload-length checks. These checks do not constitute a subjective listening
review of the entire narration.

The result contains 681.68 seconds of speech and 722.38 seconds of timed mono,
16-bit, 24-kHz PCM narration. The 27 timed page WAV payloads concatenate
byte-for-byte into the continuous narration WAV; both have PCM SHA-256
`6fde0c8fdd07a7aeabc964cd3693ee5fd3b7a1d6313aa6a8def9367e295eaff1`.
The canonical H.264/AAC MP4 is 722.4000 seconds, 12,060,645 bytes, at 908 by
510 and 30 fps, with mono 24-kHz AAC. Its SHA-256 is
`a43c099fac4aa0100592f76f76208b76619f8393b66dc84e2f6c5b60e3890297`.
Full FFmpeg decoding passed. Audio/video stream durations differ by 11 ms,
and the MP4 differs from the PCM narration by 20 ms, both within one video
frame. Final AAC levels are -29.0 dBFS mean and -6.9 dBFS peak. Representative
start, middle, and end video frames were visually inspected.

Both saved Vast instances are retained, not destroyed, with compute stopped
after validation. Combined stopped storage remains approximately $1.333/day.

## Video 13 Vast cleanup

At the instructor's explicit request on 2026-10-18, Vast.ai instances 56635818
and 56642480 were permanently destroyed, including their remote disks.
The subsequent team-account instance inventory was empty, ending further
instance compute and storage charges. Earlier retention instructions in this
file and the archived build notes are superseded by this cleanup.
The local canonical MP4 remains intact with SHA-256
`a43c099fac4aa0100592f76f76208b76619f8393b66dc84e2f6c5b60e3890297`;
local audio, reference media, pinned bootstrap scripts, and retrieved logs
remain available. New GPU work will require a new rental and setup.
