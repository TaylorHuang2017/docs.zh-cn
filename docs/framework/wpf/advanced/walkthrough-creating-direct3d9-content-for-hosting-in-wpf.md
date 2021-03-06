---
title: 演练：创建在 WPF 中承载的 Direct3D9 内容
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- WPF [WPF], creating Direct3D9 content
- Direct3D9 [WPF interoperability], creating Direct3D9 content
ms.assetid: 286e98bc-1eaa-4b5e-923d-3490a9cca5fc
ms.openlocfilehash: 462220b526db90d3acfa90a28f9bfd56dbe813e2
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991400"
---
# <a name="walkthrough-creating-direct3d9-content-for-hosting-in-wpf"></a>演练：创建在 WPF 中承载的 Direct3D9 内容
本演练演示如何创建适用于在 Windows Presentation Foundation （WPF）应用程序中承载的 Direct3D9 内容。 有关在 WPF 应用程序中承载 Direct3D9 内容的详细信息，请参阅[wpf 和 Direct3D9 互操作](wpf-and-direct3d9-interoperation.md)。

 在本演练中，你将要执行以下任务：

- 创建 Direct3D9 项目。

- 配置 Direct3D9 项目以在 WPF 应用程序中承载。

 完成后，将拥有一个包含 Direct3D9 内容的 DLL，以便在 WPF 应用程序中使用。

## <a name="prerequisites"></a>系统必备
 你需要以下组件来完成本演练：

- Visual Studio 2010。

- DirectX SDK 9 或更高版本。

## <a name="creating-the-direct3d9-project"></a>创建 Direct3D9 项目
 第一步是创建和配置 Direct3D9 项目。

#### <a name="to-create-the-direct3d9-project"></a>创建 Direct3D9 项目

1. 创建一个C++名为`D3DContent`的新 Win32 项目。

     Win32 应用程序向导将打开并显示欢迎屏幕。

2. 单击 **“下一步”** 。

     此时将显示 "应用程序设置" 屏幕。

3. 在 "**应用程序类型：** " 部分中，选择 " **DLL** " 选项。

4. 单击 **“完成”** 。

     生成 D3DContent 项目。

5. 在解决方案资源管理器中，右键单击 D3DContent 项目，然后选择 "**属性**"。

     此时将打开 " **D3DContent 属性页**" 对话框。

6. 选择**C/C++** 节点。

7. 在 "**附加包含目录**" 字段中，指定 DirectX 包含文件夹的位置。 此文件夹的默认位置为%ProgramFiles%\Microsoft DirectX SDK （*版本*） \Include。

8. 双击 "**链接器**" 节点将其展开。

9. 在 "**其他库目录**" 字段中，指定 DirectX Library 文件夹的位置。 此文件夹的默认位置为%ProgramFiles%\Microsoft DirectX SDK （*版本*） \Lib\x86。

10. 选择 "**输入**" 节点。

11. 在 "**其他依赖项**" 字段中`d3d9.lib` ， `d3dx9.lib`添加和文件。

12. 在解决方案资源管理器中，将名`D3DContent.def`为的新模块定义文件（.def）添加到项目。

## <a name="creating-the-direct3d9-content"></a>创建 Direct3D9 内容
 若要获得最佳性能，你的 Direct3D9 内容必须使用特定设置。 下面的代码演示如何创建具有最佳性能特征的 Direct3D9 图面。 有关详细信息，请参阅[Direct3D9 和 WPF 互操作性的性能注意事项](performance-considerations-for-direct3d9-and-wpf-interoperability.md)。

#### <a name="to-create-the-direct3d9-content"></a>创建 Direct3D9 内容

1. 使用解决方案资源管理器将三个C++类添加到名为的项目，如下所示。

     `CRenderer`（包含虚拟析构函数）

     `CRendererManager`

     `CTriangleRenderer`

2. 在代码编辑器中打开呈现器 .h，并将自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.h#rendererh)]

3. 在代码编辑器中打开呈现器 .cpp，并将自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderercpp)]

4. 在代码编辑器中打开 RendererManager，并将自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.h#renderermanagerh)]

5. 在代码编辑器中打开 RendererManager，并将自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#RendererManagerCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanagercpp)]

6. 在代码编辑器中打开 TriangleRenderer，并将自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.h#trianglerendererh)]

7. 在代码编辑器中打开 TriangleRenderer，并将自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#TriangleRendererCPP](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/trianglerenderer.cpp#trianglerenderercpp)]

8. 在代码编辑器中打开 stdafx.h，并将自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#StdafxH](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/stdafx.h#stdafxh)]

9. 在代码编辑器中打开 dllmain，并将自动生成的代码替换为以下代码。

     [!code-cpp[System.Windows.Interop.D3DImage#DllMain](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/dllmain.cpp#dllmain)]

10. 在代码编辑器中打开 D3DContent。

11. 将自动生成的代码替换为以下代码。

    ```cpp
    LIBRARY "D3DContent"

    EXPORTS

    SetSize
    SetAlpha
    SetNumDesiredSamples
    SetAdapter

    GetBackBufferNoRef
    Render
    Destroy
    ```

12. 生成项目。

## <a name="next-steps"></a>后续步骤

- 在 WPF 应用程序中托管 Direct3D9 内容。 有关详细信息，请参见[演练：在 WPF](walkthrough-hosting-direct3d9-content-in-wpf.md)中承载 Direct3D9 内容。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 和 WPF 互操作性的性能注意事项](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
- [演练：在 WPF 中承载 Direct3D9 内容](walkthrough-hosting-direct3d9-content-in-wpf.md)
