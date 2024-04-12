来源：[Android inline hook 浅析](https://www.sunmoonblog.com/2019/07/15/inline-hook-basic/#Android-Inline-Hook-%E6%BA%90%E7%A0%81%E5%88%86%E6%9E%90)

# Android-Inline-Hook
thumb16 thumb32 arm32 inlineHook

# Build
```ndk-build NDK_PROJECT_PATH=. APP_BUILD_SCRIPT=./Android.mk NDK_APPLICATION_MK=./Application.mk```

# Example
```C
#include <stdio.h>

#include "inlineHook.h"

int (*old_puts)(const char *) = NULL;

int new_puts(const char *string)
{
    old_puts("inlineHook success");
}

int hook()
{
    if (registerInlineHook((uint32_t) puts, (uint32_t) new_puts, (uint32_t **) &old_puts) != ELE7EN_OK) {
        return -1;
    }
    if (inlineHook((uint32_t) puts) != ELE7EN_OK) {
        return -1;
    }

    return 0;
}

int unHook()
{
    if (inlineUnHook((uint32_t) puts) != ELE7EN_OK) {
        return -1;
    }

    return 0;
}

int main()
{
    puts("test");
    hook();
    puts("test");
    unHook();
    puts("test");
}

```

# Contact
If you find any bugs, please contact me(ele7enxxh@gmail.com)
