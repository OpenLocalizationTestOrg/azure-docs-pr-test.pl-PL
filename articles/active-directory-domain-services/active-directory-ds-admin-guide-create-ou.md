---
title: "Usługami domenowymi Azure Active Directory: Przewodnik administrowania | Dokumentacja firmy Microsoft"
description: "Tworzenie jednostki organizacyjnej (OU) w domenach zarządzanych usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>Tworzenie jednostki organizacyjnej (OU) w domenie zarządzanej usług domenowych Azure AD
Azure domen zarządzanych w usługach domenowych AD to dwa wbudowane kontenery odpowiednio o nazwie "AADDC komputery" i "AADDC użytkowników". Witaj "AADDC komputery" kontenera znajdują się obiekty komputera dla wszystkich komputerów, które są przyłączone do domeny zarządzanej toohello. kontener "Użytkownicy AADDC" Hello zawiera użytkowników i grup w hello dzierżawy usługi Azure AD. Czasami może być konieczne toocreate kont usług na powitania zarządzane domeny toodeploy obciążeń. W tym celu można utworzyć niestandardowy jednostki organizacyjnej (OU) w domenie zarządzanej hello i tworzenie konta usług w tej jednostce Organizacyjnej. W tym artykule opisano sposób toocreate jednostki Organizacyjnej w domenie zarządzanej.

## <a name="before-you-begin"></a>Przed rozpoczęciem
zadania hello tooperform wymienione w tym artykule, potrzebne są:

