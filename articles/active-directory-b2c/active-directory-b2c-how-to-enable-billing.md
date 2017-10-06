---
title: "tooLink aaaHow tooAzure subskrypcji usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "Przewodnik krok po kroku tooenable rozliczeń dla dzierżawy usługi Azure AD B2C do subskrypcji platformy Azure."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>Łączenie subskrypcji Azure tooan Azure B2C dzierżawy toopay opłat użycia

Opłaty dotyczących ciągłego użytkowania dla usługi Azure Active Directory B2C (lub usługi Azure AD B2C) są rachunku tooan subskrypcji platformy Azure. Konieczne jest dla hello dzierżawy administratora tooexplicitly łącze hello Azure AD B2C dzierżawy tooan subskrypcji platformy Azure po utworzeniu dzierżawy hello B2C, sama.  To łącze jest to osiągane przez utworzenie usługi Azure AD "Dzierżawy B2C" zasobów w celu hello subskrypcji platformy Azure. Wiele dzierżaw B2C może być połączone tooa jedna subskrypcja platformy Azure oraz innych zasobów platformy Azure (na przykład maszyny wirtualne, Magazyn danych, LogicApps)


> [!IMPORTANT]
> najnowsze informacje dotyczące użycia rozliczeniach i cenach usługi B2C jest na powitania po stronie Hello: [cennik usługi Azure AD B2C](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>Krok 1 — Tworzenie dzierżawy usługi Azure AD B2C
Tworzenie dzierżawy usługi B2C musi najpierw zostać zakończona. Jeśli utworzono już urządzenie docelowe dzierżawy B2C, Pomiń ten krok. [Wprowadzenie do usługi Azure AD B2C](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>Krok 2 — Otwieranie portalu Azure w hello dzierżawy usługi Azure AD, pokazujący subskrypcji platformy Azure
Przejdź toohello [portalu Azure](https://portal.azure.com). Przełącz toohello dzierżawy usługi Azure AD, pokazujący hello subskrypcji platformy Azure, które chcesz toouse. Tej dzierżawy usługi Azure AD jest inna niż hello dzierżawy B2C. W ramach hello portalu Azure kliknij nazwę konta hello na powitania prawym górnym rogu hello pulpitu nawigacyjnego tooselect hello dzierżawy Azure AD. Tooproceed wymagana jest subskrypcja platformy Azure. [Uzyskiwanie subskrypcji platformy Azure](https://account.windowsazure.com/signup?showCatalog=True)

![Przełączanie tooyour dzierżawy Azure AD](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>Krok 3 — Tworzenie zasobu dzierżawy B2C w portalu Azure Marketplace
Otwórz Marketplace, klikając ikonę Marketplace hello, lub wybranie hello zielony "+" hello lewego górnego rogu hello pulpitu nawigacyjnego.  Wyszukaj i wybierz Azure Active Directory B2C. Wybierz opcję Utwórz.

![Wybierz witryny Marketplace](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![Funkcje B2C wyszukiwania](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

Witaj zasobów usługi Azure AD B2C Tworzenie okna dialogowego hello obejmuje następujące parametry:

1. Dzierżawy usługi Azure AD B2C — wybierz dzierżawy usługi Azure AD B2C, z listy rozwijanej hello.  Pokaż tylko kwalifikujących się dzierżaw usługi Azure AD B2C.  Kwalifikujące się dzierżawcy usługi B2C spełnia te warunki: są hello administrator globalny dzierżawy hello B2C i hello B2C dzierżawy nie jest aktualnie powiązany tooan subskrypcji platformy Azure

2. Azure AD B2C zasobu Nazwa — to nazwa domeny hello wstępnie wybrane toomatch hello dzierżawy B2C

3. Subskrypcja — aktywną subskrypcją platformy Azure, w którym są uprawnienia administratora lub administratora wspólnej.  Wiele dzierżaw usługi Azure AD B2C można dodać tooone subskrypcji platformy Azure

4. Lokalizacja grupy zasobów i grupy zasobów — to artefaktu pomaga organizować wielu zasobów platformy Azure.  Ten wybór nie ma wpływu na lokalizację dzierżawy B2C, wydajność lub rozliczeń stanu

5. Przypnij toodashboard najprostszym dzierżawcy tooyour B2C dostępu rozliczeń informacji i hello ustawieniami dzierżawy B2C ![utworzyć zasobu usługi B2C](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>Krok 4 — zarządzanie zasobami dzierżawy B2C (opcjonalnie)
Po zakończeniu wdrażania nowego zasobu "Dzierżawy B2C" jest tworzona w docelowej grupie zasobów hello i związane z subskrypcją platformy Azure.  Nowy zasób typu, który dodaje "Dzierżawy B2C" powinna zostać wyświetlona równolegle z innymi zasobami platformy Azure.

![Utwórz zasób B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

Klikając zasobów dzierżawy hello B2C jest możliwe
- Kliknij przycisk informacji dotyczących rozliczeń tooreview nazwę subskrypcji. Zobacz dotyczącymi rozliczeń i użycia.
- Kliknij ustawienia usługi Azure AD B2C tooopen nową kartę przeglądarki bezpośrednio w dzierżawie tooyour B2C blok ustawień
- Prześlij żądanie pomocy technicznej
- Przenieść użytkownika tooanother zasobów dzierżawy B2C subskrypcji Azure lub tooanother grupy zasobów.  Zmiany tego wyboru subskrypcji Azure, której odbiera opłaty za użycie.

![Ustawienia zasobu B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>Znane problemy
- Usuwanie dzierżawy B2C. Jeśli dzierżawy B2C jest tworzony, usunięty i utworzony ponownie z hello tej samej nazwy domeny, należy również usunąć i utworzyć ponownie hello zasobu "Połączeń" hello tą samą nazwą domeny.  Dostępne są to "Konsolidacji" zasobu w obszarze "Wszystkie zasoby" hello subskrypcji dzierżawcy za pośrednictwem hello portalu Azure.
- Własnym narzuconego ograniczenia lokalizacji regionalnych zasobów.  W rzadkich przypadkach użytkownik może nawiązać regionalnych ograniczenia dotyczące tworzenia zasobów platformy Azure.  To ograniczenie może uniemożliwić tworzenie hello hello łącza między subskrypcją platformy Azure i dzierżawy B2C. toomitigate, proszę złagodzenie tego ograniczenia.

## <a name="next-steps"></a>Następne kroki
Po zakończeniu tych kroków dla każdego dzierżawcy usługi B2C, subskrypcji platformy Azure są rozliczane zgodnie z szczegóły bezpośrednie Azure lub umowy Enterprise Agreement.
- Przejrzyj użycie i rozliczenia w wybranej subskrypcji Azure
- Przeglądanie szczegółowe dane użycia każdego dnia raportów za pomocą hello [użycia interfejsu API raportowania](active-directory-b2c-reference-usage-reporting-api.md)
