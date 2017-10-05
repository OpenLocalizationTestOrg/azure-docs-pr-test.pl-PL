---
title: "Dowiedz się więcej o weryfikacji dwuetapowej w usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Co to jest usługa Azure Multi-Factor Authentication, dlaczego warto używać usługi MFA, więcej informacji na temat klienta usługi Multi-Factor Authentication i różnych metod i wersje dostępne. "
keywords: "wprowadzenie do usługi MFA, omówienie uwierzytelniania mfa, co to jest usługa mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: 7334ab5b278c3339fdbc2e363fd5c609604d3e14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="7debb-104">Co to jest usługa Multi-Factor Authentication platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="7debb-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="7debb-105">Weryfikacja dwuetapowa to metoda uwierzytelniania, która wymaga więcej niż jednej metody weryfikacji i dodaje kluczową drugą warstwę zabezpieczeń do logowania użytkowników i transakcji.</span><span class="sxs-lookup"><span data-stu-id="7debb-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="7debb-106">Działania, gdyż dowolne dwa lub więcej z następujących metod weryfikacji:</span><span class="sxs-lookup"><span data-stu-id="7debb-106">It works by requiring any two or more of the following verification methods:</span></span>

* <span data-ttu-id="7debb-107">Coś znasz (zwykle hasła)</span><span class="sxs-lookup"><span data-stu-id="7debb-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="7debb-108">Coś (zaufanych urządzeń, który nie jest łatwo zduplikowany, takich jak telefon)</span><span class="sxs-lookup"><span data-stu-id="7debb-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="7debb-109">Coś jest (biometria)</span><span class="sxs-lookup"><span data-stu-id="7debb-109">Something you are (biometrics)</span></span>

<span data-ttu-id="7debb-110"><center>![Nazwa użytkownika i hasło](./media/multi-factor-authentication/pword.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![certyfikaty](./media/multi-factor-authentication/phone.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Inteligentne Phone](./media/multi-factor-authentication/hware.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![kart inteligentnych](./media/multi-factor-authentication/smart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Wirtualnej karty inteligentnej](./media/multi-factor-authentication/vsmart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![nazwy użytkownika i Hasło](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="7debb-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="7debb-111">Azure Multi-Factor Authentication (MFA) to rozwiązanie firmy Microsoft służące do przeprowadzania weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="7debb-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="7debb-112">Usługa Azure MFA zabezpiecza dostęp do danych i aplikacji, a jednocześnie spełnia wymagania użytkowników dotyczące prostoty procesu logowania.</span><span class="sxs-lookup"><span data-stu-id="7debb-112">Azure MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="7debb-113">Oferuje ona silne uwierzytelnianie za pośrednictwem różnych metod weryfikacji, w tym weryfikacji w trakcie rozmowy telefonicznej albo przy użyciu wiadomości SMS lub aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="7debb-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="7debb-114">Dlaczego warto używać usługi Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="7debb-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="7debb-115">Już dziś, więcej niż kiedykolwiek osoby coraz są połączone.</span><span class="sxs-lookup"><span data-stu-id="7debb-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="7debb-116">W przypadku inteligentne telefony, tablety, komputery przenośne i komputery osoby mają różne sposoby na jak wkrótce połączenia i łączność w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="7debb-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going to connect and stay connected at any time.</span></span> <span data-ttu-id="7debb-117">Osoby mogą uzyskać dostęp do swoich kont i aplikacji z dowolnego miejsca, co oznacza, że można więcej pracy i obsługi klientów lepiej.</span><span class="sxs-lookup"><span data-stu-id="7debb-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="7debb-118">Uwierzytelnianie wieloskładnikowe platformy Azure jest łatwy w użyciu, skalowalne i niezawodne rozwiązanie, które oferuje druga metoda uwierzytelniania, użytkownicy są chronione przez cały czas.</span><span class="sxs-lookup"><span data-stu-id="7debb-118">Azure Multi-Factor Authentication is an easy to use, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Łatwość użycia](./media/multi-factor-authentication/simple.png) | ![Skalowalność](./media/multi-factor-authentication/scalable.png) | ![Chronione przez cały czas](./media/multi-factor-authentication/protected.png) | ![Niezawodne](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="7debb-123">**Łatwy w użyciu**</span><span class="sxs-lookup"><span data-stu-id="7debb-123">**Easy to use**</span></span> |<span data-ttu-id="7debb-124">**Skalowalne**</span><span class="sxs-lookup"><span data-stu-id="7debb-124">**Scalable**</span></span> |<span data-ttu-id="7debb-125">**Chronione przez cały czas**</span><span class="sxs-lookup"><span data-stu-id="7debb-125">**Always Protected**</span></span> |<span data-ttu-id="7debb-126">**Niezawodne**</span><span class="sxs-lookup"><span data-stu-id="7debb-126">**Reliable**</span></span> |

* <span data-ttu-id="7debb-127">**Łatwy w użyciu** -Azure Multi-Factor Authentication jest prosta do konfigurowania i używania.</span><span class="sxs-lookup"><span data-stu-id="7debb-127">**Easy to Use** - Azure Multi-Factor Authentication is simple to set up and use.</span></span> <span data-ttu-id="7debb-128">Dodatkowa ochrona, dołączanego do usługi Azure Multi-Factor Authentication umożliwia użytkownikom zarządzanie swoimi własnymi urządzeniami.</span><span class="sxs-lookup"><span data-stu-id="7debb-128">The extra protection that comes with Azure Multi-Factor Authentication allows users to manage their own devices.</span></span> <span data-ttu-id="7debb-129">Najlepsze, w wielu przypadkach go można skonfigurować kilka prostych kliknięć.</span><span class="sxs-lookup"><span data-stu-id="7debb-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="7debb-130">**Skalowalne** — uwierzytelnianie wieloskładnikowe Azure korzysta z możliwości chmury i integruje się z lokalnymi AD i aplikacji niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="7debb-130">**Scalable** - Azure Multi-Factor Authentication uses the power of the cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="7debb-131">Ta ochrona jest nawet rozszerzony do dużego, kluczowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="7debb-131">This protection is even extended to your high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="7debb-132">**Chronione przez cały czas** -Azure Multi-Factor Authentication udostępnia silnego uwierzytelniania za pomocą najwyższymi standardami branżowymi.</span><span class="sxs-lookup"><span data-stu-id="7debb-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using the highest industry standards.</span></span>
* <span data-ttu-id="7debb-133">**Niezawodne** -gwarantujemy dostępność 99,9% Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="7debb-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="7debb-134">Usługa jest uznawana za niedostępną, gdy nie może otrzymywać lub przetwarzania żądania weryfikacji na potrzeby weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="7debb-134">The service is considered unavailable when it is unable to receive or process verification requests for the two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="7debb-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7debb-135">Next steps</span></span>

- <span data-ttu-id="7debb-136">Dowiedz się więcej o [jak działa usługa Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="7debb-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="7debb-137">Przeczytaj informacje o różnych [wersji i metody zużycia uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="7debb-137">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
