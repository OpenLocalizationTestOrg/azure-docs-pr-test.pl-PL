---
title: "Nieregularne działania związane z logowaniem"
description: "Raport, który zawiera logowania, które zostały zidentyfikowane jako nietypowych przez naszych algorytmów uczenia maszynowego."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 565321b6f3ad5988f383a701cb9d8bd5c9937795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="irregular-sign-in-activity"></a><span data-ttu-id="dd66d-103">Nieregularne działania związane z logowaniem</span><span class="sxs-lookup"><span data-stu-id="dd66d-103">Irregular sign-in activity</span></span>
<span data-ttu-id="dd66d-104">Nieregularne logowania są tymi, które zostały zidentyfikowane przez naszych algorytmów, na podstawie warunku "niemożliwa podróż" połączone z nietypowe logowania w lokalizacji, a urządzenie uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="dd66d-104">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign in location and device.</span></span> <span data-ttu-id="dd66d-105">Może to oznaczać, że haker pomyślnie zalogował się przy użyciu tego konta.</span><span class="sxs-lookup"><span data-stu-id="dd66d-105">This may indicate that a hacker has successfully signed in using this account.</span></span>
<span data-ttu-id="dd66d-106">Wyślemy wiadomość e-mail z powiadomieniem do administratorów globalnych możemy napotkania 10 lub więcej nietypowe logowania zdarzenia w ciągu 30 dni lub mniej należy do zakresu.</span><span class="sxs-lookup"><span data-stu-id="dd66d-106">We will send an email notification to the global admins if we encounter 10 or more anomalous sign-in events within a span of 30 days or less.</span></span> <span data-ttu-id="dd66d-107">Pamiętaj uwzględnić aad-alerts-noreply@mail.windowsazure.com na liście bezpiecznych.</span><span class="sxs-lookup"><span data-stu-id="dd66d-107">Please be sure to include aad-alerts-noreply@mail.windowsazure.com in your safe senders list.</span></span>

