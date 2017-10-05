---
title: "Integracja zestawu SDK systemu Android z usługi Azure Mobile Engagement"
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
ms.openlocfilehash: c179c39a43da0aa35e945acceacbf27fe8e328f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="d548b-103">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="d548b-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="d548b-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="d548b-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="d548b-105">Usuń awarii rzadko może się zdarzyć podczas wywoływania metody `EngagementAgentUtils.isInDedicatedEngagementProcess`, która jest już używana przez `EngagementApplication` klasy.</span><span class="sxs-lookup"><span data-stu-id="d548b-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="d548b-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="d548b-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="d548b-107">8 Obsługa systemu android (poprzednie wersje zestawu SDK nie będą działać na 8 dla systemu Android).</span><span class="sxs-lookup"><span data-stu-id="d548b-107">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="d548b-108">Nie więcej zależności biblioteki pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="d548b-108">No more dependency on support library.</span></span>
* <span data-ttu-id="d548b-109">Usuń `EngagementFragmentActivity` klasy.</span><span class="sxs-lookup"><span data-stu-id="d548b-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="d548b-110">Ze względu na [limity wykonywania tła](https://developer.android.com/preview/features/background.html) na 8 dla systemu Android, może być opóźnione dzienniki w tle, dopóki użytkownik wchodzi w interakcję z urządzeniem, będzie to mieć wpływ na Push kampanii **dostarczone** i **powiadomienie systemowe wyświetlane** statystyki opóźnieniu, jeśli urządzenie zostało uśpiony (powiadomienia będą nadal wyświetlane, będzie pierścienia i Włącz wibrację w czasie rzeczywistym bez problemów).</span><span class="sxs-lookup"><span data-stu-id="d548b-110">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="d548b-111">Ze względu na [ograniczenia lokalizacji tła](https://developer.android.com/preview/features/background-location-limits.html), w czasie rzeczywistym lokalizacji w tle nie zostanie zaktualizowany często na 8 dla systemu Android.</span><span class="sxs-lookup"><span data-stu-id="d548b-111">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="d548b-112">4.2.4 (03/30/2017)</span><span class="sxs-lookup"><span data-stu-id="d548b-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="d548b-113">Usuń powiadomienie w aplikacji koloru tekstu na 7 dla systemu Android, aby być taka sama jak starsze wersje systemu Android.</span><span class="sxs-lookup"><span data-stu-id="d548b-113">Fix in-app notification text colors on Android 7 to be the same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="d548b-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="d548b-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="d548b-115">Więcej blokady sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="d548b-115">No more WIFI lock.</span></span>
* <span data-ttu-id="d548b-116">Usuń zakleszczenie podczas wywoływania metody getDeviceId przed init (wprowadzona w 4.2.0 błędów).</span><span class="sxs-lookup"><span data-stu-id="d548b-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="d548b-117">4.2.2 (05/17/2016)</span><span class="sxs-lookup"><span data-stu-id="d548b-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="d548b-118">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="d548b-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="d548b-119">4.2.1 (05/10/2016)</span><span class="sxs-lookup"><span data-stu-id="d548b-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="d548b-120">Zabezpieczenia: Wyłącz dostęp do pliku lokalnego widoku sieci web.</span><span class="sxs-lookup"><span data-stu-id="d548b-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="d548b-121">Security: usunąć `EngagementPreferenceActivity` klasy, która rozszerza przestarzałe i niezabezpieczone `PreferenceActivity` klasy.</span><span class="sxs-lookup"><span data-stu-id="d548b-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="d548b-122">Zabezpieczenia: reach działania jest udokumentowany do użycia `exported="false"`, ta flaga umożliwia również w poprzednich wersjach zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="d548b-122">Security: reach activities are now documented to use `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="d548b-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="d548b-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="d548b-124">Zestaw SDK jest teraz licencją MIT.</span><span class="sxs-lookup"><span data-stu-id="d548b-124">The SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="d548b-125">Pozwala na stosowanie identyfikator urządzeń niestandardowych w czasie inicjowania zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="d548b-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="d548b-126">4.1.5 (02/01/2016)</span><span class="sxs-lookup"><span data-stu-id="d548b-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="d548b-127">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="d548b-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="d548b-128">4.1.4 (01/26/2016)</span><span class="sxs-lookup"><span data-stu-id="d548b-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="d548b-129">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="d548b-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="d548b-130">4.1.3 (12/9/2015)</span><span class="sxs-lookup"><span data-stu-id="d548b-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="d548b-131">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="d548b-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="d548b-132">4.1.2 (11/25/2015)</span><span class="sxs-lookup"><span data-stu-id="d548b-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="d548b-133">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="d548b-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="d548b-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="d548b-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="d548b-135">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="d548b-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="d548b-136">4.1.0 (08/25/2015)</span><span class="sxs-lookup"><span data-stu-id="d548b-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="d548b-137">Obsługa nowego modelu uprawnień dla systemu Android M.</span><span class="sxs-lookup"><span data-stu-id="d548b-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="d548b-138">Można teraz skonfigurować funkcje lokalizacji w czasie wykonywania, zamiast `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="d548b-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="d548b-139">Naprawa błędów uprawnienie: Jeśli używasz `ACCESS_FINE_LOCATION`, następnie `ACCESS_COARSE_LOCATION` nie jest już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="d548b-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="d548b-140">Ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="d548b-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="d548b-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="d548b-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="d548b-142">Protokół zmiany, aby analiza i wypychania bardziej niezawodne.</span><span class="sxs-lookup"><span data-stu-id="d548b-142">Internal protocol changes to make analytics and push more reliable.</span></span>
* <span data-ttu-id="d548b-143">Natywnych powiadomień wypychanych (GCM/ADM) teraz służy także do w powiadomieniach wewnętrznych aplikacji, musisz skonfigurować poświadczenia natywnych powiadomień wypychanych dla dowolnego typu wypychania kampanii.</span><span class="sxs-lookup"><span data-stu-id="d548b-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="d548b-144">Usuń powiadomień szerszej: były wyświetlane tylko 10s po przekazywanej.</span><span class="sxs-lookup"><span data-stu-id="d548b-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="d548b-145">Naprawa błędów w widoku sieci web: kliknięcie łącza powodowała również domyślny adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="d548b-145">Fix a bug in web view: clicking on a link was also executing the default action URL.</span></span>
* <span data-ttu-id="d548b-146">Napraw rzadkich awarii związanych z zarządzaniem lokalnej pamięci masowej.</span><span class="sxs-lookup"><span data-stu-id="d548b-146">Fix a rare crash related to local storage management.</span></span>
* <span data-ttu-id="d548b-147">Napraw zarządzania ciągu konfiguracji dynamicznej.</span><span class="sxs-lookup"><span data-stu-id="d548b-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="d548b-148">Zaktualizuj umowy licencyjnej.</span><span class="sxs-lookup"><span data-stu-id="d548b-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="d548b-149">3.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="d548b-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="d548b-150">Początkowa wersja usługi Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d548b-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="d548b-151">Konfiguracja appId zastępuje konfigurację ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="d548b-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="d548b-152">Usunięto interfejs API do wysyłania i odbierania wiadomości XMPP dowolnego z dowolnego XMPP jednostek.</span><span class="sxs-lookup"><span data-stu-id="d548b-152">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="d548b-153">Usunięto interfejs API do wysyłania i odbierania wiadomości między urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="d548b-153">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="d548b-154">Ulepszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d548b-154">Security improvements.</span></span>
* <span data-ttu-id="d548b-155">Śledzenie Google Play i SmartAd usunięte.</span><span class="sxs-lookup"><span data-stu-id="d548b-155">Google Play and SmartAd tracking removed.</span></span>

