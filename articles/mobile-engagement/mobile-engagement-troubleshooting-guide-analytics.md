---
title: "Usługi Azure Mobile Engagement przewodnik - Analytics rozwiązywania problemów"
description: "Rozwiązywanie problemów analizy, monitorowanie segmentacji i pulpit nawigacyjny w usłudze Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="f571c-103">Przewodnik rozwiązywania problemów analizy, monitorowanie segmentacji i pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="f571c-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="f571c-104">Poniżej przedstawiono możliwe problemy mogą się pojawić w jaki sposób usługi Azure Mobile Engagement zbiera informacje o aplikacji, urządzeń i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f571c-104">The following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="f571c-105">Brak opóźnione informacji</span><span class="sxs-lookup"><span data-stu-id="f571c-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="f571c-106">Problem</span><span class="sxs-lookup"><span data-stu-id="f571c-106">Issue</span></span>
* <span data-ttu-id="f571c-107">Informacje o jest opóźnione w znajdujących się w Analytics, segmentacji lub pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f571c-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="f571c-108">Monitorowanie brakuje informacji.</span><span class="sxs-lookup"><span data-stu-id="f571c-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="f571c-109">Brakuje informacji Analytics, segmentacji lub pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f571c-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="f571c-110">Naciśnięcie limity segmentacji.</span><span class="sxs-lookup"><span data-stu-id="f571c-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="f571c-111">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="f571c-111">Causes</span></span>
* <span data-ttu-id="f571c-112">Można użyć interfejsu API Analytics API monitora i segmentów API, aby sprawdzić, czy wszystkie dane można w Interfejsie brak jest widoczny za pośrednictwem interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="f571c-112">You can use the Analytics API, Monitor API, and Segments API to see if any data you are missing from the UI is visible through the APIs.</span></span>
* <span data-ttu-id="f571c-113">Jeśli zestaw SDK usługi Azure Mobile Engagement nie został poprawnie zintegrowany ze aplikacji nie będzie można zobaczyć informacje w Analytics, segmentacji, monitorowanie i pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="f571c-113">If the Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able to see information in the Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="f571c-114">Segmenty nie można zmienić po ich utworzeniu, segmentów może być tylko "sklonowane" (skopiowany) lub "zniszczone" (usunięty).</span><span class="sxs-lookup"><span data-stu-id="f571c-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="f571c-115">Segmenty może zawierać tylko 10 kryteriów.</span><span class="sxs-lookup"><span data-stu-id="f571c-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="f571c-116">Najlepszym sposobem sprawdzenia brakujące informacje z monitorowania jest skonfigurować urządzenie testu, odinstaluj i/lub zainstaluj ponownie aplikację na urządzeniu testu.</span><span class="sxs-lookup"><span data-stu-id="f571c-116">The best way to test missing information from monitoring is to setup a test device, uninstall and/or reinstall the app on the test device.</span></span>
* <span data-ttu-id="f571c-117">Informacje są odświeżane co 24 godziny dla analityka, segmentacji lub pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="f571c-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="f571c-118">Informacje zawarte w nowych segmentów mogą być niewidoczne do 24 godzin po ich utworzeniu, nawet jeśli segment jest oparta na poprzednich informacji.</span><span class="sxs-lookup"><span data-stu-id="f571c-118">Information in new segments may not be displayed until 24 hours after they are created even if the segment is based on previous information.</span></span>
* <span data-ttu-id="f571c-119">Filtrowanie danych analityka w interfejsie użytkownika zostaną wyświetlone wszystkie przykłady tego typu, niezależnie od wersji aplikacji (np. "Awarii" przefiltrowane według nazwy zostaną wyświetlone w wersji 1 i aplikacji w wersji 2).</span><span class="sxs-lookup"><span data-stu-id="f571c-119">Filtering your analytics data in the UI will show all examples of this type regardless of the version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="f571c-120">Okres czasu w celu wykonania analizy opiera się na datę z ustawień urządzeń użytkowników, dlatego użytkownik, którego telefon ma niepoprawnie ustawione Data mogą pojawiać się w przedziale czasu niewłaściwy.</span><span class="sxs-lookup"><span data-stu-id="f571c-120">The time period for Analytics is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>
* <span data-ttu-id="f571c-121">Wypchnięcia nie po stronie serwera, które dane są rejestrowane, korzystając z przycisku do "test", tylko rejestrowane są dane dla kampanie wypychania prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f571c-121">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="f571c-122">Nie można zlokalizować elementów w interfejsie użytkownika</span><span class="sxs-lookup"><span data-stu-id="f571c-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="f571c-123">Problem</span><span class="sxs-lookup"><span data-stu-id="f571c-123">Issue</span></span>
* <span data-ttu-id="f571c-124">Nie można utworzyć segmenty oparte na niektóre wbudowane lub informacje o aplikacji niestandardowych tagów kryteriów.</span><span class="sxs-lookup"><span data-stu-id="f571c-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="f571c-125">Nie można znaleźć niektórych wbudowanych lub informacje o aplikacji niestandardowych tagów kryteria analizy, monitorowanie lub pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="f571c-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="f571c-126">Nie można zinterpretować dane analizy, monitorowanie, segmentacji lub pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="f571c-126">Can't interpret the data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="f571c-127">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="f571c-127">Causes</span></span>
* <span data-ttu-id="f571c-128">Niektóre wbudowane elementy i tagi informacje o aplikacji są dostępne tylko jako kryteriów wypychania, ale nie może być dodany do segmentu lub widoczne z analizy, monitorowanie lub pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f571c-128">Some built in items and app info tags are only available as push criteria but may not be added to a segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="f571c-129">Wbudowane elementów i tagi informacje o aplikacji, których nie można dodać do segmentu należy do listy konfiguracji docelowych kryteriów w każdej kampanii wykonać taką samą funkcję jak oparte na segment.</span><span class="sxs-lookup"><span data-stu-id="f571c-129">For built in items and app info tags that can't be added to a segment, you will need to setup list of targeting criteria in each campaign to perform the same function as targeting based on a segment.</span></span>
* <span data-ttu-id="f571c-130">Wyświetlić menu kontekstowe w sekcjach analizy, monitorowanie segmentacji i pulpitów nawigacyjnych usługi Azure Mobile Engagement interfejs użytkownika więcej pomocy i informacje.</span><span class="sxs-lookup"><span data-stu-id="f571c-130">See the context menus in the Analytics, Monitoring, Segmentation, and Dashboards sections of the Azure Mobile Engagement UI for more help and how to information.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="f571c-131">Awarii, rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="f571c-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="f571c-132">Problem</span><span class="sxs-lookup"><span data-stu-id="f571c-132">Issue</span></span>
* <span data-ttu-id="f571c-133">Wystąpiła awaria aplikacji znajdujących się w analizy, monitorowanie lub pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f571c-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="f571c-134">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="f571c-134">Causes</span></span>
* <span data-ttu-id="f571c-135">Aby rozwiązać aplikacja przestaje działać w analizy, monitorowanie lub pulpit nawigacyjny upewnij się, że Sprawdź informacje o wersji pod kątem znanych problemów w poprzednich wersjach zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="f571c-135">To troubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure to check the release notes for known issues with previous versions of the SDK.</span></span>
* <span data-ttu-id="f571c-136">Aby kontynuować rozwiązywanie awarii aplikacji wykonaj zdarzenia z urządzenia testu z zainstalowania aplikacji i wyszukiwanie w sekcji "Monitor zdarzeń —" interfejsu użytkownika usługi Azure Mobile Engagement identyfikator urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f571c-136">To further troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in the “Monitor – Events” section of the Azure Mobile Engagement UI.</span></span> <span data-ttu-id="f571c-137">Następnie wykonaj zdarzenia, które powoduje aplikacji do awarii i poszukaj dodatkowych informacji w sekcji "Awarii — Monitor" interfejsu użytkownika usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f571c-137">Then perform the event that is causing your application to crash and look up additional information in the “Monitor – Crash” section of the Azure Mobile Engagement UI.</span></span> 

