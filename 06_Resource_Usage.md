## Memory Consumption
The [memory_profiler](https://github.com/fabianp/memory_profiler) is a great tool to use it is based on the following concept.

### The psutil library
psutil is a python library that provides an interface for retrieving information on running processes. 
It provides convenient, fast and cross-platform functions to access the memory usage of a Python module:

```
def memory_usage_psutil():
    # return the memory usage in MB
    import psutil
    process = psutil.Process(os.getpid())
    mem = process.get_memory_info()[0] / float(2 ** 20)
    return mem
```

The above function returns the memory usage of the current Python process in MiB. Depending on the platform 
it will choose the most accurate and fastest way to get this information. For example, in Windows it will 
use the C++ Win32 API while in Linux it will read from /proc, hiding the implementation details and 
proving on each platform a fast and accurate measurement.

### Resource module

The resource module is part of the standard Python library. It's basically a wrapper around getrusage, 
which is a POSIX standard.
```
def memory_usage_resource():
    import resource
    rusage_denom = 1024.
    mem = resource.getrusage(resource.RUSAGE_SELF).ru_maxrss / rusage_denom
    return mem
```
This approach may run several times faster than the one based in psutil.

### Querying ps directly
The method based on psutils works great but is not available by default on all Python systems. 
The following works reasonably well when all else fails: invoking the system's ps command and 
parsing the output. The code is something like::
```
def memory_usage_ps():
    import subprocess
    out = subprocess.Popen(['ps', 'v', '-p', str(os.getpid())],
    stdout=subprocess.PIPE).communicate()[0].split(b'\n')
    vsz_index = out[0].split().index(b'RSS')
    mem = float(out[1].split()[vsz_index]) / 1024
    return mem
```
The main disadvantage of this approach is that it needs to fork a process for each measurement. 
For some tasks where you need to get memory usage very fast, like in line-by-line memory usage 
then this be a huge overhead on the code. For other tasks such as getting information of long-running 
processes, where the memory usage is anyway working on a separate process this is not too bad.



