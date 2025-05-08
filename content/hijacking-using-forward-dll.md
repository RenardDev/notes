---
title: Hijacking DLL Using Function Forwards - A Left 4 Dead 2 Case Study
tags:
  - Hijack
  - Left 4 Dead 2
  - Detours
---
## Overview

This post explains how to hijack a DLL by leveraging function forwards. In this case study for Left 4 Dead 2, the original `engine.dll` is renamed to `engine_src.dll`. A new DLL, taking the original name `engine.dll`, is then created to forward function calls to the renamed original. This method allows intercepting or extending the application's functionality without modifying its core binaries.

## How It Works

1. **Renaming the Original DLL:**  
   The original `engine.dll` is renamed to `engine_src.dll`. This step is crucial as it preserves the original functionality while enabling the hijack DLL to call its exported functions seamlessly.

2. **Exporting Functions via Forwards:**  
   The hijack DLL (now named `engine.dll`) forwards the necessary functions. Function forwards essentially act as pointers, aliasing the functions that reside in `engine_src.dll`.

3. **Using Detours:**  
   The implementation leverages the Detours library (available at [RenardDev/Detours](https://github.com/RenardDev/Detours)). Detours simplifies the complexity of intercepting and redirecting function calls to the original DLL.

## Detailed Example

Below is an annotated code example that demonstrates the construction of the hijack DLL:

```cpp
#include "framework.h"

// Include the Detours library, which aids in function forwarding.
// See: https://github.com/RenardDev/Detours
#include "Detours.h"

// Export directives for forwarding functions.
// Each directive maps an export from engine_src.dll to the corresponding export in the hijack DLL.
EXPORT("engine_src.?F@@YAXPAPAVIEngineAPI@@@Z", "?F@@YAXPAPAVIEngineAPI@@@Z")
EXPORT("engine_src.CreateInterface", "CreateInterface")
EXPORT("engine_src.cvar", "cvar")
EXPORT("engine_src.g_pCVar", "g_pCVar")

BOOL APIENTRY DllMain(HMODULE hModule, DWORD ul_reason_for_call, LPVOID lpReserved) {
    switch (ul_reason_for_call) {
        case DLL_PROCESS_ATTACH:
            break;
        case DLL_THREAD_ATTACH:
            break;
        case DLL_THREAD_DETACH:
            break;
        case DLL_PROCESS_DETACH:
            break;
    }

    return TRUE;
}
```

---
### See also

---
### References
- [RenardDev/Detours](https://github.com/RenardDev/Detours)
