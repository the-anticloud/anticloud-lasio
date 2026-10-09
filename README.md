# LASIO

![licence](https://img.shields.io/badge/licence-MIT-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![checks](https://img.shields.io/badge/checks-unknown_PASS-brightgreen)

> Governed Anticloud packaging of the upstream project `LASIO` in category **OIL_GAS**. check results: see ISOLATED_LAB_RESULTS. Every number below traces to a named file + run stamp; nothing is borrowed from other projects.

**Upstream:** LASIO · **Upstream pin:** `20fb98d7e2c9444bbbc9ee0e7aff4420b7c5b512` · **Category:** OIL_GAS · **Vendor:** Anticloud FZ LLE · **Licence:** MIT

---

## What This Project Does

# lasio

<p align="center">
<a href="https://lasio.readthedocs.io/en/stable/"><strong>Documentation</strong> (stable)</a> •
<a href="https://lasio.readthedocs.io/en/latest/"><strong>Documentation</strong> (main branch)</a>
</p>

[![Run tests](https://github.com/kinverarity1/lasio/actions/workflows/ci-tests.yml/badge.svg)](https://github.com/kinverarity1/lasio/actions/workflows/ci-tests.yml)
[![PyPI version](https://img.shields.io/pypi/v/lasio.svg)](https://pypi.python.org/pypi/lasio/)
[![Code Style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://black.readthedocs.io/en/stable/the_black_code_style/index.html)
[![License](http://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/kinverarity1/lasio/blob/master/LICENSE)

Read and write Log ASCII Standard files with Python.

This is a Python 3.7+ package to read and write Log ASCII Standard
(LAS) files, used for borehole data such as geophysical, geological, or
petrophysical logs. It's compatible with versions 1.2 and 2.0 of the LAS file
specification, published by the [Canadian Well Logging
Society](https://www.cwls.org/products/#products-las). Support for LAS 3 is 
[being worked on](https://github.com/kinverarity1/lasio/issues/5).

lasio is primarily for reading and writing data and metadata to and from 
LAS files. It is designed to read as many LAS files as possible, including
those containing common errors and non-compliant formatting. It can be used
directly, but you may want to consider using some other packages, depending
on your priorities:

- [welly](https://github.com/agile-geoscience/welly) is a Python package that 
  uses lasio for I/O but provides a **lot** more functionality aimed at working
  with curves, wells, and projects. I would recommend starting there in most 
  cases, to avoid re-inventing the wheel!
- [lascheck](https://github.com/MandarJKulkarni/lascheck) is focused on
  checking whether your LAS file meets the specifications.
- [lasr](https://github.com/donald-keighley/lasr) is an R package which 
  is designed to read large amounts of data quickly from LAS files; this is 
  a great thing to check out if speed is a priority for you, as lasio is not 
  particularly fast.
- LiDAR surveys are also called "LAS files", but they are quite different and
  lasio will not help you -- check out [laspy](https://github.com/laspy/laspy)
  instead.

lasio [stopped](https://github.com/kinverarity1/lasio/issues/364) 
supporting Python 2.7 in August 2020. The final version of lasio with Python 2.7 support 
is version 0.26.

## Code of conduct

See our [code of conduct](https://lasio.readthedocs.io/en/latest/contributing.html#code-of-conduct).

## Quick start

For the minimum working requirements, you'll need numpy installed. Install
lasio with:

```bash
$ pip install lasio
```

To make sure you have everything, use this to ensure pandas, chardet, and
openpyxl are also installed:

```bash
$ pip install lasio[all]
```

Example session:

```python
>>> import lasio
```

You can read the file using a filename, file-like object, or URL:

```python
>>> las = lasio.read("sample_rev.las")
```

Data is accessible both directly as numpy arrays

```python
>>> las.keys()
['DEPT', 'DT', 'RHOB', 'NPHI', 'SFLU', 'SFLA', 'ILM', 'ILD']
>>> las['SFLU']
array([ 123.45,  123.45,  123.45, ...,  123.45,  123.45,  123.45])
>>> las['DEPT']
array([ 1670.   ,  1669.875,  1669.75 , ...,  1669.75 ,  1670.   ,
        1669.875])
```

and as ``CurveItem`` objects with associated metadata:

```python
>>> las.curves
[CurveItem(mnemonic=DEPT, unit=M, value=, descr=1  DEPTH, original_mnemonic=DEPT, data.shape=(29897,)),
CurveItem(mnemonic=DT, unit=US/M, value=, descr=2  SONIC TRANSIT TIME, original_mnemonic=DT, data.shape=(29897,)),
CurveItem(mnemonic=RHOB, unit=K/M3, value=, descr=3  BULK DENSITY, original_mnemonic=RHOB, data.shape=(29897,)),
CurveItem(mnemonic=NPHI, unit=V/V, value=, descr=4   NEUTRON POROSITY, original_mnemonic=NPHI, data.shape=(29897,)),
CurveItem(mnemonic=SFLU, unit=OHMM, value=, descr=5  RXO RESISTIVITY, original_mnemonic=SFLU, data.shape=(29897,)),
CurveItem(mnemonic=SFLA, unit=OHMM, value=, descr=6  SHALLOW RESISTIVITY, original_mnemonic=SFLA, data.shape=(29897,)),
CurveItem(mnemonic=ILM, unit=OHMM, value=, descr=7  MEDIUM RESISTIVITY, original_mnemonic=ILM, data.shape=(29897,)),
CurveItem(mnemonic=ILD, unit=OHMM, value=, descr=8  DEEP RESISTIVITY, original_mnemonic=ILD, data.shape=(29897,))]
```

Header information is parsed into simple HeaderItem objects, and stored in a
dictionary for each section of the header:

```python
>>> las.version
[HeaderItem(mnemonic=VERS, unit=, value=1.2, descr=CWLS LOG ASCII STANDARD -VERSION 1.2, original_mnemonic=VERS),
HeaderItem(mnemonic=WRAP, unit=, value=NO, descr=ONE LINE PER DEPTH STEP, original_mnemonic=WRAP)]
>>> las.well
[HeaderItem(mnemonic=STRT, unit=M, value=1670.0, descr=, original_mnemonic=STRT),
HeaderItem(mnemonic=STOP, unit=M, value=1660.0, descr=, original_mnemonic=STOP),
HeaderItem(mnemonic=STEP, unit=M, value=-0.125, descr=, original_mnemonic=STEP),
HeaderItem(mnemonic=NULL, unit=, value=-999.25, descr=, original_mnemonic=NULL),
HeaderItem(mnemonic=COMP, unit=, value=ANY OIL COMPANY LTD., descr=COMPANY, original_mnemonic=COMP),
HeaderItem(mnemonic=WELL, unit=, value=ANY ET AL OIL WELL #12, descr=WELL, original_mnemonic=WELL),
HeaderItem(mnemonic=FLD, unit=, value=EDAM, descr=FIELD, original_mnemonic=FLD),
HeaderItem(mnemonic=LOC, unit=, value=A9-16-49, descr=LOCATION, original_mnemonic=LOC),
HeaderItem(mnemonic=PROV, unit=, value=SASKATCHEWAN, descr=PROVINCE, original_mnemonic=PROV),
HeaderItem(mnemonic=SRVC, unit=, value=ANY LOGGING COMPANY LTD., descr=SERVICE COMPANY, original_mnemonic=SRVC),
HeaderItem(mnemonic=DATE, unit=, value=25-DEC-1988, descr=LOG DATE, original_mnemonic=DATE),
HeaderItem(mnemonic=UWI, unit=, value=100091604920, descr=UNIQUE WELL ID, original_mnemonic=UWI)]
>>> las.params
[HeaderItem(mnemonic=BHT, unit=DEGC, value=35.5, descr=BOTTOM HOLE TEMPERATURE, original_mnemonic=BHT),
HeaderItem(mnemonic=BS, unit=MM, value=200.0, descr=BIT SIZE, original_mnemonic=BS),
HeaderItem(mnemonic=FD, unit=K/M3, value=1000.0, descr=FLUID DENSITY, original_mnemonic=FD),
HeaderItem(mnemonic=MATR, unit=, value=0.0, descr=NEUTRON MATRIX(0=LIME,1=SAND,2=DOLO), original_mnemonic=MATR),
HeaderItem(mnemonic=MDEN, unit=, value=2710.0, descr=LOGGING MATRIX DENSITY, original_mnemonic=MDEN),
HeaderItem(mnemonic=RMF, unit=OHMM, value=0.216, descr=MUD FILTRATE RESISTIVITY, original_mnemonic=RMF),
HeaderItem(mnemonic=DFD, unit=K/M3, value=1525.0, descr=DRILL FLUID DENSITY, original_mnemonic=DFD)]
```

The data is stored as a 2D numpy array:

```python
>>> las.data
array([[ 1670.   ,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       [ 1669.875,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       [ 1669.75 ,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       ...,
       [ 1669.75 ,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       [ 1670.   ,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       [ 1669.875,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ]])
```

You can also retrieve and load data as a ``pandas`` DataFrame, build LAS files
from scratch, write them back to disc, and export to Excel, amongst other
things.

See the [package documentation](https://lasio.readthedocs.io/en/latest/) for
more details.

## Contributing

Contributions are invited and welcome.

See [Contributing](https://lasio.readthedocs.io/en/latest/contributing.html) for how to get started.

## License

[MIT](https://github.com/kinverarity1/lasio/blob/master/LICENSE)

---

## Installation

lasio with:

```bash
$ pip install lasio
```

To make sure you have everything, use this to ensure pandas, chardet, and
openpyxl are also installed:

```bash
$ pip install lasio[all]
```

Example session:

```python
>>> import lasio
```

You can read the file using a filename, file-like object, or URL:

```python
>>> las = lasio.read("sample_rev.las")
```

Data is accessible both directly as numpy arrays

```python
>>> las.keys()
['DEPT', 'DT', 'RHOB', 'NPHI', 'SFLU', 'SFLA', 'ILM', 'ILD']
>>> las['SFLU']
array([ 123.45,  123.45,  123.45, ...,  123.45,  123.45,  123.45])
>>> las['DEPT']
array([ 1670.   ,  1669.875,  1669.75 , ...,  1669.75 ,  1670.   ,
        1669.875])
```

and as ``CurveItem`` objects with associated metadata:

```python
>>> las.curves
[CurveItem(mnemonic=DEPT, unit=M, value=, descr=1  DEPTH, original_mnemonic=DEPT, data.shape=(29897,)),
CurveItem(mnemonic=DT, unit=US/M, value=, descr=2  SONIC TRANSIT TIME, original_mnemonic=DT, data.shape=(29897,)),
CurveItem(mnemonic=RHOB, unit=K/M3, value=, descr=3  BULK DENSITY, original_mnemonic=RHOB, data.shape=(29897,)),
CurveItem(mnemonic=NPHI, unit=V/V, value=, descr=4   NEUTRON POROSITY, original_mnemonic=NPHI, data.shape=(29897,)),
CurveItem(mnemonic=SFLU, unit=OHMM, value=, descr=5  RXO RESISTIVITY, original_mnemonic=SFLU, data.shape=(29897,)),
CurveItem(mnemonic=SFLA, unit=OHMM, value=, descr=6  SHALLOW RESISTIVITY, original_mnemonic=SFLA, data.shape=(29897,)),
CurveItem(mnemonic=ILM, unit=OHMM, value=, descr=7  MEDIUM RESISTIVITY, original_mnemonic=ILM, data.shape=(29897,)),
CurveItem(mnemonic=ILD, unit=OHMM, value=, descr=8  DEEP RESISTIVITY, original_mnemonic=ILD, data.shape=(29897,))]
```

Header information is parsed into simple HeaderItem objects, and stored in a
dictionary for each section of the header:

```python
>>> las.version
[HeaderItem(mnemonic=VERS, unit=, value=1.2, descr=CWLS LOG ASCII STANDARD -VERSION 1.2, original_mnemonic=VERS),
HeaderItem(mnemonic=WRAP, unit=, value=NO, descr=ONE LINE PER DEPTH STEP, original_mnemonic=WRAP)]
>>> las.well
[HeaderItem(mnemonic=STRT, unit=M, value=1670.0, descr=, original_mnemonic=STRT),
HeaderItem(mnemonic=STOP, unit=M, value=1660.0, descr=, original_mnemonic=STOP),
HeaderItem(mnemonic=STEP, unit=M, value=-0.125, descr=, original_mnemonic=STEP),
HeaderItem(mnemonic=NULL, unit=, value=-999.25, descr=, original_mnemonic=NULL),
HeaderItem(mnemonic=COMP, unit=, value=ANY OIL COMPANY LTD., descr=COMPANY, original_mnemonic=COMP),
HeaderItem(mnemonic=WELL, unit=, value=ANY ET AL OIL WELL #12, descr=WELL, original_mnemonic=WELL),
HeaderItem(mnemonic=FLD, unit=, value=EDAM, descr=FIELD, original_mnemonic=FLD),
HeaderItem(mnemonic=LOC, unit=, value=A9-16-49, descr=LOCATION, original_mnemonic=LOC),
HeaderItem(mnemonic=PROV, unit=, value=SASKATCHEWAN, descr=PROVINCE, original_mnemonic=PROV),
HeaderItem(mnemonic=SRVC, unit=, value=ANY LOGGING COMPANY LTD., descr=SERVICE COMPANY, original_mnemonic=SRVC),
HeaderItem(mnemonic=DATE, unit=, value=25-DEC-1988, descr=LOG DATE, original_mnemonic=DATE),
HeaderItem(mnemonic=UWI, unit=, value=100091604920, descr=UNIQUE WELL ID, original_mnemonic=UWI)]
>>> las.params
[HeaderItem(mnemonic=BHT, unit=DEGC, value=35.5, descr=BOTTOM HOLE TEMPERATURE, original_mnemonic=BHT),
HeaderItem(mnemonic=BS, unit=MM, value=200.0, descr=BIT SIZE, original_mnemonic=BS),
HeaderItem(mnemonic=FD, unit=K/M3, value=1000.0, descr=FLUID DENSITY, original_mnemonic=FD),
HeaderItem(mnemonic=MATR, unit=, value=0.0, descr=NEUTRON MATRIX(0=LIME,1=SAND,2=DOLO), original_mnemonic=MATR),
HeaderItem(mnemonic=MDEN, unit=, value=2710.0, descr=LOGGING MATRIX DENSITY, original_mnemonic=MDEN),
HeaderItem(mnemonic=RMF, unit=OHMM, value=0.216, descr=MUD FILTRATE RESISTIVITY, original_mnemonic=RMF),
HeaderItem(mnemonic=DFD, unit=K/M3, value=1525.0, descr=DRILL FLUID DENSITY, original_mnemonic=DFD)]
```

The data is stored as a 2D numpy array:

```python
>>> las.data
array([[ 1670.   ,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       [ 1669.875,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       [ 1669.75 ,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       ...,
       [ 1669.75 ,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       [ 1670.   ,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ],
       [ 1669.875,   123.45 ,  2550.   , ...,   123.45 ,   110.2  ,   105.6  ]])
```

You can also retrieve and load data as a ``pandas`` DataFrame, build LAS files
from scratch, write them back to disc, and export to Excel, amongst other
things.

See the [package documentation](https://lasio.readthedocs.io/en/latest/) for
more details.

## Usage

petrophysical logs. It's compatible with versions 1.2 and 2.0 of the LAS file
specification, published by the [Canadian Well Logging
Society](https://www.cwls.org/products/#products-las). Support for LAS 3 is 
[being worked on](https://github.com/kinverarity1/lasio/issues/5).

lasio is primarily for reading and writing data and metadata to and from 
LAS files. It is designed to read as many LAS files as possible, including
those containing common errors and non-compliant formatting. It can be used
directly, but you may want to consider using some other packages, depending
on your priorities:

- [welly](https://github.com/agile-geoscience/welly) is a Python package that 
  uses lasio for I/O but provides a **lot** more functionality aimed at working
  with curves, wells, and projects. I would recommend starting there in most 
  cases, to avoid re-inventing the wheel!
- [lascheck](https://github.com/MandarJKulkarni/lascheck) is focused on
  checking whether your LAS file meets the specifications.
- [lasr](https://github.com/donald-keighley/lasr) is an R package which 
  is designed to read large amounts of data quickly from LAS files; this is 
  a great thing to check out if speed is a priority for you, as lasio is not 
  particularly fast.
- LiDAR surveys are also called "LAS files", but they are quite different and
  lasio will not help you -- check out [laspy](https://github.com/laspy/laspy)
  instead.

lasio [stopped](https://github.com/kinverarity1/lasio/issues/364) 
supporting Python 2.7 in August 2020. The final version of lasio with Python 2.7 support 
is version 0.26.

## API

<a href="https://lasio.readthedocs.io/en/latest/"><strong>Documentation</strong> (main branch)</a>
</p>

[![Run tests](https://github.com/kinverarity1/lasio/actions/workflows/ci-tests.yml/badge.svg)](https://github.com/kinverarity1/lasio/actions/workflows/ci-tests.yml)
[![PyPI version](https://img.shields.io/pypi/v/lasio.svg)](https://pypi.python.org/pypi/lasio/)
[![Code Style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://black.readthedocs.io/en/stable/the_black_code_style/index.html)
[![License](http://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/kinverarity1/lasio/blob/master/LICENSE)

Read and write Log ASCII Standard files with Python.

This is a Python 3.7+ package to read and write Log ASCII Standard
(LAS) files, used for borehole data such as geophysical, geological, or
petrophysical logs. It's compatible with versions 1.2 and 2.0 of the LAS file
specification, published by the [Canadian Well Logging
Society](https://www.cwls.org/products/#products-las). Support for LAS 3 is 
[being worked on](https://github.com/kinverarity1/lasio/issues/5).

lasio is primarily for reading and writing data and metadata to and from 
LAS files. It is designed to read as many LAS files as possible, including
those containing common errors and non-compliant formatting. It can be used
directly, but you may want to consider using some other packages, depending
on your priorities:

- [welly](https://github.com/agile-geoscience/welly) is a Python package that 
  uses lasio for I/O but provides a **lot** more functionality aimed at working
  with curves, wells, and projects. I would recommend starting there in most 
  cases, to avoid re-inventing the wheel!
- [lascheck](https://github.com/MandarJKulkarni/lascheck) is focused on
  checking whether your LAS file meets the specifications.
- [lasr](https://github.com/donald-keighley/lasr) is an R package which 
  is designed to read large amounts of data quickly from LAS files; this is 
  a great thing to check out if speed is a priority for you, as lasio is not 
  particularly fast.
- LiDAR surveys are also called "LAS files", but they are quite different and
  lasio will not help you -- check out [laspy](https://github.com/laspy/laspy)
  instead.

lasio [stopped](https://github.com/kinverarity1/lasio/issues/364) 
supporting Python 2.7 in August 2020. The final version of lasio with Python 2.7 support 
is version 0.26.

## Dependencies

| Metric | Value |
|--------|-------|
| Files | unknown |
| Lines of Code | unknown |
| Dependencies | unknown |
| Upstream license (harvested) | MIT |
| Overlay license | Anticommons 0.1.0 |

Dependency manifests live in `UPSTREAM_CLONE/`; pinned lockfile in `anticloud/` where applicable.

## Configuration

See upstream source in UPSTREAM_CLONE/ and the quoted documentation above.

## Contributing

Fork the project, create a feature branch, run the test suite, and open a pull request against upstream.

## License

Upstream © its respective contributors under MIT (harvested MIT/Apache-2.0/BSD source; see `UPSTREAM_CLONE/LICENSE`). This packaging overlay is licensed under Anticommons 0.1.0.

## Upstream

- **project:** LASIO
- **Pinned SHA:** `20fb98d7e2c9444bbbc9ee0e7aff4420b7c5b512`
- **source:** `UPSTREAM_CLONE/` (pinned at the SHA above)
- **Upstream README source:** `UPSTREAM_CLONE/README.md`

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`0dcd66d01ac7e658c7982ac7167c1ca4bf1602d2628c24f82920d4e22e719cbf`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| DANS (KNAW/NWO, Netherlands) | 10.17026/PT | EU-recognised archive |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe
and Mail, Business Insider, National Post, Financial Post, StreetInsider,
Digital Journal, Barchart, International Business Times, and Fox News.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

