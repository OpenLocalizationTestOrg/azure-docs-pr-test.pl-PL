---
title: "aaaManaging grup w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toocreate i Zarządzaj grupami toomanage Azure użytkowników przy użyciu usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>Zarządzanie grupami w usłudze Azure Active Directory
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Jedną z funkcji hello zarządzania użytkownika usługi Azure Active Directory (Azure AD) jest hello możliwości toocreate grup użytkowników. Możesz użyć zadania zarządzania tooperform grupy, takich jak przypisywanie licencji lub uprawnienia tooa liczbę użytkowników jednocześnie. Można również użyć grup tooassign uprawnienia do dostępu

* Zasoby, takie jak obiekty w katalogu hello
* Zasoby zewnętrzne toohello katalogu, takiego jak aplikacji SaaS, usług platformy Azure, witryn programu SharePoint lub zasobów lokalnych

Ponadto właściciel zasobu można również przypisywać właścicielem dostępu tooa zasobów tooan usługi Azure AD grupy. To przypisanie daje członkom hello zasobu toohello dostęp do tej grupy. Następnie hello właściciela grupy hello zarządza członkostwo w grupie hello. Ostatecznie hello zasobów właściciela delegatów toohello właściciel hello grupy hello uprawnienia tooassign użytkowników tootheir zasobu.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Aby uzyskać jak toomanage grupuje się w Centrum administracyjnym hello Azure AD, zobacz [Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory](active-directory-groups-create-azure-portal.md).

## <a name="how-do-i-create-a-group"></a>Jak utworzyć grupę?
W zależności od hello toowhich usług, które zostały zasubskrybowane przez organizację można utworzyć grupę przy użyciu jednej z następujących hello:

* Witaj klasycznego portalu Azure
* portal konta Hello usługi Office 365
* Witaj w portalu konta Windows Intune

Opiszemy zadania, jak wykonywać w hello klasycznego portalu Azure. Aby uzyskać więcej informacji o użyciu portali innych niż Azure toomanage katalogu usługi Azure AD, zobacz [administrowanie katalogiem usługi Azure AD](active-directory-administer.md).

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu organizacji.
2. Wybierz hello **grup** kartę.
3. Wybierz polecenie **Dodaj grupę**.
4. W hello **Dodaj grupę** okna, określ nazwę hello i hello opis grupy.

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>Jak dodawać i usuwać pojedynczych użytkowników w grupie zabezpieczeń?
**tooadd grupy tooa użytkownika**

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu organizacji.
2. Wybierz hello **grup** kartę.
3. Otwórz toowhich grupy hello tooadd członkowie. Otwórz hello **członków** kartę hello wybrane grupy, jeśli go jeszcze nie wyświetlanie.
4. Wybierz polecenie **Dodaj członków**.
5. Na powitania **Dodaj członków** strony, wybierz opcję hello nazwę hello użytkownik lub grupa ma tooadd członkiem tej grupy. Upewnij się, że nazwa została dodana toohello **wybrane** okienka.

**tooremove użytkownika z grupy**

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu organizacji.
2. Wybierz hello **grup** kartę.
3. Otwórz grupę hello, z którego mają być członkami tooremove.
4. Wybierz hello **członków** kartę, wybierz hello nazwę elementu członkowskiego hello mają tooremove z tej grupy, a następnie kliknij przycisk **Usuń**.
5. Potwierdzenie w wierszu hello tooremove tego elementu członkowskiego z grupy hello.

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>Jak dynamicznie zarządzać hello członkostwa w grupie?
W usłudze Azure AD można bardzo łatwo skonfigurować toodetermine Prosta reguła, użytkowników, którzy są członkami toobe hello grupy. Prosta reguła to taka, która wykonuje tylko jedno porównanie. Na przykład jeśli grupa jest przypisana tooa aplikacji SaaS, można ustawić reguły użytkowników tooadd, mających stanowisko "Przedstawiciel". Ta reguła jest następnie udziela dostępu użytkowników tooall aplikacji SaaS toothis stanowisko w katalogu.

Gdy atrybuty zmian użytkownika, powitalne system ocenia wszystkie reguły grupy dynamicznej w toosee katalogu, jeśli zmiany atrybutu hello hello użytkownika spowoduje wywołanie żadnej grupy dodaje lub usuwa. Jeśli użytkownika spełnia zasady grupy, są dodawane jako członek grupy toothat. Jeśli nie spełniają hello zasady grupy, które są członkami, są usuwane jako elementy członkowskie z tej grupy.

> [!NOTE]
> Możesz skonfigurować reguły dynamicznego zarządzania członkostwem w grupach zabezpieczeń lub w grupach usługi Office 365. Członkostwo grup zagnieżdżonych nie są obecnie obsługiwane dla tooapplications przypisywania na podstawie grupy.
>
> Dynamiczne zarządzanie członkostwem w grupach wymaga toobe licencji Azure AD Premium, przypisane do
>
> * Witaj administratora, który zarządza hello regułą grupy
> * Wszyscy członkowie grupy hello
>
>

**tooenable członkostwo dynamiczne w grupie**

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie wybierz nazwę hello hello katalogu organizacji.
2. Wybierz hello **grup** kartę i hello Otwórz grupę tooedit.
3. Wybierz hello **Konfiguruj** karcie, a następnie ustaw **Włącz członkostwo dynamiczne** za**tak**.
4. Skonfiguruj prostą regułę dla toocontrol grupy hello członkostwo dynamiczne w grupie. Upewnij się, że hello **dodawania użytkowników gdzie** opcja jest zaznaczona, a następnie wybierz właściwość użytkownika z listy hello (na przykład dział, stanowisko, itp.),
5. Następnie wybierz warunek (Nie równa się, Równa się, Nie rozpoczyna się od, Rozpoczyna się od, Nie zawiera, Zawiera, Nie jest zgodne, Jest zgodne).
6. Określ wartość porównania hello wybrane właściwości użytkownika.

toolearn o tym, jak toocreate *zaawansowane* reguły (zasady, które mogą zawierać więcej niż jedno porównanie) na dynamiczne członkostwo w grupie, zobacz [przy użyciu atrybutów toocreate zaawansowane zasady](active-directory-accessmanagement-groups-with-advanced-rules.md).

## <a name="additional-information"></a>Dodatkowe informacje
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Co to jest usługa Azure Active Directory?](active-directory-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
