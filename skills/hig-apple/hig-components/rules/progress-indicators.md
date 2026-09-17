# Progress indicators — rule card

**Progress indicators** communicate ongoing work: a determinate progress bar (known duration/progress), an indeterminate spinner (unknown), or a skeleton (content shape loading). Each fits a distinct situation.

**Triggers**: `CircularProgressIndicator`, `LinearProgressIndicator`, `ProgressIndicator`, `LoadingIndicator`, `Spinner`, `spinner`, `loading`, `loader`, `progress`, `<progress`, `Skeleton`, `skeleton`, `shimmer`, `ActivityIndicator`, `RefreshIndicator`, `pulse`, `placeholder`.

## Rules

1. **Pick the right kind:**
   - **Determinate bar/ring** when progress has a percentage or a finite unit count (upload, download, install).
   - **Indeterminate spinner** for unknown-duration background work (fetching, processing).
   - **Skeleton** (shimmering content-shaped blocks) when you can show real layout early and the content arrives soon.
2. **Never blank.** During load, the interface shows *something* — the previous content dimmed + spinner, a skeleton, or a partial render. A white flash followed by content is the top anti-pattern.
3. **Spinner ≠ progress on user click.** If the work is truly quick (< ~1s), a spinner is often unnecessary; show immediate state (pressed → result). Reserve spinners for real waits; otherwise perception of speed dies.
4. **Keep the user oriented.** While loading, the surrounding UI must remain stable — no layout jumps, no shifting positions. Skeleton dimensions should match final content.
5. **Progress must be accurate-ish.** Never sit at 99% for a long pause; never lie about percentage when unknown (that's an indeterminate spinner's job).
6. **Failure surfaces honestly.** If loading fails, show the error in place with recovery (reload), not an endless spinner.
7. **Cancel/overview where work is long & cancellable** — show a cancel affordance or at least let the user leave without losing work.

## The why

Progress UI is *promise communication*: "we know you're waiting, here's how you're doing." Blank screens lie ("nothing is happening"), spinners lie when progress is known, and endless stalls teach people to abandon.

## Implementation hints

- Detect triggers above. Check:
  - Blank/white area during async load → flag (need skeleton/spinner/dimmed prior).
  - Determinate progress with no %/units available → suggest spinner (or reverse).
  - Skeleton present but dimensions ≠ final → flag (layout jump).
  - Spinner appended to every button/tap including micro-actions → flag.
  - Error path: does the failure state ever end the spinner? → flag infinite-loading.
  - Compose with a11y: announce progress; `aria-busy`, `aria-valuenow`.

## Checklist

- [ ] right kind (determinate/indeterminate/skeleton)
- [ ] never a blank load
- [ ] stable layout, no jumps
- [ ] honest progress or honest indeterminate
- [ ] failure state with recovery
- [ ] cancellable long work
- [ ] announced to screen readers