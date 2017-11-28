---
title: zachowanie alertu aaaSMS w grupach akcji | Dokumentacja firmy Microsoft
description: "Format wiadomości SMS i odpowiada tooSMS toounsubscribe wiadomości, dokonać ponownej subskrypcji lub prosić o pomoc."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="6d680-103">Zachowanie w grupach akcji alertów programu SMS</span><span class="sxs-lookup"><span data-stu-id="6d680-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="6d680-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6d680-104">Overview</span></span> ##
<span data-ttu-id="6d680-105">Grupy akcji Włącz tooconfigure listy odbiorców.</span><span class="sxs-lookup"><span data-stu-id="6d680-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="6d680-106">Następnie można użyć tych grup, podczas definiowania alerty dziennika aktywności; zapewnienie, że po wyzwoleniu alertu dziennika aktywności hello jest powiadamiany o grupy określonej akcji.</span><span class="sxs-lookup"><span data-stu-id="6d680-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="6d680-107">Jeden z alertów obsługiwane mechanizmy hello jest SMS; alerty Hello obsługuje komunikację dwukierunkową.</span><span class="sxs-lookup"><span data-stu-id="6d680-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="6d680-108">Użytkownik może odpowiadać tooan alertu:</span><span class="sxs-lookup"><span data-stu-id="6d680-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="6d680-109">**Anulowanie subskrypcji alertów:** użytkownik może zrezygnować z wszystkich alertów programu SMS dla wszystkich grup akcji lub grupy pojedynczej akcji.</span><span class="sxs-lookup"><span data-stu-id="6d680-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="6d680-110">**Dokonać ponownej subskrypcji tooalerts:** użytkownika możesz dokonać ponownej subskrypcji tooall alerty programu SMS dla wszystkich grup akcji lub grupy pojedynczej akcji.</span><span class="sxs-lookup"><span data-stu-id="6d680-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="6d680-111">**Prosić o pomoc:** użytkownik może uzyskać więcej informacji na temat hello programu SMS.</span><span class="sxs-lookup"><span data-stu-id="6d680-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="6d680-112">Będą one przekierowanego toothis artykułu</span><span class="sxs-lookup"><span data-stu-id="6d680-112">They will be redirected toothis article</span></span>

<span data-ttu-id="6d680-113">W tym artykule omówiono zachowanie hello hello SMS alertów i hello użytkownika hello akcji odpowiedzi może przyjmować na podstawie ustawień regionalnych hello hello użytkownika:</span><span class="sxs-lookup"><span data-stu-id="6d680-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="6d680-114">Zachowanie USA i Kanady SMS</span><span class="sxs-lookup"><span data-stu-id="6d680-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="6d680-115">Otrzymywanie alertów programu SMS</span><span class="sxs-lookup"><span data-stu-id="6d680-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="6d680-116">Odbiornik programu SMS, który jest skonfigurowany jako część grupy akcji, otrzymają wiadomość SMS, po zgłoszeniu alertu.</span><span class="sxs-lookup"><span data-stu-id="6d680-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="6d680-117">Witaj SMS prowadzi hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="6d680-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="6d680-118">Nazwa_skrócona grupy akcji hello ten alert został wysłany do</span><span class="sxs-lookup"><span data-stu-id="6d680-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="6d680-119">Tytuł hello alertu</span><span class="sxs-lookup"><span data-stu-id="6d680-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="6d680-120">Anulowanie subskrypcji alertów programu SMS dla jednej grupy akcji</span><span class="sxs-lookup"><span data-stu-id="6d680-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="6d680-121">Użytkownika można zrezygnować z programu SMS dla alertów dla grupy jedną akcję przez odpowiada kodu toohello 20873 hello słów kluczowych: "Wyłączanie &lt;nazwa_skrócona grupy akcji&gt;".</span><span class="sxs-lookup"><span data-stu-id="6d680-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="6d680-122">Przykład.</span><span class="sxs-lookup"><span data-stu-id="6d680-122">Ex.</span></span> <span data-ttu-id="6d680-123">Użytkownika toounsubscribe alertów dla grupy akcji z nazwa_skrócona hello "Azure" wyśle kodu toohello SMS 20873 informacją "Wyłącz Azure"</span><span class="sxs-lookup"><span data-stu-id="6d680-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="6d680-124">Anulowanie subskrypcji alertów programu SMS dla wszystkich grup, akcja</span><span class="sxs-lookup"><span data-stu-id="6d680-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="6d680-125">Użytkownik może zrezygnować z wszystkie alerty programu SMS dla wszystkich grup działań przez odpowiada toohello kodu 20873 ze wszystkimi hello następujące słowa kluczowe:</span><span class="sxs-lookup"><span data-stu-id="6d680-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="6d680-126">ZATRZYMAJ</span><span class="sxs-lookup"><span data-stu-id="6d680-126">STOP</span></span>

