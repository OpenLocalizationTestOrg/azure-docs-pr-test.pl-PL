---
title: "aaaRoles w usłudze Azure AD Privileged Identity Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie role są używane do uprzywilejowanymi tożsamościami przy hello rozszerzenie Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Innej roli administracyjnej w usłudze Azure Active Directory PIM
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

Można przypisać użytkowników w organizacji toodifferent role administracyjne w usłudze Azure AD. Te przypisania ról kontrolować, które zadania, takie jak dodawanie lub usuwanie użytkowników lub zmiana ustawień usługi, hello użytkownicy będą mogli tooperform w usłudze Azure AD, Office 365 i innych usług Microsoft Online Services i połączonych aplikacji.  

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.

Administrator globalny może aktualizować której użytkownicy są **trwale** przypisany w usłudze Azure AD przy użyciu poleceń cmdlet programu PowerShell, takich jak tooroles `Add-MsolRoleMember` i `Remove-MsolRoleMember`, lub za pośrednictwem portalu klasycznego hello zgodnie z opisem w [ Przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles.md).

Azure AD Privileged Identity Management (PIM) zarządza zasadami uprzywilejowanego dostępu dla użytkowników w usłudze Azure AD. PIM przypisuje tooone użytkowników lub ról w usłudze Azure AD i można przypisać ktoś toobe trwale w roli hello lub kwalifikujących się do hello roli. Jeśli użytkownik jest trwale przypisana rola tooa lub aktywuje przypisania roli kwalifikujących się, a następnie ich zarządzania usługi Azure Active Directory, usługi Office 365 i innych aplikacji z uprawnieniami hello przypisane role tootheir.

Nie ma żadnej różnicy w dostępie hello podane toosomeone na stałe i przypisanie roli kwalifikujących się. Witaj jedyna różnica polega na tym, że niektórzy użytkownicy nie potrzebują dostępu wszystkich czasu hello. Są uprawnione do roli hello i można ją włączyć i wyłączyć po każdej zmianie muszą.

## <a name="roles-managed-in-pim"></a>Role zarządzane w PIM
Zarządzanie tożsamościami uprzywilejowanymi umożliwia przypisywanie ról administratora toocommon użytkowników, w tym:

* **Administrator globalny** (znanego również jako administrator firmy) zawiera funkcje administracyjne tooall dostępu. Może mieć więcej niż jednego administratora globalnego w organizacji. Hello osoby, która zarejestruje się toopurchase usługi Office 365 automatycznie staje się globalnego administratora.
* **Administrator ról uprzywilejowanych** zarządza Azure AD PIM i aktualizuje przypisania roli dla innych użytkowników.  
* **Administrator rozliczeń** dokonuje zakupów, zarządza subskrypcjami, zarządza biletami pomocy technicznej i monitoruje kondycję usługi.
* **Administrator haseł** Resetuje hasła, zarządza żądaniami obsługi i monitoruje kondycję usługi. Administratorzy haseł są ograniczone tooresetting hasła dla użytkowników.
* **Administrator usługi** zarządza żądaniami obsługi i monitoruje kondycję usługi.
  
  > [!NOTE]
  > Jeśli używasz usługi Office 365 przed przypisaniem hello usługi roli tooa administrator, najpierw przypisywane uprawnienia administracyjne hello użytkownika usługi tooa, takich jak Exchange Online.
  > 
  > 
