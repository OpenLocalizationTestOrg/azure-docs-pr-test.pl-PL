---
title: "aaaSet rozliczeń lub środki alerty dotyczące subskrypcji platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak można skonfigurować alerty na rachunku Azure, aby uniknąć niespodzianki rozliczeń."
keywords: "środki alert, alert rozliczeń"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a>Ustawianie alertów rozliczeń lub faktury dla subskrypcji platformy Microsoft Azure
Jeśli jesteś hello administratora konta subskrypcji platformy Azure, można użyć hello Azure rozliczeń Usługa alertów rozliczeń toocreate dostosować alerty ułatwiające monitorowanie i zarządzanie działania rozliczeń dla konta platformy Azure.

Ta usługa jest w wersji zapoznawczej, więc należy tooenable go na stronie funkcji w wersji zapoznawczej hello najpierw.

## <a name="set-hello-alert-threshold-and-email-recipients"></a>Ustaw hello próg i adres e-mail odbiorcy alertów
1. Odwiedź stronę [strona funkcje w wersji zapoznawczej hello](https://account.windowsazure.com/PreviewFeatures) i Włącz **rozliczeń Usługa alertów**.

1. Po otrzymaniu hello e-mail potwierdzenie, że usługa rozliczeń hello jest włączona dla Twojej subskrypcji, odwiedź stronę [strony subskrypcje hello](https://account.windowsazure.com/Subscriptions) w portalu konta hello. Kliknij subskrypcję hello toomonitor, a następnie kliknij przycisk **alerty**.

    ![Zrzut ekranu przedstawiający widok subskrypcji hello Centrum konta platformy Azure z wyróżnioną pozycją alertami][Image1]

2. Następnie kliknij przycisk **dodać alertu** toocreate Twojego pierwszego z nich. Można ustawić łącznie pięć alerty dotyczące rozliczeń dla subskrypcji o różnych progu i zapasowej tootwo adresatów wiadomości e-mail o każdym alercie.

    ![Zrzut ekranu przedstawiający hello widok alertów, w którym można dodać alertu][Image2]

3. Po dodaniu alert nadaj unikatową nazwę, wybierz próg wydatków i wybierz hello adresów e-mail, gdy alerty są wysyłane. Podczas konfigurowania hello próg, można wybrać jedną **rozliczeń całkowita** lub **środki pieniężne** z hello **alertów dla** listy. Łącznie rozliczeń alert jest wysyłany, gdy subskrypcja wydatków przekracza próg hello. Uzyskać środki pieniężne alert jest wysyłany, gdy kwota środków pieniężnych spadnie poniżej hello limit. Kwota środków pieniężnych stosowane są zazwyczaj tooFree subskrypcji wersji próbnej i Visual Studio.

    ![Zrzut ekranu przedstawiający widok alertu dodanie hello, którym można skonfigurować adresatów][Image3]

Azure obsługuje dowolnego adresu e-mail, ale nie Sprawdź, czy adres e-mail hello działa, więc dokładnie literówki.

## <a name="check-on-your-alerts"></a>Sprawdź alerty
Po skonfigurowaniu alerty hello Centrum konta je i pokazuje, ile więcej można skonfigurować. Dla każdego alertu Zobacz hello daty i godziny, wysłania, czy jest alert dotyczący rozliczeń całkowita lub środki pieniężne oraz limit hello, skonfigurowane. format daty i godziny Hello 24-godzinnym koordynować czasu uniwersalnego (UTC) i Data hello jest format rrrr mm-dd. Kliknij hello oraz zarejestrować alertu w tooedit listy hello lub hello toodelete Kosza może go.

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a>Karta alerty dla klientów Enterprise Agreement (EA)
Umowa EA klienci mogą uzyskać alerty dla każdego działu w ramach rejestracji przez ustawienie wydatków przydziałów. Zobacz [przydziały wydatków działu](https://ea.azure.com/helpdocs/departmentSpendingQuotas) w tooget portalu EA hello uruchomiona.

## <a name="learn-more-about-azure-cost-management"></a>Dowiedz się więcej na temat zarządzania Azure koszt
- Szacowanie kosztów przy użyciu hello [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/), [całkowity koszt posiadania kalkulatora](https://aka.ms/azure-tco-calculator), a po dodaniu usługi.
- [Przejrzyj użycia i kosztów regularnie w portalu Azure](billing-getting-started.md#costs).
- Włącz [Azure Advisor koszt zalecenia](../advisor/advisor-cost-recommendations.md).

toolearn więcej, zobacz [Azure koszt wskazówki dotyczące zarządzania](billing-getting-started.md).

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