1. Prawidłowy **subskrypcji platformy Azure**.
2. **Katalog usługi Azure AD** -albo synchronizowane z katalogu lokalnego lub w katalogu tylko w chmurze.
3. **Usługi domenowe Azure AD** musi być włączona dla katalogu hello Azure AD. Jeśli nie zostało to jeszcze zrobione, należy wykonać wszystkie zadania hello opisane w hello [Przewodnik wprowadzający](active-directory-ds-getting-started.md).
4. Z którego administrujesz usług domenowych w usłudze hello Azure AD maszynę wirtualną przyłączonych do domeny zarządzania domeny. Jeśli nie masz maszynę wirtualną, należy wykonać wszystkie zadania hello opisane w artykule hello zatytułowany [Dołącz do domeny zarządzanej tooa maszyny wirtualnej systemu Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Wymagane poświadczenia hello **użytkownika konto należące toohello "AAD kontrolera domeny" Administratorzy** w katalogu toocreate niestandardowej jednostki Organizacyjnej w domenie zarządzanej.

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>Zainstalować narzędzia administracji AD na maszynie wirtualnej przyłączonych do domeny dla administracji zdalnej
Azure domen zarządzanych w usługach domenowych AD można zarządzać zdalnie za pomocą znanych narzędzi administracyjnych usługi Active Directory takich jak hello Centrum administracyjne Active Directory (ADAC) lub AD PowerShell. Administratorzy dzierżawy nie mają uprawnień tooconnect toodomain kontrolerów na powitania domeny zarządzanej za pośrednictwem pulpitu zdalnego. tooadminister hello domeny zarządzanej, zainstaluj funkcji narzędzia administracji hello AD na toohello przyłączone do domeny zarządzanej maszyny wirtualnej. Zobacz artykuł toohello [administrowania domeny zarządzanej usług domenowych Azure AD](active-directory-ds-admin-guide-administer-domain.md) instrukcje.

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>Utwórz jednostkę organizacyjną na powitania domeny zarządzanej
Teraz, gdy są zainstalowane narzędzia administracyjne hello AD na powitania przyłączonych do domeny maszyny wirtualnej, możemy użyć tych narzędzi toocreate jednostki organizacyjnej w domenie hello zarządzane. Wykonaj następujące kroki hello:

> [!NOTE]
> Tylko członkowie grupy "Administratorzy kontrolera domeny usługi AAD" hello ma hello toocreate wymagane uprawnienia niestandardowe jednostki Organizacyjnej. Upewnij się, należy wykonać następujące kroki jako użytkownik będący członkiem grupy toothis hello.
>
>

1. Na ekranie startowym powitania kliknij **narzędzia administracyjne**. Narzędzia administracyjne hello AD zainstalowany na maszynie wirtualnej hello powinna zostać wyświetlona.

    ![Narzędzia administracyjne zainstalowane na serwerze](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Kliknij przycisk **Centrum administracyjne usługi Active Directory**.

    ![Centrum administracyjne usługi Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooview hello domeny, kliknij nazwę domeny hello w okienku po lewej stronie powitania (na przykład "contoso100.com").

    ![ADAC — widok domeny](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. Hello prawej strony **zadania** okienku, kliknij przycisk **nowy** węźle hello nazwy domeny. W tym przykładzie mamy kliknij **nowy** w węźle "contoso100(local)" hello hello prawej strony **zadania** okienka.

    ![ADAC - nową jednostkę Organizacyjną](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. Powinny pojawić się hello opcja toocreate jednostki organizacyjnej. Kliknij przycisk **jednostki organizacyjnej** toolaunch hello **Utwórz jednostkę organizacyjną** okna dialogowego.
6. W hello **Utwórz jednostkę organizacyjną** okna dialogowego, określ **nazwa** dla hello nowej jednostki Organizacyjnej. Podaj krótki opis hello jednostki Organizacyjnej. Można również ustawić hello **zarządzany przez** pole hello jednostki Organizacyjnej. toocreate hello niestandardowej jednostki Organizacyjnej, kliknij przycisk **OK**.

    ![ADAC — Tworzenie jednostki Organizacyjnej w oknie dialogowym](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. nowo utworzone jednostki Organizacyjnej Hello powinien zostać wyświetlony hello AD Centrum administracyjne (ADAC).

    ![ADAC - utworzyć jednostkę Organizacyjną](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>Uprawnienia/zabezpieczeń dla nowo utworzonej jednostki organizacyjne
Domyślnie użytkownika hello (członek grupy hello "Administratorzy kontrolera domeny usługi AAD"), który utworzył powitalne niestandardowej jednostki Organizacyjnej ma przywileje administracyjne (Pełna kontrola) za pośrednictwem hello jednostki Organizacyjnej. Witaj użytkownika można teraz i przyznać uprawnienia tooother użytkowników lub grupy "Administratorzy kontrolera domeny usługi AAD" toohello zgodnie z potrzebami. Jak pokazano w hello następującego zrzutu ekranu, hello użytkownika "bob@domainservicespreview.onmicrosoft.com" kto nową jednostkę organizacyjną utworzony hello "MyCustomOU" jest uprawnienie do pełnej kontroli nad nim.

 ![ADAC - nowych zabezpieczeń jednostki Organizacyjnej](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>Uwagi dotyczące administrowania niestandardowych jednostek organizacyjnych
Teraz, po utworzeniu niestandardowej jednostki Organizacyjnej, można teraz i tworzenie użytkowników, grup komputerów i kont usług w tej jednostce Organizacyjnej. Nie można przenieść użytkowników lub grup z hello jednostek organizacyjnych toocustom jednostki Organizacyjnej "AADDC użytkowników".

> [!WARNING]
> Konta użytkowników, grup, kont usług i obiektów komputerów, utworzone w obszarze niestandardowych jednostek organizacyjnych nie są dostępne w dzierżawie usługi Azure AD. Innymi słowy te obiekty nie są wyświetlane przy użyciu interfejsu API Azure AD Graph hello lub hello interfejsu użytkownika programu Azure AD. Te obiekty są dostępne tylko w domenie zarządzanej usług domenowych Azure AD.
>
>

## <a name="related-content"></a>Powiązana zawartość
* [Administrowanie domeną zarządzaną usług Azure AD Domain Services](active-directory-ds-admin-guide-administer-domain.md)
* [Konfigurowanie zasad grupy w domenie zarządzanej](active-directory-ds-admin-guide-administer-group-policy.md)
* [Centrum administracyjne usługi Active Directory: Wprowadzenie](https://technet.microsoft.com/library/dd560651.aspx)
* [Przewodnik krok po kroku dotyczący kont usług](https://technet.microsoft.com/library/dd548356.aspx)
