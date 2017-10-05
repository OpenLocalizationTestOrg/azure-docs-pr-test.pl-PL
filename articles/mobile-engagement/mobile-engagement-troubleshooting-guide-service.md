---
title: "Usługi Azure Mobile Engagement przewodnik — usługa rozwiązywania problemów"
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
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="25d27-103">Przewodnik rozwiązywania problemów dotyczących usługi</span><span class="sxs-lookup"><span data-stu-id="25d27-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="25d27-104">Poniżej przedstawiono możliwe problemy, które mogą się pojawić w sposób uruchamiania usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="25d27-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="25d27-105">Awarie usługi</span><span class="sxs-lookup"><span data-stu-id="25d27-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="25d27-106">Problem</span><span class="sxs-lookup"><span data-stu-id="25d27-106">Issue</span></span>
* <span data-ttu-id="25d27-107">Problemy, które wydają się być spowodowane awarie usługi systemu Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="25d27-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="25d27-108">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="25d27-108">Causes</span></span>
* <span data-ttu-id="25d27-109">Problemy, które wydają się być spowodowane przez usługi Azure Mobile Engagement usługi awarii może być spowodowana przez kilka różnych problemów:</span><span class="sxs-lookup"><span data-stu-id="25d27-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="25d27-110">Izolowane problemy, które pierwotnie pojawiają się systemowych do wszystkich usługi Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="25d27-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="25d27-111">Znane problemy spowodowane awarii serwera (nie zawsze pokazuje stan serwera):</span><span class="sxs-lookup"><span data-stu-id="25d27-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="25d27-112">Planowanie opóźnienia, błędy docelowych, problemy aktualizacja wskaźnika, statystyki zatrzymania zbierania wypychania przestanie działać, interfejsu API przestają działać, nowe aplikacje lub użytkowników nie można utworzyć, błędy DNS i błędy przekroczenia limitu czasu w aplikacji interfejsu użytkownika, interfejsu API lub na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="25d27-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="25d27-113">Awarie zależności w chmurze [stan usługi Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="25d27-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="25d27-114">Awarie zależności usług (PNS) powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="25d27-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="25d27-115">Awarie sklepu z aplikacjami</span><span class="sxs-lookup"><span data-stu-id="25d27-115">App Store Outages</span></span>

1) <span data-ttu-id="25d27-116">Aby test, aby sprawdzić, czy problem jest systemowych można przetestować tej samej funkcji z innego</span><span class="sxs-lookup"><span data-stu-id="25d27-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="25d27-117">Usługa Azure Mobile Engagement zintegrowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="25d27-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="25d27-118">Urządzenie testowe</span><span class="sxs-lookup"><span data-stu-id="25d27-118">Test device</span></span>
* <span data-ttu-id="25d27-119">Wersja systemu operacyjnego urządzenia testu</span><span class="sxs-lookup"><span data-stu-id="25d27-119">Test device OS version</span></span>
* <span data-ttu-id="25d27-120">Kampanii</span><span class="sxs-lookup"><span data-stu-id="25d27-120">Campaign</span></span>
* <span data-ttu-id="25d27-121">Konta administratora</span><span class="sxs-lookup"><span data-stu-id="25d27-121">Administrator user account</span></span>
* <span data-ttu-id="25d27-122">Przeglądarka (tj., Firefox Chrome, itp.)</span><span class="sxs-lookup"><span data-stu-id="25d27-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="25d27-123">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="25d27-123">Computer</span></span>

