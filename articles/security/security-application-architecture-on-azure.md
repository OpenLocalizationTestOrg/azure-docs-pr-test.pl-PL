---
title: "aaaIntegrate zabezpieczeń do platformy Azure projekty architektury | Dokumentacja firmy Microsoft"
description: " Ten artykuł pomoże poznać Architektura usług i aplikacji hello na Azure toomake go łatwiejsze zabezpieczeń toointegrate do projektowania i implementacji. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="0e0e8-103">Architektura aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0e0e8-103">Application architecture on Azure</span></span>
<span data-ttu-id="0e0e8-104">toohelp Zabezpieczanie rozwiązań opartych na chmurze w systemie Microsoft Azure silne foundation architektury ma kluczowe znaczenie.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="0e0e8-105">Architektów, projektantów i implementacje korzystać z silnej wiedzy architektury usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="0e0e8-106">Ta wiedza podstawowych ułatwiające zrozumienie wszystkie składniki hello rozwiązań opartych na chmurze i stał się łatwiejsze zabezpieczeń toointegrate do wszystkich aspektów projektowania i implementacji.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="0e0e8-107">Firma Microsoft ma hello następujących toohelp możesz przy użyciu architektury dochodzenia i projektów:</span><span class="sxs-lookup"><span data-stu-id="0e0e8-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="0e0e8-108">Infographics architektury</span><span class="sxs-lookup"><span data-stu-id="0e0e8-108">Architectural infographics</span></span>
* <span data-ttu-id="0e0e8-109">Plany architektury</span><span class="sxs-lookup"><span data-stu-id="0e0e8-109">Architectural blueprints</span></span>
* <span data-ttu-id="0e0e8-110">Zestaw symboli cloud i enterprise</span><span class="sxs-lookup"><span data-stu-id="0e0e8-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="0e0e8-111">Szablon programu Visio planu 3D</span><span class="sxs-lookup"><span data-stu-id="0e0e8-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="0e0e8-112">Infographics architektury</span><span class="sxs-lookup"><span data-stu-id="0e0e8-112">Architectural infographics</span></span>
<span data-ttu-id="0e0e8-113">Firma Microsoft publikuje kilka architektury pokrewne plakaty/infographics.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="0e0e8-114">Obejmują one:</span><span class="sxs-lookup"><span data-stu-id="0e0e8-114">They include:</span></span>

* [<span data-ttu-id="0e0e8-115">Tworzenie aplikacji rzeczywistych chmury</span><span class="sxs-lookup"><span data-stu-id="0e0e8-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="0e0e8-116">Skalowanie z usługami w chmurze</span><span class="sxs-lookup"><span data-stu-id="0e0e8-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="0e0e8-117">Plany architektury</span><span class="sxs-lookup"><span data-stu-id="0e0e8-117">Architectural blueprints</span></span>
<span data-ttu-id="0e0e8-118">Firma Microsoft publikuje zbiór wysokiego poziomu [architektury plany](http://aka.ms/azblueprints) przedstawiający sposób toobuild określone typy systemów przy użyciu produktów firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="0e0e8-119">Każdy plan zawiera:</span><span class="sxs-lookup"><span data-stu-id="0e0e8-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="0e0e8-120">Płaskie 2D Visio 2003 plików, który można pobrać i zmodyfikować</span><span class="sxs-lookup"><span data-stu-id="0e0e8-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="0e0e8-121">Kolorowe perspektywy 3W PDF pliku toointroduce hello planu tooless techniczne odbiorców</span><span class="sxs-lookup"><span data-stu-id="0e0e8-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="0e0e8-122">Wideo, który przeprowadzi Cię przez hello wersji 3D</span><span class="sxs-lookup"><span data-stu-id="0e0e8-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="0e0e8-123">Zestaw symboli cloud i enterprise</span><span class="sxs-lookup"><span data-stu-id="0e0e8-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="0e0e8-124">[Wyświetl hello Visio i symbole szkolenia wideo](http://aka.ms/CnESymbolsVideo) , a następnie [pobrać zestaw Cloud i Enterprise Symbol hello](http://aka.ms/CnESymbols) toohelp utworzyć technicznej materiały, które opisują Azure, Windows Server, SQL Server i inne.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="0e0e8-125">Można użyć symboli hello w diagramów architektury, materiałów szkoleniowych prezentacji, arkusze danych, infographics, oficjalne dokumenty i nawet książek innych firm, jeśli pociągu książki hello osoby toouse produktów firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="0e0e8-126">Jednak nie są przeznaczone do użycia w interfejsów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="0e0e8-127">Szablon programu Visio planu 3D</span><span class="sxs-lookup"><span data-stu-id="0e0e8-127">3D blueprint Visio template</span></span>
<span data-ttu-id="0e0e8-128">Witaj 3D wersje hello [plany architektura Microsoft](http://aka.ms/azblueprints) początkowo zostały utworzone w narzędziu do firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="0e0e8-129">Nowy szablon programu Visio 2013 (lub nowszym) wysłane na 5 sierpnia 2015 roku jako część [kursu certyfikacji Microsoft Architecture rozproszone na EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="0e0e8-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="0e0e8-130">Szablon Hello jest również dostępna poza hello kursu.</span><span class="sxs-lookup"><span data-stu-id="0e0e8-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="0e0e8-131">[Wyświetl wideo szkolenia hello](http://aka.ms/3dBlueprintTemplateVideo) pierwszy, aby wiedzieć, co można zrobić</span><span class="sxs-lookup"><span data-stu-id="0e0e8-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="0e0e8-132">Pobierz hello [Microsoft 3d szablon programu Visio planu](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="0e0e8-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="0e0e8-133">Pobierz hello [Cloud i Enterprise symboli](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse hello szablonu 3D</span><span class="sxs-lookup"><span data-stu-id="0e0e8-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
