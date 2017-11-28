---
title: "aaaAzure Mobile Engagement Troubleshooting Guide — analiza"
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
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="52eb6-103">Przewodnik rozwiązywania problemów analizy, monitorowanie segmentacji i pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="52eb6-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="52eb6-104">Witaj poniżej przedstawiono możliwe problemy mogą się pojawić w jaki sposób usługi Azure Mobile Engagement zbiera informacje o aplikacji, urządzeń i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="52eb6-104">hello following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="52eb6-105">Brak opóźnione informacji</span><span class="sxs-lookup"><span data-stu-id="52eb6-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="52eb6-106">Problem</span><span class="sxs-lookup"><span data-stu-id="52eb6-106">Issue</span></span>
* <span data-ttu-id="52eb6-107">Informacje o jest opóźnione w znajdujących się w Analytics, segmentacji lub pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="52eb6-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="52eb6-108">Monitorowanie brakuje informacji.</span><span class="sxs-lookup"><span data-stu-id="52eb6-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="52eb6-109">Brakuje informacji Analytics, segmentacji lub pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="52eb6-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="52eb6-110">Naciśnięcie limity segmentacji.</span><span class="sxs-lookup"><span data-stu-id="52eb6-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="52eb6-111">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="52eb6-111">Causes</span></span>
* <span data-ttu-id="52eb6-112">Można użyć hello Analytics API monitora interfejsu API, i toosee segmentów interfejsu API w przypadku wszystkich danych brakuje hello interfejsu użytkownika jest widoczny za pośrednictwem interfejsów API hello.</span><span class="sxs-lookup"><span data-stu-id="52eb6-112">You can use hello Analytics API, Monitor API, and Segments API toosee if any data you are missing from hello UI is visible through hello APIs.</span></span>
* <span data-ttu-id="52eb6-113">Hello Azure Mobile Engagement SDK nie jest poprawnie zintegrowana w aplikacji nie będzie możliwe toosee informacji w hello Analytics segmentacji, monitorowanie i pulpity nawigacyjne.</span><span class="sxs-lookup"><span data-stu-id="52eb6-113">If hello Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able toosee information in hello Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="52eb6-114">Segmenty nie można zmienić po ich utworzeniu, segmentów może być tylko "sklonowane" (skopiowany) lub "zniszczone" (usunięty).</span><span class="sxs-lookup"><span data-stu-id="52eb6-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="52eb6-115">Segmenty może zawierać tylko 10 kryteriów.</span><span class="sxs-lookup"><span data-stu-id="52eb6-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="52eb6-116">Hello najlepsze sposób tootest Brak informacji z monitorowania jest toosetup urządzenie testowe, odinstaluj i/lub ponowne zainstalowanie aplikacji hello na powitania urządzenie testowe.</span><span class="sxs-lookup"><span data-stu-id="52eb6-116">hello best way tootest missing information from monitoring is toosetup a test device, uninstall and/or reinstall hello app on hello test device.</span></span>
* <span data-ttu-id="52eb6-117">Informacje są odświeżane co 24 godziny dla analityka, segmentacji lub pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="52eb6-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="52eb6-118">Informacje zawarte w nowych segmentów mogą być niewidoczne do 24 godzin po ich utworzeniu, nawet jeśli hello segment jest oparta na poprzednich informacji.</span><span class="sxs-lookup"><span data-stu-id="52eb6-118">Information in new segments may not be displayed until 24 hours after they are created even if hello segment is based on previous information.</span></span>
* <span data-ttu-id="52eb6-119">Filtrowanie danych analityka w hello interfejsu użytkownika zostaną wyświetlone wszystkie przykłady tego typu, niezależnie od wersji aplikacji hello (np. "Awarii" przefiltrowane według nazwy zostaną wyświetlone w wersji 1 i aplikacji w wersji 2).</span><span class="sxs-lookup"><span data-stu-id="52eb6-119">Filtering your analytics data in hello UI will show all examples of this type regardless of hello version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="52eb6-120">Hello okresu Analytics jest oparty na hello dat z ustawień urządzenia użytkownika hello, więc użytkownika, którego telefon ma niepoprawnie ustawione Data hello mogą pojawiać się w hello niewłaściwy przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="52eb6-120">hello time period for Analytics is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>
* <span data-ttu-id="52eb6-121">Wypchnięcia nie po stronie serwera, którego dane są rejestrowane, korzystając z przycisku hello zbyt "test", tylko rejestrowane są dane dla kampanie wypychania prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="52eb6-121">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="52eb6-122">Nie można zlokalizować elementów w interfejsie użytkownika</span><span class="sxs-lookup"><span data-stu-id="52eb6-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="52eb6-123">Problem</span><span class="sxs-lookup"><span data-stu-id="52eb6-123">Issue</span></span>
* <span data-ttu-id="52eb6-124">Nie można utworzyć segmenty oparte na niektóre wbudowane lub informacje o aplikacji niestandardowych tagów kryteriów.</span><span class="sxs-lookup"><span data-stu-id="52eb6-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="52eb6-125">Nie można znaleźć niektórych wbudowanych lub informacje o aplikacji niestandardowych tagów kryteria analizy, monitorowanie lub pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="52eb6-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="52eb6-126">Nie można zinterpretować hello danych analizy, monitorowanie, segmentacji lub pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="52eb6-126">Can't interpret hello data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="52eb6-127">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="52eb6-127">Causes</span></span>
* <span data-ttu-id="52eb6-128">Niektóre wbudowane elementy i informacje o aplikacji są dostępne tylko jako kryteriów wypychania tagi, ale może nie być dodane segmentu tooa lub widoczne z analizy, monitorowanie lub pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="52eb6-128">Some built in items and app info tags are only available as push criteria but may not be added tooa segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="52eb6-129">Utworzony w elementy i informacje o aplikacji tagi, których nie można dodać tooa segment, konieczne będzie listy toosetup docelowych kryteriów w każdym hello tooperform kampanii funkcji takie same jak oparte na segment.</span><span class="sxs-lookup"><span data-stu-id="52eb6-129">For built in items and app info tags that can't be added tooa segment, you will need toosetup list of targeting criteria in each campaign tooperform hello same function as targeting based on a segment.</span></span>
* <span data-ttu-id="52eb6-130">Wyświetlić menu kontekstowe hello w sekcjach analizy, monitorowanie segmentacji i pulpity nawigacyjne hello hello Azure Mobile Engagement w interfejsie użytkownika, aby uzyskać dalszą pomoc i w jaki sposób tooinformation.</span><span class="sxs-lookup"><span data-stu-id="52eb6-130">See hello context menus in hello Analytics, Monitoring, Segmentation, and Dashboards sections of hello Azure Mobile Engagement UI for more help and how tooinformation.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="52eb6-131">Awarii, rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="52eb6-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="52eb6-132">Problem</span><span class="sxs-lookup"><span data-stu-id="52eb6-132">Issue</span></span>
* <span data-ttu-id="52eb6-133">Wystąpiła awaria aplikacji znajdujących się w analizy, monitorowanie lub pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="52eb6-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="52eb6-134">Powoduje, że</span><span class="sxs-lookup"><span data-stu-id="52eb6-134">Causes</span></span>
* <span data-ttu-id="52eb6-135">tootroubleshoot aplikacja przestaje działać w analizy, monitorowanie lub pulpit nawigacyjny upewnij się, że informacje o wersji hello toocheck pod kątem znanych problemów z poprzednimi wersjami hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="52eb6-135">tootroubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure toocheck hello release notes for known issues with previous versions of hello SDK.</span></span>
* <span data-ttu-id="52eb6-136">toofurther Rozwiązywanie problemów z aplikacji awarii wykonaj zdarzenia z urządzeniem testu z zainstalowania aplikacji i wyszukać identyfikator urządzenia w sekcji hello "Monitor — zdarzenia" hello Azure Mobile Engagement w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="52eb6-136">toofurther troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in hello “Monitor – Events” section of hello Azure Mobile Engagement UI.</span></span> <span data-ttu-id="52eb6-137">Następnie wykonaj hello zdarzenie, które powoduje toocrash Twojej aplikacji i wyszukiwania dodatkowych informacji w hello sekcji "Monitor awarii —" hello Azure Mobile Engagement w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="52eb6-137">Then perform hello event that is causing your application toocrash and look up additional information in hello “Monitor – Crash” section of hello Azure Mobile Engagement UI.</span></span> 

