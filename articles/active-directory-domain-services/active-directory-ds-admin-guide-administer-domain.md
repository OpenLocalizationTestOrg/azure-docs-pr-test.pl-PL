---
title: "Azure Active Directory Domain Services: Administrowanie domeną zarządzaną | Dokumentacja firmy Microsoft"
description: "Administrowanie domeny zarządzanej usług domenowych Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>Administrowanie domeną zarządzaną usług domenowych Azure Active Directory
W tym artykule opisano sposób zarządzania domeny w tooadminister usług domenowych w usłudze Azure Active Directory (AD).

## <a name="before-you-begin"></a>Przed rozpoczęciem
zadania hello tooperform wymienione w tym artykule, potrzebne są:

1. Prawidłowy **subskrypcji platformy Azure**.
2. **Katalog usługi Azure AD** -albo synchronizowane z katalogu lokalnego lub w katalogu tylko w chmurze.
3. **Usługi domenowe Azure AD** musi być włączona dla katalogu hello Azure AD. Jeśli nie zostało to jeszcze zrobione, należy wykonać wszystkie zadania hello opisane w hello [Przewodnik wprowadzający](active-directory-ds-getting-started.md).
4. A **przyłączonych do domeny maszyny wirtualnej** z którego administrujesz hello domeny zarządzanej usług domenowych Azure AD. Jeśli nie masz maszynę wirtualną, należy wykonać wszystkie zadania hello opisane w artykule hello zatytułowany [Dołącz do domeny zarządzanej tooa maszyny wirtualnej systemu Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Wymagane poświadczenia hello **użytkownika konto należące toohello "AAD kontrolera domeny" Administratorzy** w katalogu tooadminister domeny zarządzanej.

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>Zadania administracyjne, które można wykonywać na domeny zarządzanej
Członkowie grupy "Administratorzy kontrolera domeny usługi AAD" hello są przyznawane uprawnienia na powitania domeny zarządzanej, umożliwiających im tooperform zadań takich jak:

* Dołącz do domeny zarządzanej toohello maszyny.
* Skonfiguruj hello wbudowanego obiektu zasad grupy dla kontenerów "AADDC komputery" i "Użytkownicy AADDC" hello w hello domeny zarządzanej.
* Administrowanie systemem DNS na powitania domeny zarządzanej.
* Utwórz i administrować niestandardowych jednostek organizacyjnych (OU) na powitania domeny zarządzanej.
* Korzyści dostępu administracyjnego toocomputers przyłączone do domeny zarządzanej toohello.

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>Uprawnienia administracyjne, które nie znajdują się w domeny zarządzanej
domeny Hello jest zarządzany przez firmę Microsoft, w tym działania, takie jak stosowanie poprawek, monitorowania i wykonywania kopii zapasowych. W związku z tym domeny hello jest zablokowana i nie masz uprawnień tooperform niektórych zadań administracyjnych na powitania domeny. Przykładowe zadania, którego nie można wykonać to poniżej.

* Nie udzielono uprawnień administratora domeny lub administratora przedsiębiorstwa dla domeny zarządzanej hello.
* Nie można rozszerzyć schemat hello hello domeny zarządzanej.
* Nie można połączyć toodomain kontrolery hello zarządzane przy użyciu pulpitu zdalnego.
* Nie można dodać domeny zarządzanej toohello kontrolerów domeny.

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>Zadanie 1 - Provision przyłączonych do domeny systemu Windows Server tooremotely maszyny wirtualnej administrowania hello domeny zarządzanej
Azure domen zarządzanych w usługach domenowych AD mogą być zarządzane przy użyciu znanych narzędzi administracyjnych usługi Active Directory takie jak hello Centrum administracyjne Active Directory (ADAC) lub AD PowerShell. Administratorzy dzierżawy nie mają uprawnień tooconnect toodomain kontrolerów na powitania domeny zarządzanej za pośrednictwem pulpitu zdalnego. W związku z tym członkami hello, które mogą administrować grupy "Administratorzy kontrolera domeny usługi AAD" zarządzane domeny zdalnie przy użyciu narzędzi administracyjnych AD z komputera klienta serwera systemu Windows, który jest toohello przyłączone do domeny zarządzanej. Narzędzia administracyjne AD można zainstalować jako część hello opcjonalna funkcja narzędzi administracji zdalnej serwera (RSAT) na komputerach z systemem Windows Server i klienta przyłączone do domeny toohello zarządzane.

pierwszym krokiem Hello jest tooset zapasowej maszyny wirtualnej systemu Windows Server, która jest domeną toohello dołączonego do zarządzanych. Instrukcje można znaleźć w artykule toohello zatytułowany [przyłączyć się do systemu Windows Server maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny](active-directory-ds-admin-guide-join-windows-vm.md).

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>Zdalne administrowanie domeny zarządzanej hello z komputera klienckiego (na przykład system Windows 10)
Witaj instrukcje w tym artykule serwera Windows hello tooadminister maszyny wirtualnej usługi AAD DS zarządzane domeny. Jednak możesz również toouse toodo maszyny wirtualnej klienta (na przykład system Windows 10) systemu Windows tak.

Możesz [zainstalować narzędzia administracji zdalnej serwera (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) na maszynie wirtualnej klienta systemu Windows, wykonując następujące instrukcje hello w witrynie TechNet.

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>Zadanie 2 — Witaj maszyny wirtualnej w narzędziach administracyjnych instalacji usługi Active Directory
Wykonaj hello następujące narzędzia administrowania Active Directory hello tooinstall kroki na maszynie wirtualnej hello przyłączony do domeny. Aby uzyskać więcej informacji zobacz temat Technet [informacji o instalowaniu i używaniu narzędzi administracji zdalnej serwera](https://technet.microsoft.com/library/hh831501.aspx).

1. Przejdź za**maszyn wirtualnych** węzła w hello klasycznego portalu Azure. Wybierz maszynę wirtualną hello utworzony w zadaniu 1, a następnie kliknij przycisk **Connect** na pasku poleceń hello u dołu okna hello hello.

    ![Połącz tooWindows maszyny wirtualnej](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. klasyczny portal Hello monit tooopen lub Zapisz plik z rozszerzeniem "RDP", który jest maszyną wirtualną toohello tooconnect używane. Kliknij plik hello tooopen, po zakończeniu pobierania.
3. W wierszu hello logowania należy użyć hello poświadczenia użytkownika należącego do grupy "Administratorzy kontrolera domeny usługi AAD" toohello. Na przykład używamy "bob@domainservicespreview.onmicrosoft.com" w tym przypadku.
4. Na ekranie startowym hello Otwórz **Menedżera serwera**. Kliknij przycisk **Dodaj role i funkcje** w okienku centralnym hello hello okna Menedżera serwera.

    ![Uruchom Menedżera serwera na maszynie wirtualnej](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. Na powitania **przed rozpoczęciem** strony hello **Kreatora dodawania ról i funkcji**, kliknij przycisk **dalej**.

    ![Przed rozpoczęciem strony](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. Na powitania **typu instalacji** zostaw hello **Instalacja roli lub funkcji** zaznaczoną opcją i kliknij przycisk **dalej**.

    ![Strona Typ instalacji](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. Na powitania **wybór serwera** strony, wybierz z puli serwerów hello hello bieżącej maszyny wirtualnej, a następnie kliknij przycisk **dalej**.

    ![Strona wybierania serwera](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. Na powitania **ról serwera** kliknij przycisk **dalej**. Ponieważ firma Microsoft nie zainstalowano żadnych ról na powitania serwera, Pomiń tę stronę.
9. Na powitania **funkcje** kliknij przycisk tooexpand hello **narzędzi administracji zdalnej serwera** węzła a następnie kliknij przycisk tooexpand hello **narzędzia do administrowania rolami** węzła. Wybierz **usług AD DS i AD LDS narzędzia** funkcję z listy hello narzędzia do administrowania rolami.

    ![Strona funkcji](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. Na powitania **potwierdzenie** kliknij przycisk **zainstalować** tooinstall hello AD i narzędzia usług AD LDS funkcji na powitania maszyny wirtualnej. Po pomyślnym zakończeniu instalacji funkcji, kliknij przycisk **Zamknij** tooexit hello **Dodaj role i funkcje** kreatora.

    ![Strona potwierdzenia](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>Zadanie 3 — Połącz tooand Eksploruj hello domeny zarządzanej
Teraz, gdy są zainstalowane narzędzia administracyjne hello AD na powitania przyłączonych do domeny maszyny wirtualnej, możemy użyć tych narzędzi tooexplore i administrować hello domeny zarządzanej.

> [!NOTE]
> Należy toobe członkiem grupy "Administratorzy kontrolera domeny usługi AAD" hello, tooadminister hello zarządzane domeny.
>
>

1. Na ekranie startowym powitania kliknij **narzędzia administracyjne**. Narzędzia administracyjne hello AD zainstalowany na maszynie wirtualnej hello powinna zostać wyświetlona.

    ![Narzędzia administracyjne zainstalowane na serwerze](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Kliknij przycisk **Centrum administracyjne usługi Active Directory**.

    ![Centrum administracyjne usługi Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooexplore hello domeny, kliknij nazwę domeny hello w okienku po lewej stronie powitania (na przykład "contoso100.com"). Zwróć uwagę dwa kontenery odpowiednio o nazwie "AADDC komputery" i "AADDC użytkowników".

    ![ADAC — widok domeny](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. Kliknij hello kontener o nazwie **użytkowników AADDC** toosee wszystkich użytkowników i grup należących toohello zarządzane domeny. Powinny pojawić się konta użytkowników i grup z usługi Azure AD dzierżawy Pokaż się w tym kontenerze. W tym przykładzie, konto użytkownika dla użytkownika hello o nazwie "bob" i grupę o nazwie "Administratorzy kontrolera domeny usługi AAD" są dostępne w tym kontenerze.

    ![ADAC - użytkownicy domeny](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. Kliknij hello kontener o nazwie **komputerów AADDC** toosee hello komputery przyłączone do domeny zarządzanej toothis. Powinny pojawić się wpis dla bieżącej maszyny wirtualnej hello, czyli toohello przyłączone do domeny. Konta komputerów dla wszystkich komputerów, które są przyłączone toohello domeny zarządzanej są przechowywane w tym kontenerze "Komputery AADDC" usługi domenowe Azure AD.

    ![ADAC — komputery przyłączone do domeny](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Przyłączanie się do systemu Windows Server maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny](active-directory-ds-admin-guide-join-windows-vm.md)
* [Wdrażanie narzędzi administracji zdalnej serwera](https://technet.microsoft.com/library/hh831501.aspx)
