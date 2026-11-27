<h1 align="center">Fit IVIM</h1>

<p align="center">
  Fits the intravoxel incoherent motion (IVIM) model to DWI with DIPY dipy_fit_ivim 1.1.1 and outputs maps of predicted S0, perfusion fraction, pseudo-diffusion D* and diffusion D.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.322"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.322-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Fits the intravoxel incoherent motion (IVIM) model to DWI with DIPY dipy_fit_ivim 1.1.1 and outputs maps of predicted S0, perfusion fraction, pseudo-diffusion D* and diffusion D.**

Runs DIPY's dipy_fit_ivim workflow on the DWI with its bvals, bvecs and brain mask. IVIM needs multiple low b-values (below a few hundred s/mm^2) to separate perfusion from diffusion; it is not meaningful for single-shell high-b data. Note that this version of main passes the b0_threshold value to --split_b_D and --split_b_S0, so those two parameters are not used.

| | |
|---|---|
| **Inputs** | `neuro/dwi` · `neuro/mask` |
| **Outputs** | `raw` |
| **Container** | `brainlife/dipy:1.1.1` |
| **Resources** | 6 CPUs |
| **Run it** | [doi.org/10.25663/brainlife.app.322](https://doi.org/10.25663/brainlife.app.322) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `DWI` | `neuro/dwi` | yes | Diffusion-weighted image with bvals and bvecs. Should include several low b-values for the IVIM bi-exponential fit. |
| `mask` | `neuro/mask` (brain, dwi) | yes | Brain mask in DWI space restricting the fit. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `raw` | - S0_predicted.nii.gz: Name of the S0 signal estimated to be saved - perfusion_fraction.nii.gz: Name of the estimated volume fractions to be saved - D_star.nii.gz: Name of the estimated pseudo-diffusion parameter to be saved - D.nii.gz: Name of the estimated diffusion parameter to be saved |

<details>
<summary><b>Parameters</b> (4)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `split_b_D` | number | `400` | Value to split the bvals to estimate D for the two-stage process of fitting |
| `split_b_S0` | number | `200` | Value to split the bvals to estimate S0 for the two-stage process of fitting. |
| `b0_threshold` | number | `0` | Threshold value for the b0 bval. |
| `command` | string | `dipy_fit_ivim` | DIPY workflow to run; only dipy_fit_ivim is accepted. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.322](https://doi.org/10.25663/brainlife.app.322), choose `neuro/dwi`, `neuro/mask` from your project, set the parameters and press **Execute**. The results are saved to your project as `raw`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/dipy:1.1.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "dwi": "/path/to/DWI/dwi",
       "bvecs": "/path/to/DWI/bvecs",
       "bvals": "/path/to/DWI/bvals",
       "mask": "/path/to/mask/mask",
       "split_b_D": 400,
       "split_b_S0": 200,
       "b0_threshold": 0,
       "command": "dipy_fit_ivim"
   }
   ```

3. Run `./main`.

## Troubleshooting

- **invalid command: <command>**: Set command to dipy_fit_ivim.

## DIPY

- This is a Brainlife wrapper App stemming from the [`dipy_fit_ivim`](https://dipy.org/documentation/latest/reference_cmd/dipy_fit_ivim/) workflow.
- This single wrapper is exposed through an apps registered on [Brainlife.io](https://brainlife.io).
- More information about DIPY : [https://dipy.org/](https://dipy.org/).
- More information about the command line `dipy_fit_ivim`: [Command line Reference](https://dipy.org/documentation/latest/reference_cmd/dipy_fit_ivim/).

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Fit IVIM. brainlife.io App. [doi:10.25663/brainlife.app.322](https://doi.org/10.25663/brainlife.app.322)
- Garyfallidis E et al. Dipy, a library for the analysis of diffusion MRI data. Frontiers in Neuroinformatics 8:8 (2014). [doi:10.3389/fninf.2014.00008](https://doi.org/10.3389/fninf.2014.00008)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- Serge Koudoro
- Javier Ricardo Guaje Guerra

**Contributors**

- Soichi Hayashi

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io, which runs this App, is publicly funded by Wellcome, the U.S. National Institutes of Health and the U.S. National Science Foundation; acknowledging that support helps keep it running.</sub>

## License

See [LICENSE](LICENSE).
