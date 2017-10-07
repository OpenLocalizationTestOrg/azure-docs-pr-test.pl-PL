---
title: "aaaLearn o weryfikacji dwuetapowej w usługi Azure MFA | Dokumentacja firmy Microsoft"
description: "Co to jest usługa Azure Multi-Factor Authentication, dlaczego warto używać usługi MFA, więcej informacji na temat powitania klienta uwierzytelniania wieloskładnikowego i hello różnych metod i wersje dostępne. "
keywords: "tooMFA wprowadzenie omówienie uwierzytelniania mfa, co to jest usługa mfa"
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
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="031b4-104">Co to jest usługa Multi-Factor Authentication platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="031b4-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="031b4-105">Weryfikacja dwuetapowa to metoda uwierzytelniania, która wymaga więcej niż jednej metody weryfikacji i dodaje kluczową drugą warstwę logowania toouser zabezpieczeń i transakcji.</span><span class="sxs-lookup"><span data-stu-id="031b4-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="031b4-106">Działania, gdyż dowolne dwa lub więcej hello następujące metody weryfikacji:</span><span class="sxs-lookup"><span data-stu-id="031b4-106">It works by requiring any two or more of hello following verification methods:</span></span>

* <span data-ttu-id="031b4-107">Coś znasz (zwykle hasła)</span><span class="sxs-lookup"><span data-stu-id="031b4-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="031b4-108">Coś (zaufanych urządzeń, który nie jest łatwo zduplikowany, takich jak telefon)</span><span class="sxs-lookup"><span data-stu-id="031b4-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="031b4-109">Coś jest (biometria)</span><span class="sxs-lookup"><span data-stu-id="031b4-109">Something you are (biometrics)</span></span>

<span data-ttu-id="031b4-110"><center>![Nazwa użytkownika i hasło](./media/multi-factor-authentication/pword.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![certyfikaty](./media/multi-factor-authentication/phone.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Inteligentne Phone](./media/multi-factor-authentication/hware.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![kart inteligentnych](./media/multi-factor-authentication/smart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![Wirtualnej karty inteligentnej](./media/multi-factor-authentication/vsmart.png) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![nazwy użytkownika i Hasło](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="031b4-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="031b4-111">Azure Multi-Factor Authentication (MFA) to rozwiązanie firmy Microsoft służące do przeprowadzania weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="031b4-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="031b4-112">Usługa Azure MFA ułatwia zabezpieczenie dostępu toodata i aplikacje spełniając zapotrzebowanie na prosty proces logowania.</span><span class="sxs-lookup"><span data-stu-id="031b4-112">Azure MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="031b4-113">Oferuje ona silne uwierzytelnianie za pośrednictwem różnych metod weryfikacji, w tym weryfikacji w trakcie rozmowy telefonicznej albo przy użyciu wiadomości SMS lub aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="031b4-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="031b4-114">Dlaczego warto używać usługi Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="031b4-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="031b4-115">Już dziś, więcej niż kiedykolwiek osoby coraz są połączone.</span><span class="sxs-lookup"><span data-stu-id="031b4-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="031b4-116">W przypadku inteligentne telefony, tablety, komputery przenośne i komputery osoby mają różne sposoby na sposób będą tooconnect i łączność w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="031b4-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going tooconnect and stay connected at any time.</span></span> <span data-ttu-id="031b4-117">Osoby mogą uzyskać dostęp do swoich kont i aplikacji z dowolnego miejsca, co oznacza, że można więcej pracy i obsługi klientów lepiej.</span><span class="sxs-lookup"><span data-stu-id="031b4-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="031b4-118">Uwierzytelnianie wieloskładnikowe platformy Azure jest łatwe toouse, skalowalnych i niezawodne rozwiązanie zapewnia druga metoda uwierzytelniania, dlatego użytkownicy są chronione przez cały czas.</span><span class="sxs-lookup"><span data-stu-id="031b4-118">Azure Multi-Factor Authentication is an easy toouse, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Łatwe tooUse](./media/multi-factor-authentication/simple.png) | ![Skalowalność](./media/multi-factor-authentication/scalable.png) | ![Chronione przez cały czas](./media/multi-factor-authentication/protected.png) | ![Niezawodne](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="031b4-123">**Łatwe toouse**</span><span class="sxs-lookup"><span data-stu-id="031b4-123">**Easy toouse**</span></span> |<span data-ttu-id="031b4-124">**Skalowalne**</span><span class="sxs-lookup"><span data-stu-id="031b4-124">**Scalable**</span></span> |<span data-ttu-id="031b4-125">**Chronione przez cały czas**</span><span class="sxs-lookup"><span data-stu-id="031b4-125">**Always Protected**</span></span> |<span data-ttu-id="031b4-126">**Niezawodne**</span><span class="sxs-lookup"><span data-stu-id="031b4-126">**Reliable**</span></span> |

* <span data-ttu-id="031b4-127">**Łatwe tooUse** -Azure Multi-Factor Authentication jest proste tooset się i używania.</span><span class="sxs-lookup"><span data-stu-id="031b4-127">**Easy tooUse** - Azure Multi-Factor Authentication is simple tooset up and use.</span></span> <span data-ttu-id="031b4-128">Witaj dodatkowej ochrony dołączanego do usługi Azure Multi-Factor Authentication umożliwia toomanage użytkowników ich własnych urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="031b4-128">hello extra protection that comes with Azure Multi-Factor Authentication allows users toomanage their own devices.</span></span> <span data-ttu-id="031b4-129">Najlepsze, w wielu przypadkach go można skonfigurować kilka prostych kliknięć.</span><span class="sxs-lookup"><span data-stu-id="031b4-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="031b4-130">**Skalowalne** — uwierzytelnianie wieloskładnikowe Azure korzysta z możliwości hello hello w chmurze i integruje się z lokalnymi AD i aplikacji niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="031b4-130">**Scalable** - Azure Multi-Factor Authentication uses hello power of hello cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="031b4-131">Ta ochrona jest nawet rozszerzony tooyour dużych, kluczowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="031b4-131">This protection is even extended tooyour high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="031b4-132">**Chronione przez cały czas** -Azure Multi-Factor Authentication udostępnia silnego uwierzytelniania za pomocą hello najwyższymi standardami branżowymi.</span><span class="sxs-lookup"><span data-stu-id="031b4-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using hello highest industry standards.</span></span>
* <span data-ttu-id="031b4-133">**Niezawodne** -gwarantujemy dostępność 99,9% Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="031b4-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="031b4-134">Hello usługa jest uznawana za niedostępną gdy nie jest w stanie tooreceive lub proces weryfikacji żądania hello weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="031b4-134">hello service is considered unavailable when it is unable tooreceive or process verification requests for hello two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="031b4-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="031b4-135">Next steps</span></span>

- <span data-ttu-id="031b4-136">Dowiedz się więcej o [jak działa usługa Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="031b4-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="031b4-137">Przeczytaj informacje o różnych hello [wersji i metody zużycia uwierzytelnianie wieloskładnikowe Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="031b4-137">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
