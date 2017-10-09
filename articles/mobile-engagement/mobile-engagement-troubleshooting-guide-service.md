---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - usługi"
description: "Rozwiązywanie problemów z przewodniki dotyczące usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="8e588-103">Przewodnik rozwiązywania problemów dotyczących usługi</span><span class="sxs-lookup"><span data-stu-id="8e588-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="8e588-104">Witaj poniżej przedstawiono możliwe problemy, które mogą się pojawić w sposób uruchamiania usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e588-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="8e588-105">Awarie usługi</span><span class="sxs-lookup"><span data-stu-id="8e588-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="8e588-106">Problem</span><span class="sxs-lookup"><span data-stu-id="8e588-106">Issue</span></span>
* <span data-ttu-id="8e588-107">Problemy, które są wyświetlane toobe spowodowane awarie usługi systemu Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e588-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="8e588-108">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="8e588-108">Causes</span></span>
* <span data-ttu-id="8e588-109">Problemy, które pojawiają się toobe spowodowane Azure Mobile Engagement usługi awarii może być spowodowana przez kilka różnych problemów:</span><span class="sxs-lookup"><span data-stu-id="8e588-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="8e588-110">Izolowane problemy, które pierwotnie pojawiają się tooall systemowe usługi Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8e588-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="8e588-111">Znane problemy spowodowane awarii serwera (nie zawsze pokazuje stan serwera):</span><span class="sxs-lookup"><span data-stu-id="8e588-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="8e588-112">Planowanie opóźnienia, błędy docelowych, problemy aktualizacja wskaźnika, statystyki zatrzymania zbierania wypychania przestanie działać, interfejsu API przestają działać, nowe aplikacje lub użytkowników nie można utworzyć, błędy DNS i błędy przekroczenia limitu czasu w hello aplikacji, interfejsu API lub interfejsu użytkownika na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="8e588-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="8e588-113">Awarie zależności w chmurze [stan usługi Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="8e588-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="8e588-114">Awarie zależności usług (PNS) powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="8e588-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="8e588-115">Awarie sklepu z aplikacjami</span><span class="sxs-lookup"><span data-stu-id="8e588-115">App Store Outages</span></span>

1) <span data-ttu-id="8e588-116">toosee tootest, jeśli hello problem jest systemowych można przetestować hello sam funkcji z innego</span><span class="sxs-lookup"><span data-stu-id="8e588-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="8e588-117">Usługa Azure Mobile Engagement zintegrowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="8e588-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="8e588-118">Urządzenie testowe</span><span class="sxs-lookup"><span data-stu-id="8e588-118">Test device</span></span>
* <span data-ttu-id="8e588-119">Wersja systemu operacyjnego urządzenia testu</span><span class="sxs-lookup"><span data-stu-id="8e588-119">Test device OS version</span></span>
* <span data-ttu-id="8e588-120">Kampanii</span><span class="sxs-lookup"><span data-stu-id="8e588-120">Campaign</span></span>
* <span data-ttu-id="8e588-121">Konta administratora</span><span class="sxs-lookup"><span data-stu-id="8e588-121">Administrator user account</span></span>
* <span data-ttu-id="8e588-122">Przeglądarka (tj., Firefox Chrome, itp.)</span><span class="sxs-lookup"><span data-stu-id="8e588-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="8e588-123">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="8e588-123">Computer</span></span>

