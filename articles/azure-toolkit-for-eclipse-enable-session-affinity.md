---
title: "za pomocą koligacji sesji aaaEnable hello zestawu narzędzi platformy Azure dla programu Eclipse"
description: "Dowiedz się, jak za pomocą koligacji sesji tooenable hello zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="6ee53-103">Włącz koligacji sesji</span><span class="sxs-lookup"><span data-stu-id="6ee53-103">Enable Session Affinity</span></span>
<span data-ttu-id="6ee53-104">W ramach hello zestawu narzędzi platformy Azure dla programu Eclipse można włączyć koligacji sesji HTTP, lub "trwałe sesje", dla poszczególnych ról.</span><span class="sxs-lookup"><span data-stu-id="6ee53-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="6ee53-105">Witaj poniższy obraz przedstawia hello **równoważenia obciążenia** funkcji koligacji sesji hello tooenable użyć okna dialogowego właściwości:</span><span class="sxs-lookup"><span data-stu-id="6ee53-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="6ee53-106">tooenable koligacji sesji dla roli użytkownika</span><span class="sxs-lookup"><span data-stu-id="6ee53-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="6ee53-107">Kliknij prawym przyciskiem myszy rolę hello w obszarze Eksplorator projektów programu Eclipse na, kliknij przycisk **Azure**, a następnie kliknij przycisk **równoważenia obciążenia**.</span><span class="sxs-lookup"><span data-stu-id="6ee53-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="6ee53-108">W hello **właściwości WorkerRole1 Równoważenie obciążenia sieciowego** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="6ee53-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="6ee53-109">a.</span><span class="sxs-lookup"><span data-stu-id="6ee53-109">a.</span></span> <span data-ttu-id="6ee53-110">Sprawdź **koligacji sesji HTTP włączyć (trwałe sesje) dla tej roli.**</span><span class="sxs-lookup"><span data-stu-id="6ee53-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="6ee53-111">b.</span><span class="sxs-lookup"><span data-stu-id="6ee53-111">b.</span></span> <span data-ttu-id="6ee53-112">Dla **wejściowy punkt końcowy toouse**, na przykład wybierz toouse wejściowy punkt końcowy **http (publicznego: 80, private: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="6ee53-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="6ee53-113">Aplikacja musi używać tego punktu końcowego, jako jego punkt końcowy HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ee53-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="6ee53-114">Można włączyć wiele punktów końcowych dla roli użytkownika, ale można wybrać tylko jedną z nich toosupport trwałe sesje.</span><span class="sxs-lookup"><span data-stu-id="6ee53-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="6ee53-115">c.</span><span class="sxs-lookup"><span data-stu-id="6ee53-115">c.</span></span> <span data-ttu-id="6ee53-116">Aplikacja jest ponownie kompilowana.</span><span class="sxs-lookup"><span data-stu-id="6ee53-116">Rebuild your application.</span></span>

<span data-ttu-id="6ee53-117">Po włączeniu, jeśli masz więcej niż jedno wystąpienie roli, pochodzących z określonego klienta żądań HTTP będą nadal obsługiwane przez hello takie same wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="6ee53-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="6ee53-118">Hello Eclipse Toolkit umożliwia to przez zainstalowanie specjalne moduł usług IIS do każdego wystąpienia roli o nazwie Routing żądań aplikacji (ARR).</span><span class="sxs-lookup"><span data-stu-id="6ee53-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="6ee53-119">Moduł ARR zmienia trasę wystąpienia odpowiedniej roli toohello żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ee53-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="6ee53-120">zestaw narzędzi Hello automatycznie skonfiguruje hello wybrany punkt końcowy tak, aby ruch przychodzący HTTP hello pierwszy routingiem toohello ARR oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="6ee53-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="6ee53-121">Hello toolkit tworzy nowy wewnętrzny punkt końcowy, który serwer Java jest skonfigurowany toolisten do.</span><span class="sxs-lookup"><span data-stu-id="6ee53-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="6ee53-122">To jest punkt końcowy hello używane przez wystąpienie odpowiedniej roli toohello ruch HTTP ARR tooreroute hello.</span><span class="sxs-lookup"><span data-stu-id="6ee53-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="6ee53-123">W ten sposób każde wystąpienie roli we wdrożeniu w wielu wystąpieniach służy jako zwrotny serwer proxy dla wszystkich hello innych przypadkach włączenie trwałe sesje.</span><span class="sxs-lookup"><span data-stu-id="6ee53-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="6ee53-124">Uwagi dotyczące koligacji sesji</span><span class="sxs-lookup"><span data-stu-id="6ee53-124">Notes about session affinity</span></span>
* <span data-ttu-id="6ee53-125">Koligacji sesji nie działa w emulatorze obliczeń hello.</span><span class="sxs-lookup"><span data-stu-id="6ee53-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="6ee53-126">Ustawienia Hello mogą być stosowane w emulatorze obliczeń hello bez zakłócania w procesie kompilacji lub wykonywania emulatora obliczeniowe, ale funkcja hello nie działa w ramach hello emulatora obliczeń.</span><span class="sxs-lookup"><span data-stu-id="6ee53-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="6ee53-127">Włączenie koligacji sesji spowoduje zwiększenie hello ilość miejsca na dysku zajmowanego przez wdrożenia na platformie Azure jako dodatkowego oprogramowania zostanie pobrany i zainstalowany w wystąpienia roli, po uruchomieniu usługi w hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="6ee53-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="6ee53-128">tooinitialize czasu Hello każdej roli będzie trwać dłużej.</span><span class="sxs-lookup"><span data-stu-id="6ee53-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="6ee53-129">Wewnętrzny punkt końcowy toofunction jako rerouter ruchu, jak wspomniano powyżej, zostaną dodane.</span><span class="sxs-lookup"><span data-stu-id="6ee53-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="6ee53-130">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6ee53-130">See Also</span></span>
<span data-ttu-id="6ee53-131">[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6ee53-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="6ee53-132">[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6ee53-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="6ee53-133">[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="6ee53-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="6ee53-134">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="6ee53-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
