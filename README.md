#Anaconda-Windows-AMD
optimized numpy, numexpr, scipy, scikit-learn for AMD CPU with patched Intel MKL+compiler

because Anacodna didn't provide "nomkl" package for Windows,

use `conda uninstall scikit-learn scipy numexpr numpy --force -y` to uninstall "cripple AMD" version and pip install patched package.

----

# Benchmark

https://github.com/IntelPython/ibench

AMD Ryzen Threadripper 1950X

## Anaconda3 5.0.0 stock
	python -m ibench run -b all --size small --runs 3 --file stock.out
	Cholesky:
	Cholesky:   N = 10000
	Cholesky:   elapsed 4.750731 gflops 70.164637
	Cholesky:   elapsed 4.797629 gflops 69.478766
	Cholesky:   elapsed 4.782000 gflops 69.705847
	Cholesky:   gflops 69.705847
	Det:
	Det:   N = 15000
	Det:   elapsed 21.612758 gflops 104.105176
	Det:   elapsed 20.128157 gflops 111.783706
	Det:   elapsed 20.237557 gflops 111.179428
	Det:   gflops 111.179428
	Dot:
	Dot:   N = 5000
	Dot:   elapsed 2.719163 gflops 91.940067
	Dot:   elapsed 2.547295 gflops 98.143330
	Dot:   elapsed 2.844185 gflops 87.898631
	Dot:   gflops 91.940067
	Fft:
	Fft:   N = 520000
	Fft:   elapsed 24.300705 gflops 2.031595
	Fft:   elapsed 25.769671 gflops 1.915787
	Fft:   elapsed 22.269129 gflops 2.216934
	Fft:   gflops 2.031595
	Inv:
	Inv:   N = 10000
	Inv:   elapsed 37.959076 gflops 52.688322
	Inv:   elapsed 37.318347 gflops 53.592942
	Inv:   elapsed 37.254794 gflops 53.684366
	Inv:   gflops 53.592942
	Lu:
	Lu:   N = 20000
	Lu:   elapsed 76.371366 gflops 69.834201
	Lu:   elapsed 76.887068 gflops 69.365804
	Lu:   elapsed 75.965055 gflops 70.207721
	Lu:   gflops 69.834201
	Qr:
	Qr:   N = 5000
	Qr:   elapsed 2.531648 gflops 65.833260
	Qr:   elapsed 2.437882 gflops 68.365362
	Qr:   elapsed 2.578530 gflops 64.636315
	Qr:   gflops 65.833260
	Svd:
	Svd:   N = 5000
	Svd:   elapsed 65.604034 gflops 2.540494
	Svd:   elapsed 65.213364 gflops 2.555713
	Svd:   elapsed 64.947696 gflops 2.566167
	Svd:   gflops 2.555713

## patched

OMP_NUM_THREADS=16

OMP_DYNAMIC=FALSE

KMP_AFFINITY=granularity=core,scatter

KMP_CPUINFO_FILE=%HOMEDRIVE%\%HOMEPATH%\cpuinfo.txt

	python -m ibench run -b all --size small --runs 3 --file patched.out
	Cholesky:
	Cholesky:   N = 10000
	Cholesky:   elapsed 2.766047 gflops 120.508929
	Cholesky:   elapsed 2.734804 gflops 121.885643
	Cholesky:   elapsed 2.734805 gflops 121.885611
	Cholesky:   gflops 121.885611
	Det:
	Det:   N = 15000
	Det:   elapsed 12.564355 gflops 179.078033
	Det:   elapsed 11.876862 gflops 189.443979
	Det:   elapsed 11.751847 gflops 191.459262
	Det:   gflops 189.443979
	Dot:
	Dot:   N = 5000
	Dot:   elapsed 1.203303 gflops 207.761453
	Dot:   elapsed 1.093918 gflops 228.536308
	Dot:   elapsed 1.078316 gflops 231.843042
	Dot:   gflops 228.536308
	Fft:
	Fft:   N = 520000
	Fft:   elapsed 21.878450 gflops 2.256522
	Fft:   elapsed 21.784669 gflops 2.266236
	Fft:   elapsed 21.799743 gflops 2.264669
	Fft:   gflops 2.264669
	Inv:
	Inv:   N = 10000
	Inv:   elapsed 13.189449 gflops 151.636356
	Inv:   elapsed 13.002043 gflops 153.821974
	Inv:   elapsed 12.939530 gflops 154.565115
	Inv:   gflops 153.821974
	Lu:
	Lu:   N = 20000
	Lu:   elapsed 52.617392 gflops 101.360655
	Lu:   elapsed 48.023288 gflops 111.057230
	Lu:   elapsed 47.522964 gflops 112.226447
	Lu:   gflops 111.057230
	Qr:
	Qr:   N = 5000
	Qr:   elapsed 1.984685 gflops 83.976385
	Qr:   elapsed 1.969060 gflops 84.642759
	Qr:   elapsed 2.406628 gflops 69.253180
	Qr:   gflops 83.976385
	Svd:
	Svd:   N = 5000
	Svd:   elapsed 61.072073 gflops 2.729016
	Svd:   elapsed 61.025206 gflops 2.731112
	Svd:   elapsed 60.806422 gflops 2.740939
	Svd:   gflops 2.731112
