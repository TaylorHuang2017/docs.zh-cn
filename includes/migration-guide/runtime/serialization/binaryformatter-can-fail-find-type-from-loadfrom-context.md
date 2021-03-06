---
ms.openlocfilehash: ac929a8b3e9a7d56122f5699c51819ad483d1f5e
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59803350"
---
### <a name="binaryformatter-can-fail-to-find-type-from-loadfrom-context"></a>BinaryFormatter 可能无法从 LoadFrom 上下文找到类型

|   |   |
|---|---|
|详细信息|自 .NET Framework 4.5 起，大量 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> 更改可能在使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name> 反序列化 LoadFrom 上下文中负载的类型时导致反序列化出现差异。 这些更改由新的方式引起，<xref:System.Xml.Serialization.XmlSerializer?displayProperty=name> 现在加载了一种类型，可以在 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name> 稍后尝试反序列化为该类型时，导致其他行为。 默认序列化活页夹虽然在某些情况下可以基于 XmlSerializer 旧行为工作，但它不会自动搜索 LoadFrom 上下文。 由于这些更改，当从其他上下文加载的程序集加载类型时，可能引发 <xref:System.IO.FileNotFoundException?displayProperty=name>。|
|建议|如果显示此异常，则 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name> 的 <code>Binder</code> 属性可以设为将查找正确类型的自定义活页夹。<pre><code class="lang-csharp">var formatter = new BinaryFormatter { Binder = new TypeFinderBinder() }&#13;&#10;</code></pre>然后自定义活页夹：<pre><code class="lang-csharp">public class TypeFinderBinder : SerializationBinder&#13;&#10;{&#13;&#10;private static readonly string s_assemblyName = Assembly.GetExecutingAssembly().FullName;&#13;&#10;&#13;&#10;public override Type BindToType(string assemblyName, string typeName)&#13;&#10;{&#13;&#10;return Type.GetType(String.Format(CultureInfo.InvariantCulture, &quot;{0}, {1}&quot;, typeName, s_assemblyName));&#13;&#10;}&#13;&#10;}&#13;&#10;</code></pre>|
|范围|边缘|
|版本|4.5|
|类型|运行时|
|受影响的 API|<ul><li><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream,System.Runtime.Remoting.Messaging.HeaderHandler)?displayProperty=nameWithType></li></ul>|
