---
title: CorBindToRuntime 函数
ms.date: 03/30/2017
api_name:
- CorBindToRuntime
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- CorBindToRuntime
helpviewer_keywords:
- CorBindToRuntime function [.NET Framework hosting]
ms.assetid: 799740aa-46ec-4532-95da-6444565b4971
topic_type:
- apiref
ms.openlocfilehash: 9d4b8bb7d5b3da15f665849c8d18c3a10dbe600b
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73138314"
---
# <a name="corbindtoruntime-function"></a>CorBindToRuntime 函数
使非托管宿主能够将公共语言运行时（CLR）加载到进程中。  
  
 此函数已在 .NET Framework 4 中弃用。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT CorBindToRuntime (  
    [in]  LPCWSTR     pwszVersion,   
    [in]  LPCWSTR     pwszBuildFlavor,   
    [in]  REFCLSID    rclsid,   
    [in]  REFIID      riid,   
    [out] LPVOID FAR  *ppv  
);  
```  
  
## <a name="parameters"></a>参数  
 `pwszVersion`  
 中一个字符串，描述要加载的 CLR 的版本。  
  
 .NET Framework 中的版本号由以句点分隔的四个部分组成：*主*版本. 次要版本. 内部版本号. 修订号。 作为 `pwszVersion` 传递的字符串必须以字符 "v" 开头，后跟版本号的前三个部分（例如，"1.0.1529"）。  
  
 某些版本的 CLR 随策略声明一起安装，后者指定与以前版本的 CLR 的兼容性。 默认情况下，启动填充程序根据策略语句计算 `pwszVersion`，并加载与请求的版本兼容的运行时的最新版本。 主机可以通过为 `flags` 参数传递值 `STARTUP_LOADER_SAFEMODE` 来强制填充程序跳过策略评估并加载 `pwszVersion` 中指定的确切版本，如下所述。  
  
 如果调用方为 `pwszVersion`指定 null，则加载最新版本的运行时。 如果传递 null，则主机将无法控制加载的运行时版本。 虽然这种方法可能适用于某些情况，但强烈建议主机提供要加载的特定版本。  
  
 `pwszBuildFlavor`  
 中一个字符串，指定是加载 CLR 的服务器还是工作站版本。 有效值为 `svr` 和 `wks`。 服务器版本经过优化，可利用多个处理器进行垃圾回收，工作站构建针对单处理器计算机上运行的客户端应用程序进行了优化。  
  
 如果 `pwszBuildFlavor` 设置为 null，则会加载工作站构建。 在单处理器计算机上运行时，始终会加载工作站构建，即使 `pwszBuildFlavor` 设置为 `svr`。 但是，如果 `pwszBuildFlavor` 设置为 `svr` 并指定了并发垃圾回收（请参阅 `flags` 参数的说明），则将加载服务器生成。  
  
 `rclsid`  
 中用于实现[ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)或[ICLRRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-interface.md)接口的 coclass 的 `CLSID`。 支持的值为 CLSID_CorRuntimeHost 或 CLSID_CLRRuntimeHost。  
  
 `riid`  
 中从 `rclsid`请求的接口的 `IID`。 支持的值为 IID_ICorRuntimeHost 或 IID_ICLRRuntimeHost。  
  
 `ppv`  
 弄返回 `riid`的接口指针。  
  
## <a name="remarks"></a>备注  
 如果 `pwszVersion` 指定不存在的运行时版本，则 `CorBindToRuntimeEx` 返回 HRESULT 值 CLR_E_SHIM_RUNTIMELOAD。  
  
## <a name="execution-context-and-flow-of-windows-identity"></a>执行上下文和 Windows 标识流  
 在 CLR 版本1中，<xref:System.Security.Principal.WindowsIdentity> 对象不流经异步点，如新线程、线程池或计时器回调。 在 CLR 版本2.0 中，<xref:System.Threading.ExecutionContext> 对象包装了有关当前正在执行的线程的一些信息，并在所有异步点（而不是跨应用程序域边界）传递它。 同样，<xref:System.Security.Principal.WindowsIdentity> 对象还会流经任何异步点。 因此，线程上的当前模拟（如果有）也会流动。  
  
 可以通过两种方式更改流：  
  
1. 通过修改 <xref:System.Threading.ExecutionContext> 设置以按线程抑制流（请参阅 <xref:System.Threading.ExecutionContext.SuppressFlow%2A>、<xref:System.Security.SecurityContext.SuppressFlow%2A>和 <xref:System.Security.SecurityContext.SuppressFlowWindowsIdentity%2A> 方法）。  
  
2. 将进程默认模式更改为版本1兼容模式，其中 <xref:System.Security.Principal.WindowsIdentity> 对象不在任何异步点上流动，无论当前线程上的 <xref:System.Threading.ExecutionContext> 设置如何。 更改默认模式的方式取决于您使用的是托管可执行文件还是非托管承载接口来加载 CLR：  
  
    1. 对于托管的可执行文件，必须将[\<legacyImpersonationPolicy >](../../../../docs/framework/configure-apps/file-schema/runtime/legacyimpersonationpolicy-element.md)元素的 `enabled` 属性设置为 "`true`"。  
  
    2. 对于非托管承载接口，请在调用 `CorBindToRuntimeEx` 函数时设置 `flags` 参数中的 `STARTUP_LEGACY_IMPERSONATION` 标志。  
  
     版本1兼容性模式适用于整个进程和进程中的所有应用程序域。  
  
## <a name="remarks"></a>备注  
 [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)和 `CorBindToRuntime` 执行相同的操作，但 `CorBindToRuntimeEx` 函数允许您设置标志来指定 CLR 的行为。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Mscoree.dll  
  
 **库：** Mscoree.dll  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [CorBindToCurrentRuntime 函数](../../../../docs/framework/unmanaged-api/hosting/corbindtocurrentruntime-function.md)
- [CorBindToRuntimeByCfg 函数](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)
- [CorBindToRuntimeEx 函数](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)
- [CorBindToRuntimeHost 函数](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimehost-function.md)
- [ICorRuntimeHost 接口](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)
- [弃用的 CLR 承载函数](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
