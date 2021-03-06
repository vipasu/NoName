## InputePowerSpectra
2/2016-

---

# Concept
We aim to support a flexible integration of how to specify powerspectra to initialize simulations whether for particles or gridded data. 

## Current implementations
- Powerlaw Scale Free PowerSpectra
- "Delta Functions" of Powerlaw PowerSpectra
	
### Powerlaw Scale Free Spectra
These are specifed by the powerlaw index and their normalization.
So that in your `.conf` file
```InputPowerSpectrum = scaleFreePS(n, norm)```
would be a P = norm × kⁿ Powerspectrum. 

### Delta Function of Powerlaw Spectra
```
multiplePeaksPS(-1, 1, [1, 10, 30], 0.1) # (n, norm, kspikes, delta_k_over_k)
````

specifies a powerlaw spectrum that has a powerlaw indec `-1` and normalization such that the Powerspectrum is 1 for `k=1`, for all k that at `k=1` and `k=10` are within δk/k of 1. The resulting Powerspectrum looks like this:
![MultiplePeaks](./figs/InputMultiplePeaksPS.png)
Everything is zero but in the neighborhood of the input `k` vector `[1, 10, 30]`. 
It also supports different widths for each spike as in `multiplePeaksPS(-1, 1, [1, 10, 30], [0.1, 0.2, 0.3])`
