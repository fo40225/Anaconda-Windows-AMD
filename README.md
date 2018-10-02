# Anaconda-Windows-AMD
optimized numpy, numexpr, scipy, scikit-learn for AMD CPU with patched Intel MKL+compiler

because Anacodna didn't provide "nomkl" package for Windows,

use `conda uninstall scikit-learn scipy numexpr numpy numpy-base --force -y` to uninstall "cripple AMD" version and pip install patched package.

----

# Benchmark

https://github.com/IntelPython/ibench

``` bash
git clone --no-checkout https://github.com/IntelPython/ibench.git
cd ibench
git checkout d2a81d04352427437e6e383654cfbd36e99c5ae9
```

## AMD Ryzen Threadripper 1950X / DDR4-3000 16GB x8

### Anaconda3 5.3.0 stock
	python -m ibench run -b all --size small --runs 3 --file stock.out
	Cholesky:
	Cholesky:   N = 10000
	Cholesky:   elapsed 2.452964 gflops 135.890032
	Cholesky:   elapsed 2.406248 gflops 138.528248
	Cholesky:   elapsed 2.375005 gflops 140.350553
	Cholesky:   gflops 138.528248
	Det:
	Det:   N = 15000
	Det:   elapsed 14.999864 gflops 150.001357
	Det:   elapsed 14.687488 gflops 153.191611
	Det:   elapsed 15.187511 gflops 148.148039
	Det:   gflops 150.001357
	Dot:
	Dot:   N = 5000
	Dot:   elapsed 1.671851 gflops 149.534821
	Dot:   elapsed 1.796890 gflops 139.129290
	Dot:   elapsed 1.687488 gflops 148.149216
	Dot:   gflops 148.149216
	Fft:
	Fft:   N = 520000
	Fft:   elapsed 17.312503 gflops 2.851650
	Fft:   elapsed 17.859395 gflops 2.764326
	Fft:   elapsed 17.968908 gflops 2.747479
	Fft:   gflops 2.764326
	Inv:
	Inv:   N = 10000
	Inv:   elapsed 27.281224 gflops 73.310494
	Inv:   elapsed 27.906256 gflops 71.668518
	Inv:   elapsed 28.312495 gflops 70.640190
	Inv:   gflops 71.668518
	Lu:
	Lu:   N = 20000
	Lu:   elapsed 42.062671 gflops 126.794928
	Lu:   elapsed 42.406072 gflops 125.768151
	Lu:   elapsed 42.171893 gflops 126.466540
	Lu:   gflops 126.466540
	Qr:
	Qr:   N = 5000
	Qr:   elapsed 2.671874 gflops 62.378195
	Qr:   elapsed 2.562487 gflops 65.040971
	Qr:   elapsed 2.531252 gflops 65.843559
	Qr:   gflops 65.040971
	Svd:
	Svd:   N = 5000
	Svd:   elapsed 23.796755 gflops 7.003756
	Svd:   elapsed 24.046863 gflops 6.930911
	Svd:   elapsed 24.109386 gflops 6.912937
	Svd:   gflops 6.930911

### Anaconda3 5.3.0 patched

