# ncl_jack_fortran for Python

This is a compilation of the ncl_jack_fortran.f (Fortran subroutines used in NCL plotting of RASP 
(Regional Atmospheric Soaring Predictions) COMPUTER PROGRAM 
Original Creator: Dr. John W. (Jack) Glendening, Meteorologist (drjack@drjack.info)
Copyright 2005+  by John W. Glendening   All rights reserved.) to be used in Pyhton.

For more information about RASP and BLIPMAPs go to [drjack.info](http://www.drjack.info/ "drjack.info").

## Compilation

The library has been compiled with the following comand:

```
aaaaaaaaaaaa
```

## Usage
The compilation have been done for Python 3.6, no tested for other versions but it may work.
```python
aaaaaaaaaaaaaaa
```
## Available functions

Available functions in the library, not all of them has been tested with Python.

```python
	#*** FUNCTION TO CALCULATE W MAX/MIN IN BL (cm/sec) - linfo>0 returns height of Wmax/min
	#***           LINFO 0=w[cm/s] 1=z[m] 2=z-zsfc[m] 3=(z-zsfc)/hbl[%]

    calc_wblmaxmin( linfo, wa, z, ter, pblh, isize,jsize,ksize, bparam )
	 
	#*** FUNCTION TO FIND LOWEST NON-ZERO CLOUD LEVEL (ALL LEVELS)
    calc_cloudbase( a,z,ter, cloudbasecriteria, valuemax, lagl, isize,jsize,ksize, bparam )
	 
	#*** FUNCTION TO FIND LOWEST NON-ZERO CLOUD LEVEL IN BL
	calc_blcloudbase( a,z, ter,pblh,
     &       cloudbasecriteria, valuemax,
     &       lagl, isize,jsize,ksize, bparam )
	 
	#*** FUNCTION TO CALCULATE HEIGHT OF SFC.LCL
	calc_sfclclheight( p,tc,tdc,z,ter,pblh,
     &         isize,jsize,ksize, bparam )
	 
	#*** FUNCTION TO CALCULATE HEIGHT OF BL.CL
	calc_blclheight( pmb,tc,qvaporblavg, z,ter,pblh,
     &         isize,jsize,ksize, bparam )
	
	#*** FUNCTION TO CALCULATE BL-AVG  
	calc_blavg( a, z, ter, pblh, 
     &         isize,jsize,ksize, bparam )
	 	 
	#*** FUNCTION TO CALCULATE WSTAR (in mks - convert to wfpm outside routine)
	calc_wstar( hfx, pblh,
     &         isize,jsize,ksize, wstar )
	 	 	 
	#*** FUNCTION TO CALCULATE MAX IN BL at mass point
	calc_blmax( a,z,ter,pblh, 
     &         isize,jsize,ksize, bparam )
	 	 
	#*** FUNCTION TO CALCULATE "CRITICAL HEIGHT" WHERE EST. W<225fpm
	calc_hcrit( wstar,ter,pblh,
     &         isize,jsize, bparam )
	 	 
	#*** FUNCTION TO CALCULATE "CRITICAL HEIGHT" WHERE EST. WCRIT IS INPUT (fpm)
	calc_hlift( wcritfpm, wstar,ter,pblh,
     &         isize,jsize, bparam )
	 
	#*** FUNCTION TO CALCULATE MAX IN CHOSEN 3D BOX
	find_boxmax3d( a, ibox1in,ibox2in,jbox1in,
     &                             jbox2in,kbox1in,kbox2in,
     &         isize,jsize,ksize, amax,imaxout,jmaxout,kmaxout )
	 
	#*** FUNCTION TO LIMIT MAX FOR ARRAY
	maxlimit2d( adata, upperlimit,
     &         isize,jsize )
	 	 
	#*** FUNCTION TO LIMIT MIN FOR ARRAY
	minlimit2d( adata, lowerlimit,
     &         isize,jsize )
	 	 	 
	#*** FUNCTION TO INTEGRATE MIXING RATIO WITHIN BL  (mass-based)
	calc_blinteg_mixratio( a, ptot, psfc, z, ter, pblh,
     &         isize,jsize,ksize, bparam )
	 
	#*** FUNCTION TO INTEGRATE MIXING RATIO *ABOVE* BL  (mass-based)
	calc_aboveblinteg_mixratio( a, ptot, z, ter, pblh,
     &         isize,jsize,ksize, bparam )
	 
	#*** FUNCTION TO CALCULATE BL CLOUD-PRODUCTION EQUIV. HEAT FLUX  (based on z avg, not mass avg)
	calc_qcblhf( a,totmu, z, ter, pblh, 
     &         isize,jsize,ksize, bparam )
	 
	#*** FUNCTION TO OUTPUT DATA FILE FOR SINGLE PARAMETER - input array is REAL - lformat= decimal places (0=>INTEGER)
    output_mapdatafile( qfilename, qtitle1,qtitle2,qtitle3,
     &                               amap, NNX,NNY, lformat )
	 
	#*** FUNCTION TO CALCULATE TEMPERATURE VARIABILITY AT BL TOP = HEIGHT WHERE POT.TEMP. 4degF WARMER THAN AT BL TOP
    calc_bltop_pottemp_variability( theta, z, ter, pblh,
     &         isize,jsize,ksize, criteriondegc, bparam )
	 	 
	#*** FUNCTION TO CALCULATE WIND DIFFERENCE ACROSS BL
	calc_blwinddiff( u, v, z, ter, pblh, 
     &         isize,jsize,ksize, bparam )
	 	 
	#*** FUNCTION TO CALCULATE WIND AT BL TOP
	calc_bltopwind( u, v, z, ter, pblh, 
     &         isize,jsize,ksize, ubltop,vbltop )
	 	 
	#*** FUNCTION TO CALCULATE RELATIVE HUMIDITY FOR SINGLE GRIDPT
	calc_rh1 ( qv, pmb, tc, rh )
		   		   		   
    #*** FUNCTION TO TRUNCATE ANY ARRAY VALUES BELOW SPECIFIED MINIMUM
    trunc_2darray_min ( a, NNX,NNY, amin )
      
    #*** FUNCTION TO TRUNCATE ANY ARRAY VALUES ABOVE SPECIFIED MAXIMUM
    trunc_2darray_max ( a, NNX,NNY, amax )
		 
	#*** FUNCTION TO CALCULATE MAX SUBGRID CLOUD COVER WITHIN BL (0-100%)
	calc_subgrid_blcloudpct_grads(
     &         qvapor, qcloud, tc,pmb, z,
     &         ter, pblh, cwbasecriteria,
     &         isize,jsize,ksize, bparam )
	 
	#*** FUNCTION TO CALCULATE MAX SUBGRID CLOUD COVER WITHIN BL (0-100%)
	calc_subgrid_blcloudpct_gfdleta(
     &         qvapor, qcloud, tc,pmb, z,
     &         ter, pblh, gridspacing,
     &         isize,jsize,ksize, bparam )
	 	 
	#*** FUNCTION TO READ BLIP ARAY SIZE FROM DATA FILE
	read_blip_data_size( qfilename, NNX,NNY )
		   		   
	#*** FUNCTION TO READ BLIP ARAY SIZE AND PROJECTION DATA FROM DATA FILE
	read_blip_data_info( qfilename,NNX,NNY,
     &  qprojection,dx,dy,plat1,plat2,plon,alat0,alon0 )
	 
	#*** FUNCTION TO READ BLIP DATA FILE FOR SINGLE PARAMETER - output array is REAL
	subroutine read_blip_datafile( qfilename, NNX,NNY, adata, qid )
	 
	#***  REPLACE U,V VELOCITY COMPONENTS (grid coords) TO DIRECTION(true),SPEED
	uv2wdws_4latlon(u,v, alat,alon, nx,ny, projlat,projlon)
		   
	#** REPLACE WIND DIRECTION(true),SPEED BY VELOCITY COMPONENTS (grid coords)
	wdws2uv_4latlon( wd,ws, alat,alon, nx,ny, 
     &                   qprojection,projlat,projlon )
	 
	#** CALC LAT/LONS FOR ARRAY using indexs relative to grid center
	calc_latlon( NNX,NNY, dx,dy,
     & projlat1,projlat2,projlon,centlat,centlon, alat,alon )
	 
	#*** FUNCTION TO NORMALIZE INPUT SFC SOLAR RAD BY CLOUDLESS SFC SOLAR RAD
	calc_sfcsunpct( jday,gmthr, alat,alon,ter,
     &            z,pmb,tc,qvapor, isize,jsize,ksize, bparam ) 
	 
```