* **Administrator zarządzania użytkownikami** Resetuje hasła, monitoruje kondycję usługi oraz zarządza kontami użytkowników, grup użytkowników i żądań obsługi. Witaj, Administratorze zarządzania użytkownika nie można usunąć administratora globalnego, tworzenia innych ról administratora lub resetowania haseł dla rozliczeń, globalnych i administratorów usługi.
* **Administrator programu Exchange** ma dostęp administracyjny tooExchange Online za pośrednictwem Centrum administracyjnego programu Exchange hello (EAC) i można wykonać prawie wszystkie zadania w usłudze Exchange Online.
* **Administrator programu SharePoint** ma dostęp administracyjny tooSharePoint Online za pomocą Centrum administracyjnego usługi SharePoint Online hello i można wykonać prawie wszystkie zadania w usłudze SharePoint Online.
* **Skype dla firm administratora** ma tooSkype dostępu administracyjnego dla firm za pomocą hello Skype dla firm Centrum administracyjnego, a można wykonać prawie wszystkie zadania w programie Skype dla firm Online.

Przeczytaj następujące artykuły, aby uzyskać więcej informacji na temat [przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md) i [przypisywanie ról administratora w usłudze Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


Za pomocą usługi PIM, można [Przypisz te role użytkowników tooa](active-directory-privileged-identity-management-how-to-add-role-to-user.md) tak, aby hello użytkownik może [Uaktywnij rolę hello w razie potrzeby](active-directory-privileged-identity-management-how-to-activate-role.md).

Jeśli chcesz toogive innego toomanage dostępu użytkownika w PIM, hello ról, które wymaga PIM toohave użytkownika hello są opisane dalej w [jak toogive dostępu tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>Role nie są zarządzane w PIM
Role w ramach usługi Exchange Online lub SharePoint Online, z wyjątkiem wymienionych powyżej, nie są reprezentowane w usłudze Azure AD i dlatego nie są widoczne w PIM. Aby uzyskać więcej informacji na temat zmieniania przypisań ról szczegółowych w tych usług Office 365, zobacz [uprawnienia w usłudze Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).

Subskrypcje platformy Azure i grup zasobów również nie są reprezentowane w usłudze Azure AD. toomanage Azure subskrypcji, zobacz [jak tooadd lub zmień role administratora platformy Azure](../billing/billing-add-change-azure-subscription-administrator.md) i uzyskać więcej informacji o Azure RBAC, zobacz [kontroli dostępu](role-based-access-control-configure.md).

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>Role użytkownika i logowanie
Dla pewnych usług firmy Microsoft i aplikacji, przypisywanie roli tooa użytkownika może nie być wystarczające tooenable toobe tego użytkownika administrator.

Toohello dostępu do klasycznego portalu Azure wymaga hello użytkownik jest administratorem usługi ani współadministratorem subskrypcji platformy Azure, nawet jeśli użytkownik hello nie wymagają toomanage hello subskrypcji platformy Azure.  Na przykład toomanage ustawienia konfiguracji dla usługi Azure AD w portalu klasycznym hello, użytkownik musi być zarówno w usłudze Azure AD administratora globalnego, jak i subskrypcji współadministratorem subskrypcji platformy Azure.  toolearn tooadd subskrypcji tooAzure użytkowników, zobacz temat [jak tooadd lub zmień role administratora platformy Azure](../billing/billing-add-change-azure-subscription-administrator.md).

TooMicrosoft dostęp do usług Online może wymagać hello użytkownika również należy przypisać im licencję przed ich Otwórz portal usługi hello, lub wykonywać zadania administracyjne.

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>Przypisywanie licencji użytkownika tooa w usłudze Azure AD
1. Zaloguj się toohello [klasycznego portalu Azure](http://manage.windowsazure.com) z konta administratora globalnego lub konto administratora współpracującego.
2. Wybierz **wszystkie elementy** z hello menu głównego.
3. Wybierz katalog hello toowork z i że licencji skojarzył z nim.
4. Wybierz **licencji**. zostanie wyświetlona lista Hello dostępnych licencji.
5. Wybierz plan licencji hello, który zawiera hello licencji, które mają toodistribute.
6. Wybierz **przypisywać użytkowników**.
7. Wybierz hello użytkownika, które mają tooassign licencję do.
8. Kliknij przycisk hello **przypisać** przycisku.  Witaj, użytkownik może teraz logować tooAzure.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

