---
title: aaaAzure Mobile Engagement Android SDK integracji
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK systemu Android dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a><span data-ttu-id="2e4a0-103">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="2e4a0-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="2e4a0-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="2e4a0-105">Usuń awarii rzadko może się zdarzyć podczas wywoływania metody `EngagementAgentUtils.isInDedicatedEngagementProcess`, która jest już używana przez hello `EngagementApplication` klasy.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="2e4a0-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="2e4a0-107">Obsługa 8 systemu android (poprzednie wersje powitalne zestawu SDK nie będą działać na 8 dla systemu Android).</span><span class="sxs-lookup"><span data-stu-id="2e4a0-107">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="2e4a0-108">Nie więcej zależności biblioteki pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-108">No more dependency on support library.</span></span>
* <span data-ttu-id="2e4a0-109">Usuń `EngagementFragmentActivity` klasy.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="2e4a0-110">Z powodu zbyt[limity wykonywania tła](https://developer.android.com/preview/features/background.html) na 8 dla systemu Android, dzienniki w tle mogą zostać opóźnione aż hello użytkownik wchodzi w interakcję z urządzeniem hello, będzie to mieć wpływ na Push kampanii **dostarczone** i **Powiadomienie systemowe wyświetlane** statystyki opóźnieniu, jeśli został uśpiony hello urządzenia (hello powiadomienia będą nadal wyświetlane, będzie pierścienia i Włącz wibrację w czasie rzeczywistym bez problemów).</span><span class="sxs-lookup"><span data-stu-id="2e4a0-110">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="2e4a0-111">Z powodu zbyt[ograniczenia lokalizacji tła](https://developer.android.com/preview/features/background-location-limits.html), hello czasu rzeczywistego lokalizacji w tle nie zostanie zaktualizowany często na 8 dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-111">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="2e4a0-112">4.2.4 (03/30/2017)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="2e4a0-113">Napraw powiadomień w aplikacji koloru tekstu na toobe Android 7 hello takie same jak starsze wersje systemu Android.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-113">Fix in-app notification text colors on Android 7 toobe hello same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="2e4a0-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="2e4a0-115">Więcej blokady sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-115">No more WIFI lock.</span></span>
* <span data-ttu-id="2e4a0-116">Usuń zakleszczenie podczas wywoływania metody getDeviceId przed init (wprowadzona w 4.2.0 błędów).</span><span class="sxs-lookup"><span data-stu-id="2e4a0-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="2e4a0-117">4.2.2 (05/17/2016)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="2e4a0-118">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="2e4a0-119">4.2.1 (05/10/2016)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="2e4a0-120">Zabezpieczenia: Wyłącz dostęp do pliku lokalnego widoku sieci web.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="2e4a0-121">Security: usunąć `EngagementPreferenceActivity` klasy, która rozszerza przestarzałe i niezabezpieczone `PreferenceActivity` klasy.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="2e4a0-122">Zabezpieczenia: reach działania są teraz udokumentowane toouse `exported="false"`, ta flaga umożliwia również w poprzednich wersjach zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-122">Security: reach activities are now documented toouse `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="2e4a0-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="2e4a0-124">Witaj zestawu SDK jest teraz licencją MIT.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-124">hello SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="2e4a0-125">Pozwala na stosowanie identyfikator urządzeń niestandardowych w czasie inicjowania zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="2e4a0-126">4.1.5 (02/01/2016)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="2e4a0-127">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="2e4a0-128">4.1.4 (01/26/2016)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="2e4a0-129">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="2e4a0-130">4.1.3 (12/9/2015)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="2e4a0-131">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="2e4a0-132">4.1.2 (11/25/2015)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="2e4a0-133">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="2e4a0-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="2e4a0-135">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="2e4a0-136">4.1.0 (08/25/2015)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="2e4a0-137">Obsługa nowego modelu uprawnień dla systemu Android M.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="2e4a0-138">Można teraz skonfigurować funkcje lokalizacji w czasie wykonywania, zamiast `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="2e4a0-139">Naprawa błędów uprawnienie: Jeśli używasz `ACCESS_FINE_LOCATION`, następnie `ACCESS_COARSE_LOCATION` nie jest już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="2e4a0-140">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="2e4a0-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="2e4a0-142">Wewnętrzny protokołu zmienia toomake analytics i bardziej niezawodny wypychania.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-142">Internal protocol changes toomake analytics and push more reliable.</span></span>
* <span data-ttu-id="2e4a0-143">Natywnych powiadomień wypychanych (GCM/ADM) teraz służy także do w powiadomieniach wewnętrznych aplikacji, musisz skonfigurować poświadczenia natywnych powiadomień wypychanych powitania dla dowolnego typu wypychania kampanii.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="2e4a0-144">Usuń powiadomień szerszej: były wyświetlane tylko 10s po przekazywanej.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="2e4a0-145">Naprawa błędów w widoku sieci web: kliknięcie łącza również wykonywania hello będzie domyślny adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-145">Fix a bug in web view: clicking on a link was also executing hello default action URL.</span></span>
* <span data-ttu-id="2e4a0-146">Usuń rzadkich awarii powiązane toolocal zarządzania magazynem.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-146">Fix a rare crash related toolocal storage management.</span></span>
* <span data-ttu-id="2e4a0-147">Napraw zarządzania ciągu konfiguracji dynamicznej.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="2e4a0-148">Zaktualizuj umowy licencyjnej.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="2e4a0-149">3.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="2e4a0-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="2e4a0-150">Początkowa wersja usługi Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2e4a0-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="2e4a0-151">Konfiguracja appId zastępuje konfigurację ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="2e4a0-152">Usunięte toosend interfejsu API i odbieranie komunikatów XMPP dowolnego z dowolnego XMPP jednostek.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-152">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="2e4a0-153">Usunięte toosend interfejsu API i odbierania wiadomości między urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-153">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="2e4a0-154">Ulepszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-154">Security improvements.</span></span>
* <span data-ttu-id="2e4a0-155">Śledzenie Google Play i SmartAd usunięte.</span><span class="sxs-lookup"><span data-stu-id="2e4a0-155">Google Play and SmartAd tracking removed.</span></span>

