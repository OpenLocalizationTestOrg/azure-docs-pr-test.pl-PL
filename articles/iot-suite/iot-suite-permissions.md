---
title: Pakiet Azure IoT i Azure Active Directory | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak pakiet IoT Azure używa usługi Azure Active Directory do zarządzania uprawnieniami."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/10/2017
ms.author: dobett
ms.openlocfilehash: e5804cda921e9d598d0ed02c4fafccdb40fbe7a5
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a>Uprawnienia w witrynie the azureiotsuite.com

## <a name="what-happens-when-you-sign-in"></a>Co się stanie po zalogowaniu

Przy pierwszym zalogowaniu się na [azureiotsuite.com][lnk-azureiotsuite], witryny Określa poziomy uprawnień, należy mieć na podstawie aktualnie wybranej dzierżawy usługi Azure Active Directory (AAD) i subskrypcji platformy Azure.

1. Najpierw do wypełnienia listy dzierżawców widoczne obok nazwy użytkownika, lokacji znajduje na platformie Azure dzierżaw usługi AAD, które należą do. Obecnie witryny można uzyskać tokeny użytkownika dla jednego dzierżawcy w czasie. W związku z tym podczas przełączania dzierżawcy przy użyciu listy rozwijanej w prawym górnym rogu lokacji rejestruje w tej dzierżawy uzyskać tokenów dla tej dzierżawy.

2. Następnie lokacji znajduje z platformy Azure, subskrypcje, które zostały skojarzone z wybranej dzierżawy. Podczas tworzenia nowego rozwiązania wstępnie skonfigurowane są wyświetlane dostępnych subskrypcji.

3. Na koniec lokacji pobiera wszystkie zasoby w subskrypcji i grup zasobów oznakowane jako wstępnie skonfigurowanych rozwiązań i wypełnia Kafelki na stronie głównej.

W poniższych sekcjach opisano role, które kontrolują dostęp do wstępnie skonfigurowanych rozwiązań.

## <a name="aad-roles"></a>Role usługi AAD

Role AAD kontrolowanie możliwości rozwiązania wstępnie udostępnić i zarządzanie użytkownikami w wstępnie skonfigurowane rozwiązanie.

Można znaleźć więcej informacji na temat ról administratorów w usłudze AAD w [przypisywanie ról administratorów w usłudze Azure AD][lnk-aad-admin]. Bieżący artykuł skupia się na **administratora globalnego** i **użytkownika** ról katalogu jako używane przez wstępnie skonfigurowanych rozwiązań.

### <a name="global-administrator"></a>Administrator globalny

Może istnieć wiele Administratorzy globalni na dzierżawę usługi AAD:

* Podczas tworzenia dzierżawy usługi AAD jest domyślnie administratora globalnego tej dzierżawy.
* Administrator globalny może udostępnić basic i standard wstępnie skonfigurowanych rozwiązań.

### <a name="domain-user"></a>Użytkownik domeny

Może istnieć wiele użytkowników domeny w dzierżawie usługi AAD:

* Użytkownik domeny można udostępnić podstawowego rozwiązania wstępnie skonfigurowane w ramach [azureiotsuite.com] [ lnk-azureiotsuite] lokacji.
* Użytkownik domeny, można utworzyć podstawowego rozwiązania wstępnie skonfigurowane przy użyciu interfejsu wiersza polecenia.

### <a name="guest-user"></a>Gość

Może istnieć wiele gości na dzierżawę usługi AAD. Goście mają ograniczony zestaw praw w dzierżawie usługi AAD. W związku z tym gości nie może obsłużyć wstępnie skonfigurowane rozwiązanie w dzierżawie usługi AAD.

Aby uzyskać więcej informacji dotyczących użytkowników i role w usłudze AAD zobacz następujące zasoby:

* [Tworzenie użytkowników w usłudze Azure AD][lnk-create-edit-users]
* [Przypisywanie użytkowników do aplikacji][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Role administratorów subskrypcji platformy Azure

Role administratora platformy Azure kontrolować możliwość mapowania subskrypcji platformy Azure do dzierżawy usługi AD.

Dowiedz się więcej o rolach administratora platformy Azure w artykule [jak dodać lub zmienić administratora współpracującego Azure, Administrator usługi i konto administratora][lnk-admin-roles].

## <a name="faq"></a>Często zadawane pytania

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>Jestem administratorem usługi, a chcę zmienić katalogu mapowanie między mojej subskrypcji i określonych dzierżawę usługi AAD. Jak wykonać to zadanie?

Zobacz [Aby dodać istniejącą subskrypcję do katalogu usługi Azure AD](../active-directory/active-directory-how-subscriptions-associated-directory.md#to-associate-an-existing-subscription-to-your-azure-ad-directory)

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>Zmienianie administratorem usługi ani Współadministratorem podczas logowania się za pomocą konta organizacyjnego

Zobacz artykuł pomocy technicznej [zmiany administratora usługi i Współadministrator podczas logowania się przy użyciu konta organizacyjne][lnk-service-admins].

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>Dlaczego widzę ten błąd? "Twoje konto nie ma odpowiednich uprawnień do utworzenia rozwiązania. Spróbuj skontaktować się z administratorem konta lub za pomocą innego konta."

Szukaj na poniższym diagramie, aby uzyskać wskazówki:

![][img-flowchart]

> [!NOTE]
> Jeśli nadal wyświetlany błąd po weryfikacji można administratora globalnego dla dzierżawcy usługi AAD i współadministratorem subskrypcji, poproś administratora konta, Usuń użytkownika i przypisać odpowiednie uprawnienia w podanej kolejności. Najpierw dodaj użytkownika jako administrator globalny, a następnie dodaj użytkownika jako współadministratorem subskrypcji platformy Azure. Jeśli problemy będą się powtarzać, skontaktuj się z [Pomoc i obsługa techniczna][lnk-help-support].

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>Dlaczego widzę ten błąd gdy subskrypcji platformy Azure? "Subskrypcji platformy Azure jest wymagane do utworzenia wstępnie skonfigurowanych rozwiązań. Użytkownik może utworzyć bezpłatne konto próbne w zaledwie kilka minut."

Jeśli masz pewność, że masz subskrypcję platformy Azure, sprawdź poprawność mapowania dla Twojej subskrypcji dzierżawcy i upewnij się, że wybrano poprawny dzierżawy na liście rozwijanej. Jeśli zostały sprawdzone żądaną dzierżawy jest poprawna, postępuj zgodnie z wcześniejszym diagramie i sprawdzić poprawności mapowania subskrypcji i tego dzierżawę usługi AAD.

## <a name="next-steps"></a>Kolejne kroki
Aby kontynuować zapoznawanie pakiet IoT, zobacz temat [dostosować wstępnie skonfigurowane rozwiązanie][lnk-customize].

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
