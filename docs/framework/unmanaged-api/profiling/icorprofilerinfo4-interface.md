---
title: ICorProfilerInfo4 接口
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4
helpviewer_keywords:
- ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 80a5308e-c22f-4201-ba89-31cc8562515b
topic_type:
- apiref
ms.openlocfilehash: cbd7c0d8fff55766a98e727ce22c77dd5214611b
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2019
ms.locfileid: "74448005"
---
# <a name="icorprofilerinfo4-interface"></a>ICorProfilerInfo4 接口
提供代码探查器用于与公共语言运行时（CLR）进行通信以控制事件监视和请求信息的方法。 . `ICorProfilerInfo4` 接口是其他 `ICorProfilerInfo` 接口的扩展。 它提供了用于支持实时（JIT）重新编译的新方法，已添加到 .NET Framework 4.5。  
  
## <a name="methods"></a>方法  
  
|方法|说明|  
|------------|-----------------|  
|[EnumJITedFunctions2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-enumjitedfunctions2-method.md)|返回之前 JIT 编译和 JIT 重新编译的所有函数的枚举器。|  
|[EnumThreads 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-enumthreads-method.md)|获取一个枚举器，该枚举器提供按顺序循环访问所分析进程中所有托管线程的集合的方法。|  
|[GetCodeInfo3 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getcodeinfo3-method.md)|获取本机代码的范围，该代码与指定函数的 JIT 重新编译版本相关联。|  
|[GetFunctionFromIP2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getfunctionfromip2-method.md)|将托管代码指令指针映射到指定函数的 JIT 重新编译版本。|  
|[GetILToNativeMapping2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getiltonativemapping2-method.md)|从 Microsoft 中间语言（MSIL）偏移量到指定函数的 JIT 重新编译版本中包含的代码的本机偏移量的映射。|  
|[GetObjectSize2 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getobjectsize2-method.md)|返回指定的对象的大小。|  
|[GetReJITIDs 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-getrejitids-method.md)|返回 Id 的数组，这些 Id 标识仍分配的指定函数的所有 JIT 重新编译版本。|  
|[InitializeCurrentThread 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-initializecurrentthread-method.md)|在同一线程上的后续探查器 API 调用之前初始化当前线程，以便避免死锁。|  
|[RequestReJIT 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-requestrejit-method.md)|请求 JIT 重新编译指定函数的所有实例。|  
|[RequestRevert 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-requestrevert-method.md)|将指定函数的所有实例还原为其初始版本。|  
  
## <a name="remarks"></a>备注  
 CLR 通过使用自由线程模型实现 `ICorProfilerInfo4` 接口的方法。 每个方法均返回一个 HRESULT，指示成功或失败。 有关可能的返回代码的列表，请参阅 CorError.h 文件。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **头文件：** CorProf.idl、CorProf.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [Profiling 接口](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [ICorProfilerInfo 接口](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
