---
title: "aplikacje usługi w chmurze toodebug w programie Visual Studio express emulatora aaaSetup | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooinstall hello C++ tooenable pakietu redystrybucyjnego emulatora Express programu Visual Studio"
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
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="40661-103">Używanie emulatora Express toodebug aplikacji usługi w chmurze w VS 2017</span><span class="sxs-lookup"><span data-stu-id="40661-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="40661-104">W tym artykule opisano sposób aplikacji Express emulatora usługi w chmurze toodebug toouse w VS 2017 r.</span><span class="sxs-lookup"><span data-stu-id="40661-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="40661-105">Kontekst tła</span><span class="sxs-lookup"><span data-stu-id="40661-105">Background context</span></span>
<span data-ttu-id="40661-106">Ekspresowej wersji emulatora jest używany domyślnie do debugowania role sieci Web usługi w chmurze i proces roboczy w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40661-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="40661-107">To ustawienie jest określone na stronie właściwości projektu usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="40661-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![Otwórz właściwości projektu][0]

![Emulator express został wybrany jako domyślny][1]

<span data-ttu-id="40661-110">Witaj [Visual C++ Redistributable] [ Visual C++ Redistributable] express dla programu Visual Studio jest wymagany przez Emulator.</span><span class="sxs-lookup"><span data-stu-id="40661-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="40661-111">Obecnie nie jest instalowany z hello Azure obciążenia.</span><span class="sxs-lookup"><span data-stu-id="40661-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="40661-112">Po F5 gestu toodebug aplikacji usługi w chmurze, Visual Studio będzie monitować tooinstall ten składnik i kontynuować debugowanie.</span><span class="sxs-lookup"><span data-stu-id="40661-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![Monituj o zainstaluj pakiet redystrybucyjny programu C++][2]

<span data-ttu-id="40661-114">Kliknij przycisk Tak tooinstall C++ Redistributable.</span><span class="sxs-lookup"><span data-stu-id="40661-114">Click Yes tooinstall C++ Redistributable.</span></span>

![Instalowanie pakietu redystrybucyjnego C++][3]

<span data-ttu-id="40661-116">Naciśnij klawisz F5 ponownie toolaunch sesji debugowania.</span><span class="sxs-lookup"><span data-stu-id="40661-116">Press F5 again toolaunch debugging sessions.</span></span>

![Rozpocznij debugowanie][4]

![Debugowanie powiodło się][5]

> <span data-ttu-id="40661-119">Uwaga: Instalowanie pakietu redystrybucyjnego Visual C++ jest jednorazowe nakładu pracy.</span><span class="sxs-lookup"><span data-stu-id="40661-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="40661-120">Jeśli zostały uaktualniania ze starszej wersji zestawu SDK platformy Azure i zainstalowaniu emulatora Express nie wystąpi ten problem.</span><span class="sxs-lookup"><span data-stu-id="40661-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="40661-121">Obejście ręczne</span><span class="sxs-lookup"><span data-stu-id="40661-121">Manual workaround</span></span>
<span data-ttu-id="40661-122">Można także zainstalować hello [Visual C++ Redistributable] [ Visual C++ Redistributable] ręcznie i zostaną one zastosowane sam efekt, jak jak Visual Studio na nim zainstalowany w tym systemie.</span><span class="sxs-lookup"><span data-stu-id="40661-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="40661-123">[VCRedist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="40661-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="40661-124">[VCRedist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="40661-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="40661-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40661-125">Next Steps</span></span>
<span data-ttu-id="40661-126">Dowiedz się więcej o przy użyciu emulatora usługi Azure komputera toodebug aplikacji usługi w chmurze w programie Visual Studio: [toorun przy użyciu emulatora Express i debugowania usługi w chmurze na komputerze lokalnym][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="40661-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
