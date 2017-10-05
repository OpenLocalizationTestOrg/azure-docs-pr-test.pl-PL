---
title: "Włącz koligacji sesji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse"
description: "Dowiedz się, jak włączyć koligacji sesji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="adb39-103">Włącz koligacji sesji</span><span class="sxs-lookup"><span data-stu-id="adb39-103">Enable Session Affinity</span></span>
<span data-ttu-id="adb39-104">W ramach zestawu narzędzi platformy Azure dla programu Eclipse można włączyć koligacji sesji HTTP, lub "trwałe sesje", dla poszczególnych ról.</span><span class="sxs-lookup"><span data-stu-id="adb39-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="adb39-105">Poniższy obraz przedstawia **równoważenia obciążenia** używane do włączania funkcji koligacji sesji okno dialogowe właściwości:</span><span class="sxs-lookup"><span data-stu-id="adb39-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="adb39-106">Aby włączyć koligacji sesji dla roli użytkownika</span><span class="sxs-lookup"><span data-stu-id="adb39-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="adb39-107">Kliknij prawym przyciskiem myszy rolę, w obszarze Eksplorator projektów programu Eclipse na, kliknij przycisk **Azure**, a następnie kliknij przycisk **równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="adb39-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="adb39-108">W **właściwości WorkerRole1 Równoważenie obciążenia sieciowego** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="adb39-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="adb39-109">a.</span><span class="sxs-lookup"><span data-stu-id="adb39-109">a.</span></span> <span data-ttu-id="adb39-110">Sprawdź **koligacji sesji HTTP włączyć (trwałe sesje) dla tej roli.**</span><span class="sxs-lookup"><span data-stu-id="adb39-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="adb39-111">b.</span><span class="sxs-lookup"><span data-stu-id="adb39-111">b.</span></span> <span data-ttu-id="adb39-112">Aby uzyskać **wejściowy punkt końcowy do użycia**, wybierz wejściowy punkt końcowy do użycia, na przykład **http (publicznego: 80, private: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="adb39-112">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="adb39-113">Aplikacja musi używać tego punktu końcowego, jako jego punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="adb39-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="adb39-114">Można włączyć wiele punktów końcowych dla roli użytkownika, ale można wybrać tylko jeden z nich do obsługi trwałe sesje.</span><span class="sxs-lookup"><span data-stu-id="adb39-114">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>

   <span data-ttu-id="adb39-115">c.</span><span class="sxs-lookup"><span data-stu-id="adb39-115">c.</span></span> <span data-ttu-id="adb39-116">Aplikacja jest ponownie kompilowana.</span><span class="sxs-lookup"><span data-stu-id="adb39-116">Rebuild your application.</span></span>

<span data-ttu-id="adb39-117">Po włączeniu, jeśli masz więcej niż jedno wystąpienie roli, pochodzących z określonego klienta żądań HTTP będą nadal obsługiwane przez tego samego wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="adb39-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="adb39-118">Zestaw narzędzi Eclipse umożliwia to przez zainstalowanie specjalne moduł usług IIS do każdego wystąpienia roli o nazwie Routing żądań aplikacji (ARR).</span><span class="sxs-lookup"><span data-stu-id="adb39-118">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="adb39-119">Moduł ARR zmienia trasę żądania HTTP do wystąpienia odpowiedniej roli.</span><span class="sxs-lookup"><span data-stu-id="adb39-119">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="adb39-120">Zestaw narzędzi automatycznie skonfiguruje wybranego punktu końcowego, tak aby ruch przychodzący HTTP najpierw jest kierowane do oprogramowania ARR.</span><span class="sxs-lookup"><span data-stu-id="adb39-120">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="adb39-121">Zestaw narzędzi również tworzy nowy wewnętrzny punkt końcowy który serwer Java jest skonfigurowany do nasłuchiwania.</span><span class="sxs-lookup"><span data-stu-id="adb39-121">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="adb39-122">To punktowi końcowemu używanemu przez moduł ARR do przekierowywania ruchu HTTP do wystąpienia odpowiedniej roli.</span><span class="sxs-lookup"><span data-stu-id="adb39-122">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="adb39-123">W ten sposób każde wystąpienie roli we wdrożeniu w wielu wystąpieniach służy jako zwrotny serwer proxy dla wszystkich innych przypadkach włączenie trwałe sesje.</span><span class="sxs-lookup"><span data-stu-id="adb39-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="adb39-124">Uwagi dotyczące koligacji sesji</span><span class="sxs-lookup"><span data-stu-id="adb39-124">Notes about session affinity</span></span>
* <span data-ttu-id="adb39-125">Koligacja sesji nie działa w emulatorze obliczeń.</span><span class="sxs-lookup"><span data-stu-id="adb39-125">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="adb39-126">Ustawienia mogą być stosowane w emulatorze obliczeń bez zakłócania w procesie kompilacji lub wykonywania emulatora obliczeniowe, ale sama ta funkcja nie działa w ramach emulatora obliczeń.</span><span class="sxs-lookup"><span data-stu-id="adb39-126">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>

* <span data-ttu-id="adb39-127">Włączenie koligacji sesji spowoduje zwiększenie ilości miejsca na dysku zajmowanego przez wdrożenia na platformie Azure jako dodatkowego oprogramowania zostanie pobrany i zainstalowany w wystąpienia roli, po uruchomieniu usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="adb39-127">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>

* <span data-ttu-id="adb39-128">Czas inicjowania każdej roli będzie trwać dłużej.</span><span class="sxs-lookup"><span data-stu-id="adb39-128">The time to initialize each role will take longer.</span></span>

* <span data-ttu-id="adb39-129">Wewnętrzny punkt końcowy, do działania jako rerouter ruchu, jak wspomniano powyżej, zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="adb39-129">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="adb39-130">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="adb39-130">See Also</span></span>
<span data-ttu-id="adb39-131">[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="adb39-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="adb39-132">[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="adb39-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="adb39-133">[Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="adb39-133">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="adb39-134">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="adb39-134">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
