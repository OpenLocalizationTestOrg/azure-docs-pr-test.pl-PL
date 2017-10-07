---
title: "aaaManage hello katalogu dla subskrypcji usługi Office 365 na platformie Azure | Dokumentacja firmy Microsoft"
description: "Zarządzanie katalogiem subskrypcji usługi Office 365 przy użyciu usługi Azure Active Directory i hello klasycznego portalu Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>Zarządzanie hello katalogu dla subskrypcji usługi Office 365 na platformie Azure
W tym artykule opisano sposób toomanage katalogu, który został utworzony dla subskrypcji usługi Office 365 przy użyciu hello klasycznego portalu Azure. Musi być hello Administrator usługi albo współadministratorem subskrypcji platformy Azure toosign w toohello klasycznego portalu Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, już dziś możesz zarejestrować się w celu uzyskania [bezpłatnej 30-dniowej wersji próbnej](https://azure.microsoft.com/trial/get-started-active-directory/) i za pomocą tego łącza w ciągu 5 minut wdrożyć swoje pierwsze rozwiązanie w chmurze. Można pracy hello toouse się, że konto służbowe Użyj toosign w tooOffice 365.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.

Po ukończeniu hello subskrypcji platformy Azure można zarejestrować toohello klasycznego portalu Azure i uzyskiwać dostęp do usług Azure. Kliknij rozszerzenie usługi Active Directory hello toomanage hello tym samym katalogu, który służy do uwierzytelniania użytkowników usługi Office 365.

Jeśli masz już subskrypcję platformy Azure, toomanage procesu hello kolejnego katalogu jest również oczywisty. Na przykład Jan Nowak może mieć subskrypcję usługi Office 365 dla domeny Contoso.com. Ma on także subskrypcję platformy Azure, którą uzyskał przy użyciu swojego konta Microsoft msmith@hotmail.com. W takim przypadku zarządza dwoma katalogami.

| Subskrypcja | Office 365 | Azure |
| --- | --- | --- |
|   Nazwa wyświetlana |Contoso |Domyślny katalog Azure Active Directory (Azure AD) |
|   Nazwa domeny |contoso.com |jnowakhotmail.onmicrosoft.com |

Maciej chce tożsamości użytkownika hello toomanage w katalogu firmy Contoso hello, gdy jest on podpisany tooAzure przy użyciu swojego konta Microsoft, aby mógł włączać funkcje usługi Azure AD, takie jak uwierzytelnianie wieloskładnikowe. powitania po diagram może pomóc tooillustrate hello procesu.

![Diagram toomanage dwoma niezależnymi katalogami](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

W takim przypadku hello dwa katalogi są od siebie niezależne.

## <a name="toomanage-two-independent-directories"></a>toomanage dwoma niezależnymi katalogami
W celu dla toomanage Jan Nowak obu katalogów jest on zalogowany w tooAzure jako msmith@hotmail.com, musi wykonać następujące kroki hello:

> [!NOTE]
> Te kroki można wykonać tylko wtedy, gdy użytkownik jest zalogowany za pomocą konta Microsoft. Jeśli hello użytkownik jest zalogowany za pomocą konta służbowego, hello opcja zbyt**Użyj istniejącego katalogu** nie jest dostępna. Konto służbowe można uwierzytelnić tylko za pomocą jego katalogu macierzystego (oznacza to, że hello katalog w którym hello służbowe konto jest przechowywane, jest właścicielem tego hello firmy lub szkoły).
>
>

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) jako msmith@hotmail.com.
2. Kliknij pozycje **Nowy** > **App Services** > **Active Directory** > **Katalog** > **Utwórz niestandardowy**.
3. Kliknij opcję Użyj istniejącego katalogu i zaznacz hello **jestem toobe gotowa, teraz wylogować** wyboru.
4. Zaloguj się toohello klasycznego portalu Azure jako administrator globalny domeny Contoso.onmicrosoft.com (na przykład msmith@contoso.com).
5. Po wyświetleniu monitu zbyt**Użyj hello Contoso katalogu platformy Azure?**, kliknij przycisk **Kontynuuj**.
6. Kliknij pozycję **Wyloguj się teraz**.
7. Zaloguj się toohello klasycznego portalu Azure jako msmith@hotmail.com. hello katalogu firmy Contoso i katalog domyślny hello są wyświetlane w hello rozszerzenie usługi Active Directory.

Po wykonaniu tych czynności msmith@hotmail.com jest administratorem globalnym w katalogu firmy Contoso hello.

## <a name="tooadminister-resources-as-hello-global-admin"></a>zasoby tooadminister jako hello Administrator globalny
Teraz załóżmy, że Anna Kowalska musi administrować witrynami sieci Web i bazy danych zasobów, które są skojarzone z hello subskrypcji platformy Azure dla msmith@hotmail.com. Aby mogła to zrobić, Jan Nowak musi toocomplete te dodatkowe kroki:

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) przy użyciu konta administratora usługi hello na powitania subskrypcji platformy Azure (w tym przykładzie msmith@hotmail.com).
2. Transfer katalogu firmy Contoso toohello subskrypcji hello: kliknij **ustawienia** > **subskrypcje** > Wybierz subskrypcję hello > **Edytuj katalog** > Wybierz **Contoso (Contoso.com)**. W ramach transferu hello, wszelkie służbowego konta, które mają uprawnień współadministratorów subskrypcji hello są usuwane.
3. Dodać Annę Kowalską jako współadministratora subskrypcji hello: kliknij **ustawienia** > **Administratorzy** > wybrać subskrypcję hello > **Dodaj** > typu **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat hello relacji między subskrypcjami i katalogami, zobacz [jak subskrypcja jest skojarzona z katalogiem](active-directory-how-subscriptions-associated-directory.md).
