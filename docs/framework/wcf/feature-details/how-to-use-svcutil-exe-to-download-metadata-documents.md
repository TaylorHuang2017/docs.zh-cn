---
title: 如何：使用 Svcutil.exe 下载元数据文档
ms.date: 03/30/2017
ms.assetid: 15524274-3167-4627-b722-d6cedb9fa8c6
ms.openlocfilehash: 359cdb58ef65c9fb69c0ecfc759f70164a369cce
ms.sourcegitcommit: 09b4090b78f52fd09b0e430cd4b26576f1fdf96e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2020
ms.locfileid: "76212105"
---
# <a name="how-to-use-svcutilexe-to-download-metadata-documents"></a>如何：使用 Svcutil.exe 下载元数据文档
您可以使用 Svcutil.exe 从正在运行的服务中下载元数据并将元数据保存到本地文件。 对于 HTTP 和 HTTPS URL 方案，Svcutil.exe 尝试使用 Ws-metadataexchange 和[XML Web Service 发现](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/fxx6cfx2(v=vs.100))检索元数据。 对于所有其他 URL 架构，Svcutil.exe 仅使用 WS-MetadataExchange。  
  
 默认情况下，Svcutil.exe 使用 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 类中定义的绑定。 若要配置用于 WS-MetadataExchange 的绑定，必须在 Svcutil.exe 的配置文件 (svcutil.exe.config) 中定义一个客户端终结点，使该终结点使用 `IMetadataExchange` 约定，并具有与元数据终结点地址的统一资源标识符 (URI) 架构相同的名称。  
  
> [!CAUTION]
> 当运行 Svcutil.exe 来获取公开两个不同服务协定的服务的元数据时，每个服务协定分别包含同一名称的操作时，Svcutil.exe 会显示错误，指出 "无法从 ... 中获取元数据"例如，如果你有一个服务，该服务公开一个名为 `ICarService` 的服务协定，该服务协定具有一个操作 `Get(Car c)` 并且同一服务公开一个名为 `IBookService` 的服务协定，该协定具有一个操作 `Get(Book b)`。 若要解决此问题，请执行下列操作之一：
>
> - 重命名其中的一项操作。
> - 将 <xref:System.ServiceModel.OperationContractAttribute.Name%2A> 设置为其他名称。
> - 使用 <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> 属性将其中一项操作的命名空间设置为其他命名空间。
  
## <a name="to-download-metadata-using-svcutilexe"></a>使用 Svcutil.exe 下载元数据  
  
1. 在以下位置找到 Svcutil.exe 工具：  
  
     C:\Program Files\Microsoft SDKs\Windows\v1.0.\bin  
  
2. 在命令提示符处，使用下面的格式启动该工具。  
  
    ```console
    svcutil.exe /t:metadata  <url>* | <epr>  
    ```  
  
     您必须指定 `/t:metadata` 选项才能下载元数据。 否则，会生成客户端代码和配置。  
  
3. > 参数 <`url`指定提供元数据的服务终结点的 URL，或者指定到联机托管的元数据文档的 URL。 `epr`> 参数为支持 Ws-metadataexchange 的服务终结点指定包含 WS-ADDRESSING `EndpointAddress` 的 XML 文件的路径。  
  
 有关使用此工具进行元数据下载的更多选项，请参阅 " [svcutil.exe" 元数据实用工具（）](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)。  
  
## <a name="example"></a>示例  
 下面的命令从正在运行的服务中下载元数据文档。  
  
```console
svcutil /t:metadata http://service/metadataEndpoint  
```  
  
## <a name="see-also"></a>另请参阅

- [ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
