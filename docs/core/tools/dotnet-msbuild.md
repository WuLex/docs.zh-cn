---
title: dotnet msbuild 命令 - .NET Core CLI
description: dotnet msbuild 命令可提供对 MSBuild 命令行的访问权限。
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.openlocfilehash: c51c058391de4925afd4339fe84e28500d692e1a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="dotnet-msbuild"></a>dotnet msbuild

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet msbuild` - 生成项目及其所有依赖项。

## <a name="synopsis"></a>摘要

`dotnet msbuild <msbuild_arguments> [-h]`

## <a name="description"></a>描述

`dotnet msbuild` 命令允许访问功能完备的 MSBuild。

该命令与现有的 MSBuild 命令行客户端具有完全相同的功能。 选项一致。 使用 [MSBuild 命令行引用](/visualstudio/msbuild/msbuild-command-line-reference)获取可用选项的信息。 

## <a name="examples"></a>示例

生成项目及其依赖项：

`dotnet msbuild`

使用“发布”配置生成项目及其依赖项：

`dotnet msbuild /p:Configuration=Release`

运行发布目标并发布 `osx.10.11-x64` RID：

`dotnet msbuild /t:Publish /p:RuntimeIdentifiers=osx.10.11-x64`

请参阅包含 SDK 添加的所有目标的整个项目：

`dotnet msbuild /pp`
