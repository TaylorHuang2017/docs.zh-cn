---
title: ICLRDataTarget::GetMachineType 方法
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.GetMachineType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::GetMachineType
helpviewer_keywords:
- ICLRDataTarget::GetMachineType method [.NET Framework debugging]
- GetMachineType method [.NET Framework debugging]
ms.assetid: 5f1f9c61-3e3b-48b2-b111-a4395f7623a7
topic_type:
- apiref
ms.openlocfilehash: 941d1b4057ef78a6235a0ba853e48a000f2087e8
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73122888"
---
# <a name="iclrdatatargetgetmachinetype-method"></a>ICLRDataTarget::GetMachineType 方法
获取目标进程正在使用的指令集类型的标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetMachineType (  
    [out] ULONG32     *machineType  
);  
```  
  
## <a name="parameters"></a>参数  
 `machineType`  
 弄一个指向值的指针，该指针指示目标进程使用的指令集。 返回的 `machineType` 是在 WinNT 头文件中定义的 IMAGE_FILE_MACHINE 常量之一。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** ClrData，ClrData  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [ICLRDataTarget 接口](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget-interface.md)
