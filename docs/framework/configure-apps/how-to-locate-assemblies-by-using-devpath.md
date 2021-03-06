---
title: 如何：使用 DEVPATH 查找程序集
ms.date: 03/30/2017
helpviewer_keywords:
- DEVPATH
- .NET Framework application configuration, assemblies
- application configuration files, specifying assembly's location
- app.config files, assembly locations
- locating assemblies
- assemblies [.NET Framework], location
ms.assetid: 44d2eadf-7eec-443c-a2ac-d601fd919e17
ms.openlocfilehash: 6fa864f814d6a9ce04f2bce92c61cd0075ab5145
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913002"
---
# <a name="how-to-locate-assemblies-by-using-devpath"></a>如何：使用 DEVPATH 查找程序集
开发人员可能希望确保它们所构建的共享程序集在多个应用程序中正常工作。 开发人员可以创建一个 DEVPATH 环境变量, 该变量指向程序集的生成输出目录, 而不是在开发周期期间将程序集不断置于全局程序集缓存中。  
  
 例如, 假设要生成一个名为 MySharedAssembly 的共享程序集, 并且输出目录为 C:\MySharedAssembly\Debug。 可以将 C:\MySharedAssembly\Debug 放在 DEVPATH 变量中。 然后必须在计算机配置文件中指定[ \<developmentMode >](./file-schema/runtime/developmentmode-element.md)元素。 此元素告知公共语言运行时使用 DEVPATH 来定位程序集。  
  
 共享程序集必须可由运行时发现。  若要为解析程序集引用指定一个专用目录, 请使用[ \<基本代码 > 元素](./file-schema/runtime/codebase-element.md), 或[ \<](./file-schema/runtime/probing-element.md)在配置文件中探测 > 元素, 如[指定程序集的位置](specify-assembly-location.md)中所述。  你还可以将程序集放在应用程序目录的子目录中。 有关更多信息，请参阅 [运行时如何定位程序集](../deployment/how-the-runtime-locates-assemblies.md)。  
  
> [!NOTE]
> 这是一项高级功能, 仅用于开发。  
  
 下面的示例演示如何使运行时在由 DEVPATH 环境变量指定的目录中搜索程序集。  
  
## <a name="example"></a>示例  
  
```xml  
<configuration>  
  <runtime>  
    <developmentMode developerInstallation="true"/>  
  </runtime>  
</configuration>  
```  
  
 此设置默认为 false。  
  
> [!NOTE]
> 仅在开发时使用此设置。 运行时不检查在 DEVPATH 中找到的具有强名称的程序集的版本。 它只使用它找到的第一个程序集。  
  
## <a name="see-also"></a>请参阅

- [使用配置文件配置应用程序](index.md)
