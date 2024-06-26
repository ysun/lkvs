## Features Supported

Below are the test cases for new features on the Intel EMR platform in OpenEuler (referred to as OE) OS. Please note that the specific test content for each feature can be found in the relevant content under the BM directory, which will not be repeated here. We believe that these test cases are a subset of all related feature tests there.

[TODO feature list]
* tests-dsa

Tested with [OpenEuler 24.03 LTS](https://www.openeuler.org/zh/download/?version=openEuler%2024.03%20LTS)

## Dependencies
### tests-topology
* hwloc.x86_64 package
```
yum install hwloc
```

* cpuid tool

### tests-sdsi
* intel_sdsi tool
Build and install from the kernel source code: `tools/arch/x86/intel_sdsi/intel_sdsi.c`

### tests-isst
* intel-speed-select
stress-ng.x86_64
```
yum install stress-ng
ln -s /usr/bin/stress-ng /usr/bin/stress
```

### tests-cstate
* perf.x86_64 package
```
yum install perf
```

### tests-pstate and tests-rapl
* turbostat tool version 2024.xx.xx is required,
recompile from the latest mainline kernel source code: `tools/power/x86/turbostat/turbostat.c`

## Known Issues
### Tools Missing
* cpuid
(workaround: copy from CentOS 9)

* rdmsr-tool

* Kernel Features Missing
gcc missing AMX FP16 support
(workaround: compile tmul.c with gcc13+ and copy the binary into OE)

* Kernel idxd driver missing SVA support
(resulting in DSA/IAX not working)

* CET
OE kernel does NOT configuure CONFIG_X86_USER_SHADOW_STACK=y, resulting in CET SHSTK not working.

* OS failed to put CPUs offline, the unknown driver module may have improper IRQ allocation,
which will cause available IRQ is not enough during CPUs Offline and online. e.g. error log
CPU 206 has 151 vectors, 103 available. Cannot disable CPU
CPU 207 has 150 vectors, 102 available. Cannot disable CPU
