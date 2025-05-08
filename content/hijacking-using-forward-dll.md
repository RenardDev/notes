---
title: Hijacking DLL using forwards
tags:
    - Hijack
---

Example code for Left 4 Dead 2. Where `engine_src.dll` is the renamed original `engine.dll`, and the hijack dll itself is renamed to `engine.dll`:

```cpp
#include "framework.h"

// Detours
#include "Detours.h" // https://github.com/RenardDev/Detours

EXPORT("engine_src.?F@@YAXPAPAVIEngineAPI@@@Z", "?F@@YAXPAPAVIEngineAPI@@@Z")
EXPORT("engine_src.CreateInterface", "CreateInterface")
EXPORT("engine_src.cvar", "cvar")
EXPORT("engine_src.g_pCVar", "g_pCVar")

BOOL APIENTRY DllMain(HMODULE hModule, DWORD ul_reason_for_call, LPVOID lpReserved) {
    switch (ul_reason_for_call)
    {
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