<span data-ttu-id="6d680-127">Przykład.</span><span class="sxs-lookup"><span data-stu-id="6d680-127">Ex.</span></span> <span data-ttu-id="6d680-128">Użytkownika toounsubscribe wszystkich alertów programu SMS dla wszystkich grup akcji, są wysyłane kodu toohello SMS 20873 informacją stop (Zatrzymaj)"</span><span class="sxs-lookup"><span data-stu-id="6d680-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="6d680-129">Jeśli użytkownik anulował z alertów programu SMS, ale jest następnie dodawana tooa nowej grupy akcji; BĘDĄ one otrzymywać alerty programu SMS dla tej nowej grupy akcji, ale pozostaje anulować ze wszystkich grup poprzedniej akcji.</span><span class="sxs-lookup"><span data-stu-id="6d680-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="6d680-130">Resubscribing tooSMS alerty dla jednej grupy akcji</span><span class="sxs-lookup"><span data-stu-id="6d680-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="6d680-131">Użytkownika można dokonać ponownej subskrypcji tooSMS alertów dla grupy jedną akcję przez odpowiada kodu toohello 20873 hello słów kluczowych: "Włącz &lt;nazwa_skrócona grupy akcji&gt;".</span><span class="sxs-lookup"><span data-stu-id="6d680-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="6d680-132">Przykład.</span><span class="sxs-lookup"><span data-stu-id="6d680-132">Ex.</span></span> <span data-ttu-id="6d680-133">Użytkownika tooalerts tooresubscribe dla grupy akcji z nazwa_skrócona hello "Azure" wyśle kodu toohello SMS 20873 informacją "Włącz Azure"</span><span class="sxs-lookup"><span data-stu-id="6d680-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="6d680-134">Resubscribing tooSMS alertów dla wszystkich grup, akcja</span><span class="sxs-lookup"><span data-stu-id="6d680-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="6d680-135">Użytkownik może dokonać ponownej subskrypcji tooall programu SMS dla alertów dla wszystkich grup akcji ze odpowiada toohello kodu 20873 ze wszystkimi hello następujące słowa kluczowe:</span><span class="sxs-lookup"><span data-stu-id="6d680-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="6d680-136">POCZĄTEK</span><span class="sxs-lookup"><span data-stu-id="6d680-136">START</span></span>

<span data-ttu-id="6d680-137">Przykład.</span><span class="sxs-lookup"><span data-stu-id="6d680-137">Ex.</span></span> <span data-ttu-id="6d680-138">Użytkownika toounsubscribe wszystkich alertów programu SMS dla wszystkich grup akcji, są wysyłane kodu toohello SMS 20873 informacją "START"</span><span class="sxs-lookup"><span data-stu-id="6d680-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="6d680-139">Żądanie pomocy przy użyciu usługi SMS</span><span class="sxs-lookup"><span data-stu-id="6d680-139">Requesting help via SMS</span></span>
<span data-ttu-id="6d680-140">Użytkownika można zadawać uzyskać więcej informacji o hello programu SMS, że otrzymał przez odpowiada kodu toohello 20873 za pomocą dowolnego z następujących słów kluczowych hello:</span><span class="sxs-lookup"><span data-stu-id="6d680-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="6d680-141">POMOC</span><span class="sxs-lookup"><span data-stu-id="6d680-141">HELP</span></span>

<span data-ttu-id="6d680-142">Toohello użytkownika z artykułem toothis łącza zostanie wysłana odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="6d680-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d680-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d680-143">Next Steps</span></span>
<span data-ttu-id="6d680-144">Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md) i Dowiedz się, jak tooget alerty</span><span class="sxs-lookup"><span data-stu-id="6d680-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="6d680-145">Dowiedz się więcej o [limitów szybkości programu SMS](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="6d680-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="6d680-146">Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="6d680-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
