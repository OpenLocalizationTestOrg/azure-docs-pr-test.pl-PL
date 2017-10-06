---
title: aaaSign ins po wielokrotnych niepowodzeniach
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
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="14d17-103">Logowania po wielokrotnych niepowodzeniach</span><span class="sxs-lookup"><span data-stu-id="14d17-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="14d17-104">Ten raport wskazuje użytkowników, którzy mają pomyślnie zalogował się po wiele kolejnych logowania nie powiodła się podczas prób.</span><span class="sxs-lookup"><span data-stu-id="14d17-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="14d17-105">Możliwe przyczyny:</span><span class="sxs-lookup"><span data-stu-id="14d17-105">Possible causes include:</span></span>

* <span data-ttu-id="14d17-106">Użytkownik miał zapomniane hasła</span><span class="sxs-lookup"><span data-stu-id="14d17-106">User had forgotten their password</span></span></li><li><span data-ttu-id="14d17-107">Użytkownik jest ofiarą hello odgadnięcie ataków siłowych hasła powiodło się</span><span class="sxs-lookup"><span data-stu-id="14d17-107">User is hello victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="14d17-108">Ten raport zostanie w wynikach hello wiele kolejnych nieudanych prób logowania wprowadzone toohello wcześniejszego pomyślnego logowania i sygnatura czasowa skojarzona hello pierwszego pomyślnego logowania.</span><span class="sxs-lookup"><span data-stu-id="14d17-108">Results from this report will show you hello number of consecutive failed sign-in attempts made prior toohello successful sign-in and a timestamp associated with hello first successful sign-in.</span></span>

<span data-ttu-id="14d17-109">**Raport ustawienia**: hello minimalną liczbę kolejnych nieudanych logowania można skonfigurować w prób, które musi wystąpić, zanim mogą być wyświetlane w raporcie hello.</span><span class="sxs-lookup"><span data-stu-id="14d17-109">**Report Settings**: You can configure hello minimum number of consecutive failed sign in attempts that must occur before it can be displayed in hello report.</span></span> <span data-ttu-id="14d17-110">Po wprowadzeniu zmian jest toothis ustawieniem dla niego toonote ważne, czy te zmiany nie zostaną zastosowane tooany istniejących nie powiodło się logowania, które aktualnie wyświetlane w raporcie istniejących.</span><span class="sxs-lookup"><span data-stu-id="14d17-110">When you make changes toothis setting it is important toonote that these changes will not be applied tooany existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="14d17-111">Jednak zostaną one zastosowane tooall przyszłych logowania. Raport o zmianach toothis może zawierać tylko przez administratorów licencjonowane.</span><span class="sxs-lookup"><span data-stu-id="14d17-111">However, they will be applied tooall future sign-ins. Changes toothis report can only be made by licensed admins.</span></span>

![Logowania po wielokrotnych niepowodzeniach](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

