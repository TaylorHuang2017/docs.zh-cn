---
title: ICorDebugRuntimeUnwindableFrame 接口
ms.date: 03/30/2017
api_name:
- ICorDebugUnwindableFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugUnwindableFrame
helpviewer_keywords:
- ICorDebugUnwindableFrame interface [.NET Framework debugging]
ms.assetid: cd6a3982-6ed3-4909-808d-a66055e813e0
topic_type:
- apiref
ms.openlocfilehash: 2902744b6af3c7b2bd4def73b04807ce3333a8a1
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73131891"
---
# <a name="icordebugruntimeunwindableframe-interface"></a>ICorDebugRuntimeUnwindableFrame 接口
提供对非托管方法的支持，这些方法需要公共语言运行时 (CLR) 来展开帧。  
  
## <a name="remarks"></a>备注  
 `ICorDebugRuntimeUnwindableFrame` 是 ICorDebugFrame 接口的专用版本。 它由需要运行时展开当前堆栈上的帧的非托管方法使用。 现有的展开约定不起作用，因为它们不使用 JIT 编译代码。 当调试器发现不可展开帧时，它应使用[ICorDebugStackWalk：： Next](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-next-method.md)方法展开它，但它应执行检查。 调试器接收到 `ICorDebugRuntimeUnwindableFrame`时，它可以调用[ICorDebugStackWalk：： GetContext](../../../../docs/framework/unmanaged-api/debugging/icordebugstackwalk-getcontext-method.md)方法来检索框架的上下文。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头**：CorDebug.idl、CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [调试接口](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [调试](../../../../docs/framework/unmanaged-api/debugging/index.md)
