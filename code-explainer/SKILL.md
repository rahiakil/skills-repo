---
name: code-explainer
description: >
  Annotates, explains, refactors, and documents simulation and analysis code for photonics
  research. Works with Python (numpy, scipy, matplotlib, gdspy, meep, EMpy), MATLAB,
  Lumerical script, and COMSOL LiveLink. Produces inline comments, docstrings, README
  files, and plain-English explanations of what code does physically. Also converts
  scripts between languages and modernizes legacy code. Trigger: "explain this code",
  "add comments", "what does this do", "refactor", "document this script", "convert to
  Python", "write a docstring", "clean up my code", "add type hints".
version: "1.0"
added: 2026-04-07
domain: code, research
---

# Code Explainer Skill

You annotate, explain, refactor, and document research code with both technical
accuracy and physical intuition.

## Modes

- `explain` — Plain-English explanation of what the code does physically, not just syntactically
- `annotate` — Add inline comments to every non-obvious line
- `docstring` — Write NumPy-style docstrings for all functions
- `refactor` — Clean up structure, naming, remove magic numbers
- `convert` — Translate between Python / MATLAB / Lumerical script / Julia
- `readme` — Write a README.md for a script or project folder
- `debug` — Identify likely bugs or numerical issues

## Explanation Style

When explaining photonics code, always connect code to physics:
- Don't just say "this multiplies by k" — say "this computes the wave vector
  k = 2π·n/λ, which sets how fast the phase accumulates as light propagates"
- Identify what physical quantity each variable represents
- Flag unit choices (nm vs. m vs. um) and ensure consistency
- Note where approximations are made (paraxial, scalar, slowly-varying envelope)

## Annotation Template

```python
# ── Physical meaning: [what this represents] ──────────────────────
wavelength_nm = 1550          # Operating wavelength [nm] (telecom C-band)
n_eff = 2.45                  # Effective refractive index of SOI waveguide (TE0 mode)
k0 = 2 * np.pi / (wavelength_nm * 1e-9)  # Free-space wave vector [rad/m]
beta = k0 * n_eff             # Propagation constant [rad/m]
```

## Docstring Template (NumPy style)

```python
def lorentzian_fit(wavelength, center, fwhm, amplitude, offset):
    """
    Fit a Lorentzian lineshape to a photonic resonance.

    Parameters
    ----------
    wavelength : np.ndarray
        Wavelength array [nm].
    center : float
        Resonance center wavelength [nm].
    fwhm : float
        Full-width at half-maximum [nm]. Related to Q-factor by Q = center/fwhm.
    amplitude : float
        Peak transmission amplitude [linear, not dB].
    offset : float
        Baseline transmission offset.

    Returns
    -------
    np.ndarray
        Lorentzian transmission profile, same shape as wavelength.

    Notes
    -----
    Q-factor extracted as: Q = center / fwhm
    """
```

## Common Photonics Code Patterns to Recognize

- Transfer matrix method (TMM) → explain layer-by-layer phase accumulation
- FDTD time stepping → explain Courant stability condition
- Mode overlap integral → explain why it measures coupling efficiency
- S-parameter conversion (S to T, ABCD) → explain physical meaning
- Fourier transform of field profile → explain angular spectrum
- Lorentzian/Fano fit → explain resonance physics

## Refactoring Rules

1. No magic numbers — define named constants with units in comments
2. Functions do one thing — split multi-purpose functions
3. Variable names are physical: `n_eff` not `n`, `lambda_nm` not `l`
4. Add `assert` statements for physical sanity checks:
   ```python
   assert 0 < n_eff < 4, "Refractive index out of physical range for silicon"
   ```
5. Use `pathlib.Path` for file I/O, never raw string paths
