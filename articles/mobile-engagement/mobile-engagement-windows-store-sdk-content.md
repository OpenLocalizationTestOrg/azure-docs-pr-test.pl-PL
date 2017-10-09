---
title: "aaaWindows uniwersalny zestaw SDK aplikacji zawartości"
description: "Więcej informacji na temat zawartości hello hello aplikacji uniwersalnego zestawu SDK dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="94bef-103">Zawartość zestawu SDK aplikacji uniwersalnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="94bef-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="94bef-104">Ten dokument wymieniono i opisano zawartości hello wdrożone przez hello zestawu SDK w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94bef-104">This document lists and describes hello content deployed by hello SDK in your application.</span></span>

## <a name="hello-resources-folder"></a><span data-ttu-id="94bef-105">Witaj `/Resources` folderu</span><span class="sxs-lookup"><span data-stu-id="94bef-105">hello `/Resources` folder</span></span>
<span data-ttu-id="94bef-106">Ten folder zawiera wszystkie zasoby hello, które wymaga usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="94bef-106">This folder contains all hello resources that Mobile Engagement needs.</span></span> <span data-ttu-id="94bef-107">Można również dostosować je toofit aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94bef-107">You can also customize them toofit your app.</span></span>

* <span data-ttu-id="94bef-108">`EngagementConfiguration.xml`: hello pliku konfiguracji usługi Mobile Engagement, jest to, gdzie można dostosować ustawienia usługi Mobile Engagement (parametry połączenia usługi Mobile Engagement, awarii raportu...).</span><span class="sxs-lookup"><span data-stu-id="94bef-108">`EngagementConfiguration.xml` : hello Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="94bef-109">folder polecenia</span><span class="sxs-lookup"><span data-stu-id="94bef-109">/html folder</span></span>
* <span data-ttu-id="94bef-110">`EngagementNotification.html`: hello `Notification` widok html projektu dla transparentach w aplikacji w sieci web.</span><span class="sxs-lookup"><span data-stu-id="94bef-110">`EngagementNotification.html` : hello `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="94bef-111">`EngagementAnnouncement.html`: hello `Announcement` widoku projektowanie html w aplikacji międzysegmentowe widoków witryn sieci web.</span><span class="sxs-lookup"><span data-stu-id="94bef-111">`EngagementAnnouncement.html` : hello `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="94bef-112">/images folder</span><span class="sxs-lookup"><span data-stu-id="94bef-112">/images folder</span></span>
* <span data-ttu-id="94bef-113">`EngagementIconNotification.png`: hello brand ikony wyświetlane pod kątem hello lewej powiadomienia, Zastąp to jedno z ikoną marki.</span><span class="sxs-lookup"><span data-stu-id="94bef-113">`EngagementIconNotification.png` : hello brand icon displayed at hello left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="94bef-114">`EngagementIconOk.png`: hello `Ok` ikona hello reach zawartości stron hello jest przycisk akcji lub sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="94bef-114">`EngagementIconOk.png` : hello `Ok` icon of hello reach content pages for hello action or validation button.</span></span>
* <span data-ttu-id="94bef-115">`EngagementIconNOK.png`: hello `NOK` ikona hello przycisk weryfikacji zawartości stron reach hello jest wyłączony.</span><span class="sxs-lookup"><span data-stu-id="94bef-115">`EngagementIconNOK.png` : hello `NOK` icon used when hello validation button of hello reach content pages is disabled.</span></span>
* <span data-ttu-id="94bef-116">`EngagementIconClose.png`: hello `Close` ikona hello osiągnąć powiadomienia i zawartości hello odrzucić przycisku.</span><span class="sxs-lookup"><span data-stu-id="94bef-116">`EngagementIconClose.png` : hello `Close` icon of hello reach notifications and contents for hello dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="94bef-117">/overlay folder</span><span class="sxs-lookup"><span data-stu-id="94bef-117">/overlay folder</span></span>
* <span data-ttu-id="94bef-118">`EngagementPageOverlay.cs`: hello nakładki strony jest odpowiedzialny za dodawanie hello reach usługi Engagement podrzędnych tooits interfejsu użytkownika w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94bef-118">`EngagementPageOverlay.cs` : hello overlay page responsible for adding hello Engagement reach in-app UI tooits child.</span></span>