```
SET KMP_AFFINITY=granularity=core,compact,1,0
SET KMP_CPUINFO_FILE=cpuinfo.txt
SET MKL_NUM_THREADS=16
SET OMP_NUM_THREADS=16
```

	python -m ibench run -b all --size small --runs 3 --file patched.out
	Cholesky:
	Cholesky:   N = 10000
	Cholesky:   elapsed 1.077014 gflops 309.497756
	Cholesky:   elapsed 1.060764 gflops 314.238968
	Cholesky:   elapsed 1.038576 gflops 320.952313
	Cholesky:   gflops 314.238968
	Det:
	Det:   N = 15000
	Det:   elapsed 5.932113 gflops 379.291513
	Det:   elapsed 5.878459 gflops 382.753388
	Det:   elapsed 5.869332 gflops 383.348560
	Det:   gflops 382.753388
	Dot:
	Dot:   N = 5000
	Dot:   elapsed 0.681815 gflops 366.668170
	Dot:   elapsed 0.651215 gflops 383.897605
	Dot:   elapsed 0.677767 gflops 368.858433
	Dot:   gflops 368.858433
	Fft:
	Fft:   N = 520000
	Fft:   elapsed 17.159977 gflops 2.876997
	Fft:   elapsed 17.064160 gflops 2.893151
	Fft:   elapsed 17.137996 gflops 2.880687
	Fft:   gflops 2.880687
	Inv:
	Inv:   N = 10000
	Inv:   elapsed 7.979070 gflops 250.655780
	Inv:   elapsed 7.922433 gflops 252.447712
	Inv:   elapsed 7.961345 gflops 251.213835
	Inv:   gflops 251.213835
	Lu:
	Lu:   N = 20000
	Lu:   elapsed 19.155079 gflops 278.429206
	Lu:   elapsed 19.042639 gflops 280.073226
	Lu:   elapsed 19.200626 gflops 277.768716
	Lu:   gflops 278.429206
	Qr:
	Qr:   N = 5000
	Qr:   elapsed 1.905688 gflops 87.457465
	Qr:   elapsed 1.884816 gflops 88.425965
	Qr:   elapsed 1.818387 gflops 91.656322
	Qr:   gflops 88.425965
	Svd:
	Svd:   N = 5000
	Svd:   elapsed 17.913329 gflops 9.304059
	Svd:   elapsed 18.530348 gflops 8.994254
	Svd:   elapsed 18.548804 gflops 8.985305
	Svd:   gflops 8.994254

## i7 8700

### Anaconda3 5.3.0 stock

	python -m ibench run -b all --size small --runs 3 --file stock.out
	Cholesky:
	Cholesky:   N = 10000
	Cholesky:   elapsed 1.218446 gflops 273.572562
	Cholesky:   elapsed 1.256650 gflops 265.255564
	Cholesky:   elapsed 1.261148 gflops 264.309454
	Cholesky:   gflops 265.255564
	Det:
	Det:   N = 15000
	Det:   elapsed 9.779099 gflops 230.082547
	Det:   elapsed 9.709930 gflops 231.721537
	Det:   elapsed 10.945049 gflops 205.572400
	Det:   gflops 230.082547
	Dot:
	Dot:   N = 5000
	Dot:   elapsed 1.124725 gflops 222.276583
	Dot:   elapsed 1.249702 gflops 200.047695
	Dot:   elapsed 1.234089 gflops 202.578521
	Dot:   gflops 202.578521
	Fft:
	Fft:   N = 520000
	Fft:   elapsed 11.457346 gflops 4.308956
	Fft:   elapsed 11.562778 gflops 4.269666
	Fft:   elapsed 11.481678 gflops 4.299824
	Fft:   gflops 4.299824
	Inv:
	Inv:   N = 10000
	Inv:   elapsed 9.040725 gflops 221.221185
	Inv:   elapsed 10.287056 gflops 194.419084
	Inv:   elapsed 10.661030 gflops 187.599142
	Inv:   gflops 194.419084
	Lu:
	Lu:   N = 20000
	Lu:   elapsed 30.562632 gflops 174.505041
	Lu:   elapsed 31.136132 gflops 171.290811
	Lu:   elapsed 30.551234 gflops 174.570146
	Lu:   gflops 174.505041
	Qr:
	Qr:   N = 5000
	Qr:   elapsed 1.468397 gflops 113.502483
	Qr:   elapsed 1.446315 gflops 115.235382
	Qr:   elapsed 1.593857 gflops 104.568155
	Qr:   gflops 113.502483
	Svd:
	Svd:   N = 5000
	Svd:   elapsed 28.396710 gflops 5.869225
	Svd:   elapsed 28.365670 gflops 5.875647
	Svd:   elapsed 28.302233 gflops 5.888817
	Svd:   gflops 5.875647
