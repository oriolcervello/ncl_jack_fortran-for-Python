# ncl_jack_fortran for Python

This is a compilation of the ncl_jack_fortran.f (Fortran subroutines used in NCL plotting of RASP 
(Regional Atmospheric Soaring Predictions) COMPUTER PROGRAM 
Original Creator: Dr. John W. (Jack) Glendening, Meteorologist (drjack@drjack.info)
Copyright 2005+  by John W. Glendening   All rights reserved.) to be used in Pyhton.

For more information about RASP and BLIPMAPs go to [drjack.info](http://www.drjack.info/ "drjack.info").

## Compilation

The library has been compiled for Python usage with 64-bit OS, with the following comand:

```
f2py3.6 -c -m ncl_jack_fortran ncl_jack_fortran.f
```

## Usage
The compilation have been done for Python 3.6, no tested for other versions but it may work.

Example:
```python
import ncl_jack_fortran

...

bparam = ncl_jack_fortran.calc_wblmaxmin(linfo,wa,z,ter,pblh)
```

If using [wrf-python](https://wrf-python.readthedocs.io/en/latest/index.html) is needed to traspose all matrix before sending them to the lib. For the original use with NCL the traspose was made automatically.

"For NCL arrays, the fastest-varying dimension is the rightmost, while for Fortran it is the leftmost dimension. Therefore, if XA is a Fortran array dimensioned idim x jdim, this array will be dimensioned jdim x idim in NCL." [More info.](https://www.ncl.ucar.edu/Document/Tools/WRAPIT.shtml)


```python
import numpy as np
import ncl_jack_fortran
from wrf import getvar

pblh = getvar(ncfile, "pblh")
ter = getvar(ncfile, "HGT")
wa = getvar(ncfile, "wa")
z = getvar(ncfile, "z")

pblh=np.transpose(pblh.values)
ter=np.transpose(ter.values)
wa=np.transpose(wa.values)
z=np.transpose(z.values)

...

bparam = ncl_jack_fortran.calc_wblmaxmin(linfo,wa,z,ter,pblh)
```


## Available functions

Available and tested with Python functions in the library.

```python
#*** FUNCTION TO CALCULATE W MAX/MIN IN BL (cm/sec) - linfo>0 returns height of Wmax/min
#***           LINFO 0=w[cm/s] 1=z[m] 2=z-zsfc[m] 3=(z-zsfc)/hbl[%]

bparam = calc_wblmaxmin(linfo,wa,z,ter,pblh,[isize,jsize,ksize])

Wrapper for ``calc_wblmaxmin``.

# Parameters
# ----------
linfo : input int
wa : input rank-3 array('f') with bounds (isize,jsize,ksize)
z : input rank-3 array('f') with bounds (isize,jsize,ksize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(wa,0)
jsize : input int, optional
    Default: shape(wa,1)
ksize : input int, optional
    Default: shape(wa,2)

# Returns
# -------
bparam : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO FIND LOWEST NON-ZERO CLOUD LEVEL IN BL
bparam = calc_blcloudbase(a,z,ter,pblh,cloudbasecriteria,valuemax,lagl,[isize,jsize,ksize])

Wrapper for ``calc_blcloudbase``.

# Parameters
# ----------
a : input rank-3 array('f') with bounds (isize,jsize,ksize)
z : input rank-3 array('f') with bounds (isize,jsize,ksize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)
cloudbasecriteria : input float
valuemax : input float
lagl : input int

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(a,0)
jsize : input int, optional
    Default: shape(a,1)
ksize : input int, optional
    Default: shape(a,2)

# Returns
# -------
bparam : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO CALCULATE BL-AVG  
bparam = calc_blavg(a,z,ter,pblh,[isize,jsize,ksize])

Wrapper for ``calc_blavg``.

# Parameters
# ----------
a : input rank-3 array('f') with bounds (isize,jsize,ksize)
z : input rank-3 array('f') with bounds (isize,jsize,ksize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(a,0)
jsize : input int, optional
    Default: shape(a,1)
ksize : input int, optional
    Default: shape(a,2)

# Returns
# -------
bparam : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO CALCULATE WIND AT BL TOP
ubltop,vbltop = calc_bltopwind(u,v,z,ter,pblh,[isize,jsize,ksize])

Wrapper for ``calc_bltopwind``.

# Parameters
# ----------
u : input rank-3 array('f') with bounds (isize,jsize,ksize)
v : input rank-3 array('f') with bounds (isize,jsize,ksize)
z : input rank-3 array('f') with bounds (isize,jsize,ksize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(u,0)
jsize : input int, optional
    Default: shape(u,1)
ksize : input int, optional
    Default: shape(u,2)

# Returns
# -------
ubltop : rank-2 array('f') with bounds (isize,jsize)
vbltop : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO CALCULATE MAX SUBGRID CLOUD COVER WITHIN BL (0-100%)
bparam = calc_subgrid_blcloudpct_grads(qvapor,qcloud,tc,pmb,z,ter,pblh,cwbasecriteria,[isize,jsize,ksize])

Wrapper for ``calc_subgrid_blcloudpct_grads``.

# Parameters
# ----------
qvapor : input rank-3 array('f') with bounds (isize,jsize,ksize)
qcloud : input rank-3 array('f') with bounds (isize,jsize,ksize)
tc : input rank-3 array('f') with bounds (isize,jsize,ksize)
pmb : input rank-3 array('f') with bounds (isize,jsize,ksize)
z : input rank-3 array('f') with bounds (isize,jsize,ksize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)
cwbasecriteria : input float

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(qvapor,0)
jsize : input int, optional
    Default: shape(qvapor,1)
ksize : input int, optional
    Default: shape(qvapor,2)

# Returns
# -------
bparam : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO CALCULATE WSTAR (in mks - convert to wfpm outside routine)
wstar = calc_wstar(hfx,pblh,ksize,[isize,jsize])

Wrapper for ``calc_wstar``.

# Parameters
# ----------
hfx : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)
ksize : input int

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(hfx,0)
jsize : input int, optional
    Default: shape(hfx,1)

# Returns
# -------
wstar : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO CALCULATE "CRITICAL HEIGHT" WHERE EST. W<225fpm
bparam = calc_hcrit(wstar,ter,pblh,[isize,jsize])

Wrapper for ``calc_hcrit``.

# Parameters
# ----------
wstar : input rank-2 array('f') with bounds (isize,jsize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(wstar,0)
jsize : input int, optional
    Default: shape(wstar,1)

# Returns
# -------
bparam : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO CALCULATE HEIGHT OF SFC.LCL
bparam = calc_sfclclheight(p,tc,tdc,z,ter,pblh,[isize,jsize,ksize])

Wrapper for ``calc_sfclclheight``.

# Parameters
# ----------
p : input rank-3 array('f') with bounds (isize,jsize,ksize)
tc : input rank-3 array('f') with bounds (isize,jsize,ksize)
tdc : input rank-3 array('f') with bounds (isize,jsize,ksize)
z : input rank-3 array('f') with bounds (isize,jsize,ksize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(p,0)
jsize : input int, optional
    Default: shape(p,1)
ksize : input int, optional
    Default: shape(p,2)

# Returns
# -------
bparam : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO CALCULATE HEIGHT OF BL.CL
bparam = calc_blclheight(pmb,tc,qvaporblavg,z,ter,pblh,[isize,jsize,ksize])

Wrapper for ``calc_blclheight``.

# Parameters
# ----------
pmb : input rank-3 array('f') with bounds (isize,jsize,ksize)
tc : input rank-3 array('f') with bounds (isize,jsize,ksize)
qvaporblavg : input rank-2 array('f') with bounds (isize,jsize)
z : input rank-3 array('f') with bounds (isize,jsize,ksize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(pmb,0)
jsize : input int, optional
    Default: shape(pmb,1)
ksize : input int, optional
    Default: shape(pmb,2)

# Returns
# -------
bparam : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO CALCULATE TEMPERATURE VARIABILITY AT BL TOP = HEIGHT WHERE POT.TEMP. 4degF WARMER THAN AT BL TOP
bparam = calc_bltop_pottemp_variability(theta,z,ter,pblh,criteriondegc,[isize,jsize,ksize])

Wrapper for ``calc_bltop_pottemp_variability``.

# Parameters
# ----------
theta : input rank-3 array('f') with bounds (isize,jsize,ksize)
z : input rank-3 array('f') with bounds (isize,jsize,ksize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)
criteriondegc : input float

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(theta,0)
jsize : input int, optional
    Default: shape(theta,1)
ksize : input int, optional
    Default: shape(theta,2)

# Returns
# -------
bparam : rank-2 array('f') with bounds (isize,jsize)
```
```python
#*** FUNCTION TO CALCULATE WIND DIFFERENCE ACROSS BL
bparam = calc_blwinddiff(u,v,z,ter,pblh,[isize,jsize,ksize])

Wrapper for ``calc_blwinddiff``.

# Parameters
# ----------
u : input rank-3 array('f') with bounds (isize,jsize,ksize)
v : input rank-3 array('f') with bounds (isize,jsize,ksize)
z : input rank-3 array('f') with bounds (isize,jsize,ksize)
ter : input rank-2 array('f') with bounds (isize,jsize)
pblh : input rank-2 array('f') with bounds (isize,jsize)

# Other Parameters
# ----------------
isize : input int, optional
    Default: shape(u,0)
jsize : input int, optional
    Default: shape(u,1)
ksize : input int, optional
    Default: shape(u,2)

# Returns
# -------
bparam : rank-2 array('f') with bounds (isize,jsize)
```

## Credit
Original Creator: Dr. John W. (Jack) Glendening.

ncl_jack_fortran for Python: Oriol Cervelló.
