---
title: "Usługi Azure Active Directory B2C: Atrybuty niestandardowe | Dokumentacja firmy Microsoft"
description: "Jak atrybutów niestandardowych toouse w usłudze Azure Active Directory B2C toocollect informacji o użytkownikach"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a>Usługa Azure Active Directory B2C: Użyj niestandardowych atrybutów toocollect informacji o użytkownikach
Katalogu usługi Azure Active Directory (Azure AD) B2C zawiera zestaw wbudowanych informacji (atrybuty): imię, nazwisko, Miasto, kod pocztowy i innych atrybutów. Jednak każda aplikacja dla użytkownika ma unikatowe wymagania, na jakie toogather atrybuty konsumentów. Z usługi Azure AD B2C można rozszerzyć hello zestaw atrybutów przechowywanych dla każdego konta użytkownika. Atrybuty niestandardowe można tworzyć na powitania [portalu Azure](https://portal.azure.com/) i używać go w wypełnieniu zasad, jak pokazano poniżej. Może także odczytywać i zapisywać te atrybuty przy użyciu hello [interfejsu API usługi Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

> [!NOTE]
> Użyj atrybutów niestandardowych [Azure AD Graph interfejsu API katalogu schematu rozszerzenia](https://msdn.microsoft.com/library/azure/dn720459.aspx).
> 
> 

## <a name="create-a-custom-attribute"></a>Tworzenie niestandardowego atrybutu
1. [Wykonaj te bloku funkcji toohello B2C toonavigate kroki na powitania portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Kliknij przycisk **atrybuty użytkownika**.
3. Kliknij przycisk **+ Dodaj** u góry bloku hello hello.
4. Podaj **nazwa** hello atrybutu niestandardowego (na przykład "ShoeSize") i opcjonalnie **opis**. Kliknij przycisk **Utwórz**.
   
   > [!NOTE]
   > Tylko Witaj, "String" **— typ danych** jest obecnie dostępna.
   > 
   > 

Atrybut niestandardowy Hello jest teraz dostępna w liście hello **atrybuty użytkownika**i do użytku w zasadach tworzenia konta.

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a>Użyj atrybutu niestandardowego w ramach zasad rejestracji
1. [Wykonaj te bloku funkcji toohello B2C toonavigate kroki na powitania portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Kliknij przycisk **Zasady tworzenia konta**.
3. Kliknij przycisk tooopen Twojego zasad rejestracji (na przykład "B2C_1_SiUp") go. Kliknij przycisk **Edytuj** u góry bloku hello hello.
4. Kliknij przycisk **atrybuty rejestracji** i wybierz hello atrybutu niestandardowego (na przykład "ShoeSize"). Kliknij przycisk **OK**.
5. Kliknij przycisk **oświadczenia aplikacji** i wybierz hello atrybutu niestandardowego. Kliknij przycisk **OK**.
6. Kliknij przycisk **zapisać** u góry bloku hello hello.

Można użyć funkcji "Uruchom teraz" hello na powitania zasad tooverify powitania klienta środowisko. Powinny teraz zobacz "ShoeSize" hello liście atrybutów zebrane podczas tworzenia konta użytkownika i zobaczyć ją w hello token wysłany tooyour wstecz aplikacji.

## <a name="notes"></a>Uwagi
* Wraz z zasadami tworzenia konta atrybuty niestandardowe można również zasady rejestracji i logowania i profilu edytowanie zasad.
* Jest to znane ograniczenie atrybutów niestandardowych. Jest tylko utworzyć hello jest używany po raz pierwszy w dowolne zasady, a nie po dodaniu listy toohello **atrybuty użytkownika**.

