---
title: Logowania po wielokrotnych niepowodzeniach
description: "Raport, który wskazuje użytkowników, którzy mają pomyślnie zalogował się po wiele kolejnych logowania nie powiodła się podczas prób."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="5c5da-103">Logowania po wielokrotnych niepowodzeniach</span><span class="sxs-lookup"><span data-stu-id="5c5da-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="5c5da-104">Ten raport wskazuje użytkowników, którzy mają pomyślnie zalogował się po wiele kolejnych logowania nie powiodła się podczas prób.</span><span class="sxs-lookup"><span data-stu-id="5c5da-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="5c5da-105">Możliwe przyczyny:</span><span class="sxs-lookup"><span data-stu-id="5c5da-105">Possible causes include:</span></span>

* <span data-ttu-id="5c5da-106">Użytkownik miał zapomniane hasła</span><span class="sxs-lookup"><span data-stu-id="5c5da-106">User had forgotten their password</span></span></li><li><span data-ttu-id="5c5da-107">Użytkownik jest ofiarą odgadnięcie ukierunkowany hasła pomyślne wymusić ataków</span><span class="sxs-lookup"><span data-stu-id="5c5da-107">User is the victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="5c5da-108">Wyniki z tego raportu Pokaż liczbę kolejnych nieudanych prób logowania utworzone przed pomyślnym logowaniem i sygnaturę czasową skojarzone z pierwszego pomyślnego logowania.</span><span class="sxs-lookup"><span data-stu-id="5c5da-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span></span>

<span data-ttu-id="5c5da-109">**Raport ustawienia**: można skonfigurować minimalną liczbę kolejnych logowania nie powiodło się podczas prób, które musi wystąpić, zanim mogą być wyświetlane w raporcie.</span><span class="sxs-lookup"><span data-stu-id="5c5da-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span></span> <span data-ttu-id="5c5da-110">Możesz zmienić to ustawienie jest należy pamiętać, że te zmiany nie zostaną zastosowane do istniejącego logowania zakończonych niepowodzeniem ins który aktualnie wyświetlane w istniejącego raportu.</span><span class="sxs-lookup"><span data-stu-id="5c5da-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="5c5da-111">Jednak zostaną one zastosowane do wszystkich przyszłych logowania.</span><span class="sxs-lookup"><span data-stu-id="5c5da-111">However, they will be applied to all future sign-ins.</span></span> <span data-ttu-id="5c5da-112">Zmiany w tym raporcie może zawierać tylko przez administratorów licencjonowane.</span><span class="sxs-lookup"><span data-stu-id="5c5da-112">Changes to this report can only be made by licensed admins.</span></span>

![Logowania po wielokrotnych niepowodzeniach](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