2) <span data-ttu-id="8e588-124">tootest Jeśli hello problem wpływa tylko na powitania interfejsu użytkownika lub hello interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="8e588-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="8e588-125">Przetestuj hello sam funkcji z obu hello Azure Mobile Engagement w interfejsie użytkownika i hello Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="8e588-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="8e588-126">tootest, jeśli jest hello problem z siecią telefon komórkowy:</span><span class="sxs-lookup"><span data-stu-id="8e588-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="8e588-127">Testowanie podczas połączonych toohello Internetu za pośrednictwem sieci Wi-Fi i za pośrednictwem sieci 3G telefonu komórkowego.</span><span class="sxs-lookup"><span data-stu-id="8e588-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="8e588-128">Upewnij się, czy Zapora nie blokuje tych portów lub adresy IP hello Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e588-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="8e588-129">tootest, jeśli jest hello problem z urządzeniem:</span><span class="sxs-lookup"><span data-stu-id="8e588-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="8e588-130">Należy sprawdzić, czy urządzenie jest w stanie tooconnect tooAzure Mobile Engagement z innej aplikacji zintegrowane usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e588-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="8e588-131">Test, który może generować zdarzenia, zadań i awarii (Crash) na telefonie, którą można wyświetlić w hello Azure Mobile Engagement w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8e588-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="8e588-132">Sprawdzić, czy można wysyłać powiadomienia wypychane z hello Azure Mobile Engagement UI tooyour urządzenia, zależnie od jego identyfikator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8e588-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="8e588-133">tootest, jeśli jest hello problem z aplikacją:</span><span class="sxs-lookup"><span data-stu-id="8e588-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="8e588-134">Instalowanie i testowanie aplikacji w emulatorze zamiast z fizycznego urządzenia:</span><span class="sxs-lookup"><span data-stu-id="8e588-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="8e588-135">tootest Jeśli hello problem dotyczy użytkownika tooend uaktualnień systemu operacyjnego urządzenia, które wymagają uaktualnienia tooresolve zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="8e588-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="8e588-136">Przetestować aplikację na różnych urządzeniach z różnymi wersjami hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="8e588-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="8e588-137">Upewnij się, że używasz najnowszej wersji hello hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="8e588-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="8e588-138">Łączność i problemy nieprawidłowe informacje</span><span class="sxs-lookup"><span data-stu-id="8e588-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="8e588-139">Problem</span><span class="sxs-lookup"><span data-stu-id="8e588-139">Issue</span></span>
* <span data-ttu-id="8e588-140">Logowanie do problemów hello Azure Mobile Engagement w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8e588-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="8e588-141">Błędy połączenia z hello interfejsu API usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e588-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="8e588-142">Problemy z przekazywaniem tagi informacje o aplikacji za pośrednictwem hello interfejsu API urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8e588-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="8e588-143">Pobieranie dzienników lub wyeksportowanych danych z usługi Azure Mobile Engagement problemów.</span><span class="sxs-lookup"><span data-stu-id="8e588-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="8e588-144">Niepoprawne informacje wyświetlone w hello Azure Mobile Engagement w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8e588-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="8e588-145">Niepoprawne informacje widoczne w dziennikach usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8e588-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="8e588-146">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="8e588-146">Causes</span></span>
* <span data-ttu-id="8e588-147">Upewnij się, że konto użytkownika ma wystarczające uprawnienia tooperform hello zadań.</span><span class="sxs-lookup"><span data-stu-id="8e588-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="8e588-148">Potwierdź, że hello problem nie jest izolowane tooone komputera lub sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="8e588-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="8e588-149">Sprawdź, czy ten hello usługi Azure Mobile Engagement ma nie zgłoszone przerwy w działaniu.</span><span class="sxs-lookup"><span data-stu-id="8e588-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="8e588-150">Upewnij się, czy pliki Tag informacje o aplikacji wykonaj wszystkie te reguły:</span><span class="sxs-lookup"><span data-stu-id="8e588-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="8e588-151">Użyj hello tylko zestaw znaków UTF8 (zestaw znaków ANSI hello nie jest obsługiwane).</span><span class="sxs-lookup"><span data-stu-id="8e588-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="8e588-152">Użyj przecinka "," jako separatora hello (przecinka można otworzyć usługi żądania toorequest toochange hello CSV znak separatora "," znak tooanother, np. średnikiem ";").</span><span class="sxs-lookup"><span data-stu-id="8e588-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="8e588-153">Użyj małe litery logiczna wartości "true" i "false".</span><span class="sxs-lookup"><span data-stu-id="8e588-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="8e588-154">Użyj pliku, który jest mniejszy niż hello maksymalny rozmiar pliku 35 MB.</span><span class="sxs-lookup"><span data-stu-id="8e588-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

