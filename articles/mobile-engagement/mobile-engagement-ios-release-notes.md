---
title: aaaAzure Mobile Engagement iOS SDK informacje o wersji | Dokumentacja firmy Microsoft
description: "Najnowsze aktualizacje i procedury dla systemu iOS SDK dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="4574d-103">Informacje o wersji usługi Azure Mobile Engagement iOS SDK</span><span class="sxs-lookup"><span data-stu-id="4574d-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="4574d-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="4574d-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="4574d-105">Identyfikatory stałych wyczyszczone w tle.</span><span class="sxs-lookup"><span data-stu-id="4574d-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="4574d-106">Stałe ostrzeżenia na 9 XCode o interfejsach API nie jest wywoływana w kolejki głównej.</span><span class="sxs-lookup"><span data-stu-id="4574d-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="4574d-107">Stała sond Reach przeciek pamięci.</span><span class="sxs-lookup"><span data-stu-id="4574d-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="4574d-108">Obsługę systemu iOS usunąć 6.X.</span><span class="sxs-lookup"><span data-stu-id="4574d-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="4574d-109">Począwszy od ten cel wdrożenia hello wersji aplikacji musi mieć co najmniej system iOS 7.</span><span class="sxs-lookup"><span data-stu-id="4574d-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="4574d-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="4574d-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="4574d-111">Ulepszona dostarczania dziennika w tle.</span><span class="sxs-lookup"><span data-stu-id="4574d-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="4574d-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="4574d-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="4574d-113">Stałe powiadomienie nie których wykonano akcje na urządzeniach z systemem iOS 10.</span><span class="sxs-lookup"><span data-stu-id="4574d-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="4574d-114">Zastąpić XCode 7.</span><span class="sxs-lookup"><span data-stu-id="4574d-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="4574d-115">3.2.4 (06/30/2016)</span><span class="sxs-lookup"><span data-stu-id="4574d-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="4574d-116">Stałe agregacji między dzienniki techniczne i inne dzienniki.</span><span class="sxs-lookup"><span data-stu-id="4574d-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="4574d-117">3.2.3 (06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="4574d-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="4574d-118">Gdzie dostarczanie opinii nie został zgłoszony, gdy aplikacja jest w tle hello usterki hello stałym.</span><span class="sxs-lookup"><span data-stu-id="4574d-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="4574d-119">Zoptymalizowane hello wysyłania dzienników technicznych.</span><span class="sxs-lookup"><span data-stu-id="4574d-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="4574d-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="4574d-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="4574d-121">Usunięte usterki w anulowania żądania HTTP, która czasami prowadzi toocrash.</span><span class="sxs-lookup"><span data-stu-id="4574d-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="4574d-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="4574d-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="4574d-123">Opóźnienie hello stałej, gdy nowe wystąpienie aplikacji jest wyzwalana przez powiadomienie dotyczące linków bezpośrednich</span><span class="sxs-lookup"><span data-stu-id="4574d-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="4574d-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="4574d-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="4574d-125">Włączone kodu bitowego w toomake SDK hello działać z **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="4574d-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="4574d-126">Usunięte usterki powiązanych aplikacji tooin powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="4574d-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="4574d-127">Wprowadzone powiadomienia w aplikacji hello bardziej niezawodna w przypadku niskim poziomie naładowania baterii i innych takich scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="4574d-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="4574d-128">Usunąć dodatkowe konsoli dzienniki generowane przez 3 biblioteki strony.</span><span class="sxs-lookup"><span data-stu-id="4574d-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="4574d-129">3.1.0 (08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="4574d-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="4574d-130">Napraw błąd zgodności z systemem iOS 9 z biblioteką innych firm.</span><span class="sxs-lookup"><span data-stu-id="4574d-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="4574d-131">Została ona powoduje awarii (Crash) podczas wysyłania sonduje wyników, informacje o aplikacji lub dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="4574d-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="4574d-132">3.0.0 (06/19/2015)</span><span class="sxs-lookup"><span data-stu-id="4574d-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="4574d-133">Usługa Mobile Engagement używa cichych powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="4574d-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="4574d-134">Obsługę systemu iOS usunąć 4.X.</span><span class="sxs-lookup"><span data-stu-id="4574d-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="4574d-135">Począwszy od ten cel wdrożenia hello wersji aplikacji musi mieć co najmniej iOS 6.</span><span class="sxs-lookup"><span data-stu-id="4574d-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="4574d-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="4574d-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="4574d-137">Identyfikator urządzenia usługi Mobile Engagement Hello urządzeń < iOS 6 teraz opiera się na identyfikator GUID generowany podczas instalacji.</span><span class="sxs-lookup"><span data-stu-id="4574d-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="4574d-138">2.1.0 (04/24/2015)</span><span class="sxs-lookup"><span data-stu-id="4574d-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="4574d-139">Dodano Swift zgodności.</span><span class="sxs-lookup"><span data-stu-id="4574d-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="4574d-140">Po kliknięciu przycisku na powiadomienie, akcji hello adres URL jest teraz wykonywane prawo po otwarciu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4574d-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="4574d-141">Dodano brakujący plik nagłówka w pakiecie SDK.</span><span class="sxs-lookup"><span data-stu-id="4574d-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="4574d-142">Rozwiązano problem przy wyłączonej osoby zgłaszającej awarii usługi Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="4574d-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="4574d-143">2.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="4574d-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="4574d-144">Początkowa wersja usługi Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4574d-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="4574d-145">Konfiguracja appId/sdkKey zastępuje konfigurację ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="4574d-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="4574d-146">Usunięte toosend interfejsu API i odbieranie komunikatów XMPP dowolnego z dowolnego XMPP jednostek.</span><span class="sxs-lookup"><span data-stu-id="4574d-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="4574d-147">Usunięte toosend interfejsu API i odbierania wiadomości między urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="4574d-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="4574d-148">Ulepszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4574d-148">Security improvements.</span></span>
* <span data-ttu-id="4574d-149">Śledzenie SmartAd usunięte.</span><span class="sxs-lookup"><span data-stu-id="4574d-149">SmartAd tracking removed.</span></span>
