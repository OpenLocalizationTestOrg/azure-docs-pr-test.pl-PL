---
title: Logowania z wielu lokalizacji geograficznych
description: "Raport, który wskazuje użytkowników, którego dwa logowania wydawały się następować z różnych regionów, a czas między logowaniami dodatki uniemożliwia użytkownikowi ma przemieścić między tymi lokalizacjami."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a><span data-ttu-id="48cad-103">Logowania z wielu lokalizacji geograficznych</span><span class="sxs-lookup"><span data-stu-id="48cad-103">Sign-ins from multiple geographies</span></span>
<span data-ttu-id="48cad-104">Ten raport zawiera pomyślnego logowania z użytkownikiem, gdzie dwa logowania wydawały się następować z różnych regionów, a czas między sesje logowania uniemożliwia użytkownik zdążył przemieścić się między tymi lokalizacjami.</span><span class="sxs-lookup"><span data-stu-id="48cad-104">This report includes successful sign-ins from a user where two sign-ins appeared to originate from different regions and the time between the sign-ins makes it impossible for the user to have traveled between those regions.</span></span> <span data-ttu-id="48cad-105">Możliwe przyczyny:</span><span class="sxs-lookup"><span data-stu-id="48cad-105">Possible causes include:</span></span>

* <span data-ttu-id="48cad-106">Użytkownik udostępnia komuś swoje hasło z innymi użytkownikami</span><span class="sxs-lookup"><span data-stu-id="48cad-106">User is sharing their password with other users</span></span>
* <span data-ttu-id="48cad-107">Użytkownik korzysta z pulpitu zdalnego w celu uruchomienia przeglądarki sieci web dla logowania</span><span class="sxs-lookup"><span data-stu-id="48cad-107">User is using a remote desktop to launch a web browser for sign-in</span></span>
* <span data-ttu-id="48cad-108">Haker zalogował się na konto użytkownika z innego kraju</span><span class="sxs-lookup"><span data-stu-id="48cad-108">A hacker has signed in to the account of a user from a different country</span></span>
* <span data-ttu-id="48cad-109">Użytkownik korzysta z sieci VPN lub serwer proxy</span><span class="sxs-lookup"><span data-stu-id="48cad-109">User is using a VPN or proxy</span></span>
* <span data-ttu-id="48cad-110">Użytkownik jest zalogowany przy użyciu wielu urządzeń w tym samym czasie, takie jak pulpit i na telefon komórkowy i adres IP telefonu komórkowego jest rzadko używana.</span><span class="sxs-lookup"><span data-stu-id="48cad-110">User is signed in from multiple devices at the same time, such as a desktop and a mobile phone, and the IP address of the mobile phone is unusual.</span></span>

<span data-ttu-id="48cad-111">Wyniki z tego raportu zostanie wyświetlona pomyślnego logowania zdarzenia, oraz czas między sesje logowania, regionów, w którym sesje logowania wydawały się następować z i podróży szacowany czas między tymi lokalizacjami.</span><span class="sxs-lookup"><span data-stu-id="48cad-111">Results from this report will show you the successful sign-in events, together with the time between the sign-ins, the regions where the sign-ins appeared to originate from, and the estimated travel time between those regions.</span></span> <span data-ttu-id="48cad-112">Podczas podróży, wyświetlane jest tylko szacowana i może różnić się od czasu rzeczywistego podróży między lokacjami.</span><span class="sxs-lookup"><span data-stu-id="48cad-112">The travel time shown is only an estimate and may be different from the actual travel time between the locations.</span></span>

![Logowania z wielu lokalizacji geograficznych](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)

