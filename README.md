# AnalysispulsesMayoClinic

AnalysispulsesMayoClinic is a lightweight analysis project for studying pulse-by-pulse detector behavior using paired acquisitions from:

- a **detector** channel (measurement under evaluation), and
- a **reference** channel (stability baseline).

The repository focuses on no-movement and scan datasets exported as CSV files, with notebooks that:

1. load detector/reference time-series data,
2. detect individual pulses in each signal,
3. synchronize detector pulses with the corresponding reference pulses, and
4. evaluate normalization quality using the detector/reference ratio.

## Project purpose

The main purpose is to validate whether pulse normalization with a reference signal reduces variability and improves reproducibility. In practice, this allows you to:

- compare pulse extraction strategies (rule-based vs SciPy peak detection),
- test synchronization methods (index-based vs time-based matching), and
- quantify how ratio-based normalization behaves across datasets.

## Main notebooks

- `Nomovement.ipynb` — baseline analysis for no-movement acquisitions, including:
  - original pulse extraction/synchronization workflow,
  - SciPy-based alternatives (`getpulses_scipy`, `syncpulses_bytime`), and
  - side-by-side comparisons to verify equivalent outcomes on the same data.
- `pulse_matching_scipy_notebook.ipynb` — additional experimentation for pulse matching workflows.

## Typical workflow

1. Open `Nomovement.ipynb`.
2. Run cells in order to generate pulse-level DataFrames.
3. Inspect detector, reference, and ratio plots.
4. Compare summary statistics (mean/std/CV) between methods.

## Data assumptions

The current notebook logic assumes:

- input CSV files contain `Time`, `ch0`, and `ch1` columns,
- first/last portions of acquisitions represent baseline (no-light) intervals,
- detector and reference are acquired close enough in time to enable pulse matching.

If these assumptions change, thresholds and synchronization tolerances should be re-tuned.
