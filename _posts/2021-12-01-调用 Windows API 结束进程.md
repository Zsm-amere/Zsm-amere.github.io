---
layout:     post
title:      调用 Windows API 结束进程
subtitle:   调用 Windows API 结束进程
date:       2021-12-01
author:     XL
header-img: img/post-bg-debug.png
catalog: true
tags:
	- C++
	- Windows
---

# 调用 Windows API 结束进程

```C++
#include <Windows.h>
#include <TlHelp32.h>

int WINAPI()
{
    HANDLE hProcess = CreateToolhelp32Snapshot(TH32CS_SNAPPROCESS, NULL);
    PROCESSENTRY32 *pInfo = new PROCESSENTRY32;
    pInfo->dwSize = sizeof(PROCESSENTRY32);
    
    // 遍历所有进程
    if (Process32First(hProcess, pInfo))
    {
        do
        {
            QString text = QString::fromWCharArray(pInfo->szExeFile);
            
            int a = QString::compare("Notepads.exe", text);
            if (0 == a)
            {
                // 尝试结束进程
                if (!TerminateProcess(OpenProcess(PROCESS_TERMINATE, FALSE, pInfo->th32ProcessID), TRUE))
                {
                    if (!CloseHandle(hProcess))
                    {
                        exit(-1);
                    }
                    exit(-2);
                }
                break;
            }
        }
        while (Process32Next(hProcess, pInfo));
    }
    if (!CloseHandle(hProcess))
        exit(-1);
    else
        return 0;
}
```

