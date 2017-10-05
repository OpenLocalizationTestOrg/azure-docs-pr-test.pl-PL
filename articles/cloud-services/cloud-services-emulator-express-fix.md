---
title: "Instalacji ekspresowej wersji emulatora do debugowania aplikacji usługi w chmurze w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak instalowanie pakietu redystrybucyjnego C++, aby włączyć emulatora Express programu Visual Studio"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="e568d-103">Debugowanie aplikacji usługi w chmurze w VS 2017 przy użyciu emulatora Express</span><span class="sxs-lookup"><span data-stu-id="e568d-103">Use Emulator Express to debug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="e568d-104">W tym artykule wyjaśniono, jak użyć emulatora Express do debugowania aplikacji usługi w chmurze w VS 2017 r.</span><span class="sxs-lookup"><span data-stu-id="e568d-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="e568d-105">Kontekst tła</span><span class="sxs-lookup"><span data-stu-id="e568d-105">Background context</span></span>
<span data-ttu-id="e568d-106">Ekspresowej wersji emulatora jest używany domyślnie do debugowania role sieci Web usługi w chmurze i proces roboczy w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e568d-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="e568d-107">To ustawienie jest określone na stronie właściwości projektu usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e568d-107">This setting is specified in the Cloud Services project properties page.</span></span>

![Otwórz właściwości projektu][0]

![Emulator express został wybrany jako domyślny][1]

<span data-ttu-id="e568d-110">[Visual C++ Redistributable] [ Visual C++ Redistributable] express dla programu Visual Studio jest wymagany przez Emulator.</span><span class="sxs-lookup"><span data-stu-id="e568d-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="e568d-111">Obecnie nie jest instalowana z obciążeniem, platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e568d-111">Currently it is not installed with the Azure workload.</span></span> <span data-ttu-id="e568d-112">Po gestu F5 debugowanie aplikacji usługi w chmurze Visual Studio będzie monit Zainstaluj ten składnik i kontynuować debugowanie.</span><span class="sxs-lookup"><span data-stu-id="e568d-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span></span>

![Monituj o zainstaluj pakiet redystrybucyjny programu C++][2]

<span data-ttu-id="e568d-114">Kliknij przycisk Tak, aby zainstalować pakiet redystrybucyjny programu C++.</span><span class="sxs-lookup"><span data-stu-id="e568d-114">Click Yes to install C++ Redistributable.</span></span>

![Instalowanie pakietu redystrybucyjnego C++][3]

<span data-ttu-id="e568d-116">Naciśnij klawisz F5, aby ponownie uruchomić sesji debugowania.</span><span class="sxs-lookup"><span data-stu-id="e568d-116">Press F5 again to launch debugging sessions.</span></span>

![Rozpocznij debugowanie][4]

![Debugowanie powiodło się][5]

> <span data-ttu-id="e568d-119">Uwaga: Instalowanie pakietu redystrybucyjnego Visual C++ jest jednorazowe nakładu pracy.</span><span class="sxs-lookup"><span data-stu-id="e568d-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="e568d-120">Jeśli zostały uaktualniania ze starszej wersji zestawu SDK platformy Azure i zainstalowaniu emulatora Express nie wystąpi ten problem.</span><span class="sxs-lookup"><span data-stu-id="e568d-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="e568d-121">Obejście ręczne</span><span class="sxs-lookup"><span data-stu-id="e568d-121">Manual workaround</span></span>
<span data-ttu-id="e568d-122">Można także zainstalować [Visual C++ Redistributable] [ Visual C++ Redistributable] ręcznie i zostaną one zastosowane sam efekt, jak jak Visual Studio na nim zainstalowany w tym systemie.</span><span class="sxs-lookup"><span data-stu-id="e568d-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="e568d-123">[VCRedist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="e568d-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="e568d-124">[VCRedist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="e568d-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="e568d-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e568d-125">Next Steps</span></span>
<span data-ttu-id="e568d-126">Dowiedz się więcej o przy użyciu emulatora usługi Azure komputera do debugowania aplikacji usługi w chmurze w programie Visual Studio: [przy użyciu emulatora Express by przeprowadzić debugowanie usługi w chmurze na komputerze lokalnym][Using Emulator Express to run and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="e568d-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