2) <span data-ttu-id="25d27-124">Aby sprawdzić, czy problem dotyczy tylko interfejsu użytkownika lub interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="25d27-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="25d27-125">Przetestuj tę samą funkcję z interfejsu użytkownika usługi Azure Mobile Engagement i Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="25d27-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="25d27-126">Aby sprawdzić, czy problem dotyczy sieci telefon komórkowy:</span><span class="sxs-lookup"><span data-stu-id="25d27-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="25d27-127">Testowanie podczas połączenia z Internetem za pośrednictwem sieci Wi-Fi i za pośrednictwem sieci 3G telefonu komórkowego.</span><span class="sxs-lookup"><span data-stu-id="25d27-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="25d27-128">Upewnij się, że Zapora nie blokuje Azure Mobile Engagement adresy i porty.</span><span class="sxs-lookup"><span data-stu-id="25d27-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="25d27-129">Aby sprawdzić, czy problem dotyczy urządzenia:</span><span class="sxs-lookup"><span data-stu-id="25d27-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="25d27-130">Należy sprawdzić, czy urządzenie jest w stanie nawiązać połączenia z usługi Azure Mobile Engagement z innej aplikacji zintegrowane usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="25d27-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="25d27-131">Test, który może generować zdarzenia, zadań i awarii (Crash) na telefonie, które są widoczne w Interfejsie użytkownika usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="25d27-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="25d27-132">Sprawdzić, czy można wysyłać powiadomienia wypychane w interfejsie użytkownika usługi Azure Mobile Engagement na urządzenie oparte na jej identyfikator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="25d27-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="25d27-133">Aby sprawdzić, czy problem dotyczy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="25d27-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="25d27-134">Instalowanie i testowanie aplikacji w emulatorze zamiast z fizycznego urządzenia:</span><span class="sxs-lookup"><span data-stu-id="25d27-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="25d27-135">Aby sprawdzić, czy problem dotyczy uaktualnień systemu operacyjnego dla użytkownika końcowego urządzeń, które wymagają uaktualnienia zestawu SDK do rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="25d27-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="25d27-136">Przetestować aplikację na różnych urządzeniach z różnymi wersjami systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="25d27-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="25d27-137">Upewnij się, że używasz najnowszej wersji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="25d27-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="25d27-138">Łączność i problemy nieprawidłowe informacje</span><span class="sxs-lookup"><span data-stu-id="25d27-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="25d27-139">Problem</span><span class="sxs-lookup"><span data-stu-id="25d27-139">Issue</span></span>
* <span data-ttu-id="25d27-140">Problemy z logowania w Interfejsie użytkownika usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="25d27-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="25d27-141">Błędy połączenia z Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="25d27-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="25d27-142">Problemy z przekazywaniem tagi informacje o aplikacji za pomocą interfejsu API urządzenia.</span><span class="sxs-lookup"><span data-stu-id="25d27-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="25d27-143">Pobieranie dzienników lub wyeksportowanych danych z usługi Azure Mobile Engagement problemów.</span><span class="sxs-lookup"><span data-stu-id="25d27-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="25d27-144">Nieprawidłowe informacje wyświetlane w Interfejsie użytkownika usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="25d27-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="25d27-145">Niepoprawne informacje widoczne w dziennikach usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="25d27-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="25d27-146">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="25d27-146">Causes</span></span>
* <span data-ttu-id="25d27-147">Upewnij się, że konto użytkownika ma wystarczające uprawnienia do wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="25d27-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="25d27-148">Upewnij się, że problem nie jest izolowane do jednego komputera lub sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="25d27-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="25d27-149">Upewnij się, że nie ma usługi Azure Mobile Engagement zgłoszone awarii.</span><span class="sxs-lookup"><span data-stu-id="25d27-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="25d27-150">Upewnij się, czy pliki Tag informacje o aplikacji wykonaj wszystkie te reguły:</span><span class="sxs-lookup"><span data-stu-id="25d27-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="25d27-151">Użyj tylko zestaw znaków UTF8 (zestaw znaków ANSI nie jest obsługiwane).</span><span class="sxs-lookup"><span data-stu-id="25d27-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="25d27-152">Użyj przecinka "," jako znak separatora (można otworzyć usługi do żądania zmiany znak separatora CSV ze przecinek "," do innego znaku, np. średnikiem ";").</span><span class="sxs-lookup"><span data-stu-id="25d27-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="25d27-153">Użyj małe litery logiczna wartości "true" i "false".</span><span class="sxs-lookup"><span data-stu-id="25d27-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="25d27-154">Używany plik, który jest mniejszy niż maksymalny rozmiar pliku 35 MB.</span><span class="sxs-lookup"><span data-stu-id="25d27-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

