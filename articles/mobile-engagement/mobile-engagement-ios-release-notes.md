---
title: Azure Mobile Engagement iOS SDK informacje o wersji | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 9bdaa57f9902373ccf796ff109332b64c66bf9e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="f7555-103">Informacje o wersji usługi Azure Mobile Engagement iOS SDK</span><span class="sxs-lookup"><span data-stu-id="f7555-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="f7555-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="f7555-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="f7555-105">Identyfikatory stałych wyczyszczone w tle.</span><span class="sxs-lookup"><span data-stu-id="f7555-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="f7555-106">Stałe ostrzeżenia na 9 XCode o interfejsach API nie jest wywoływana w kolejki głównej.</span><span class="sxs-lookup"><span data-stu-id="f7555-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="f7555-107">Stała sond Reach przeciek pamięci.</span><span class="sxs-lookup"><span data-stu-id="f7555-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="f7555-108">Obsługę systemu iOS usunąć 6.X.</span><span class="sxs-lookup"><span data-stu-id="f7555-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="f7555-109">Począwszy od tej wersji cel wdrożenia aplikacji musi mieć co najmniej system iOS 7.</span><span class="sxs-lookup"><span data-stu-id="f7555-109">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="f7555-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="f7555-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="f7555-111">Ulepszona dostarczania dziennika w tle.</span><span class="sxs-lookup"><span data-stu-id="f7555-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="f7555-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="f7555-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="f7555-113">Stałe powiadomienie nie których wykonano akcje na urządzeniach z systemem iOS 10.</span><span class="sxs-lookup"><span data-stu-id="f7555-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="f7555-114">Zastąpić XCode 7.</span><span class="sxs-lookup"><span data-stu-id="f7555-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="f7555-115">3.2.4 (06/30/2016)</span><span class="sxs-lookup"><span data-stu-id="f7555-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="f7555-116">Stałe agregacji między dzienniki techniczne i inne dzienniki.</span><span class="sxs-lookup"><span data-stu-id="f7555-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="f7555-117">3.2.3 (06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="f7555-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="f7555-118">Stałe usterki, gdzie dostarczanie opinii nie został zgłoszony podczas aplikacji znajduje się w tle.</span><span class="sxs-lookup"><span data-stu-id="f7555-118">Fixed the bug where delivery feedback is not reported when app is in the background.</span></span>
* <span data-ttu-id="f7555-119">Zoptymalizowanych pod kątem wysyłania dzienników technicznych.</span><span class="sxs-lookup"><span data-stu-id="f7555-119">Optimized the sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="f7555-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="f7555-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="f7555-121">Usunięte usterki w anulowania żądania HTTP, która czasami prowadzi do awarii.</span><span class="sxs-lookup"><span data-stu-id="f7555-121">Fixed bug on HTTP request cancellation which sometimes leads to crash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="f7555-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="f7555-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="f7555-123">Stałe opóźnienie wyzwolenia nowe wystąpienie aplikacji przez powiadomienie z linków bezpośrednich</span><span class="sxs-lookup"><span data-stu-id="f7555-123">Fixed the delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="f7555-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="f7555-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="f7555-125">Włączone kodu bitowego w zestawie SDK, aby pracować z **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="f7555-125">Enabled Bitcode in the SDK to make it work with **Xcode 7**.</span></span>
* <span data-ttu-id="f7555-126">Usunięte usterki związane z powiadomienia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7555-126">Fixed bugs related to in-app notifications.</span></span>
* <span data-ttu-id="f7555-127">Wprowadzone bardziej niezawodna w przypadku niskim poziomie naładowania baterii i inne scenariusze, takie powiadomienia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7555-127">Made the in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="f7555-128">Usunąć dodatkowe konsoli dzienniki generowane przez 3 biblioteki strony.</span><span class="sxs-lookup"><span data-stu-id="f7555-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="f7555-129">3.1.0 (08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="f7555-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="f7555-130">Napraw błąd zgodności z systemem iOS 9 z biblioteką innych firm.</span><span class="sxs-lookup"><span data-stu-id="f7555-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="f7555-131">Została ona powoduje awarii (Crash) podczas wysyłania sonduje wyników, informacje o aplikacji lub dodatkowe dane.</span><span class="sxs-lookup"><span data-stu-id="f7555-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="f7555-132">3.0.0 (06/19/2015)</span><span class="sxs-lookup"><span data-stu-id="f7555-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="f7555-133">Usługa Mobile Engagement używa cichych powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="f7555-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="f7555-134">Obsługę systemu iOS usunąć 4.X.</span><span class="sxs-lookup"><span data-stu-id="f7555-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="f7555-135">Począwszy od tej wersji cel wdrożenia aplikacji musi mieć co najmniej iOS 6.</span><span class="sxs-lookup"><span data-stu-id="f7555-135">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="f7555-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="f7555-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="f7555-137">Identyfikator urządzenia usługi Mobile Engagement dla urządzeń < iOS 6 teraz opiera się na identyfikator GUID generowany podczas instalacji.</span><span class="sxs-lookup"><span data-stu-id="f7555-137">The Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="f7555-138">2.1.0 (04/24/2015)</span><span class="sxs-lookup"><span data-stu-id="f7555-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="f7555-139">Dodano Swift zgodności.</span><span class="sxs-lookup"><span data-stu-id="f7555-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="f7555-140">Po kliknięciu przycisku na powiadomienie, akcji, którą adres URL jest teraz wykonywane prawo po otwarciu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7555-140">When clicking on a notification, the action URL is now executed right after the application is opened.</span></span>
* <span data-ttu-id="f7555-141">Dodano brakujący plik nagłówka w pakiecie SDK.</span><span class="sxs-lookup"><span data-stu-id="f7555-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="f7555-142">Rozwiązano problem, gdy osoby zgłaszającej awarii usługi Mobile Engagement został wyłączony.</span><span class="sxs-lookup"><span data-stu-id="f7555-142">Fixed an issue when the Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="f7555-143">2.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="f7555-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="f7555-144">Początkowa wersja usługi Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f7555-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="f7555-145">Konfiguracja appId/sdkKey zastępuje konfigurację ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="f7555-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="f7555-146">Usunięto interfejs API do wysyłania i odbierania wiadomości XMPP dowolnego z dowolnego XMPP jednostek.</span><span class="sxs-lookup"><span data-stu-id="f7555-146">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="f7555-147">Usunięto interfejs API do wysyłania i odbierania wiadomości między urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="f7555-147">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="f7555-148">Ulepszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="f7555-148">Security improvements.</span></span>
* <span data-ttu-id="f7555-149">Śledzenie SmartAd usunięte.</span><span class="sxs-lookup"><span data-stu-id="f7555-149">SmartAd tracking removed.</span></span>
