---
title: "Azure Active Directory Domain Services: Administrowanie DNS w domenach zarządzanych | Dokumentacja firmy Microsoft"
description: "Administrowanie systemem DNS w domenach zarządzanych usług domenowych Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>Administrowanie systemem DNS w domenie zarządzanej usług domenowych Azure AD
Azure Active Directory Domain Services zawiera serwer DNS (rozpoznawanie nazw domen), który udostępnia rozpoznawanie nazw DNS dla domeny zarządzanej hello. Czasami może być konieczne tooconfigure DNS w domenie hello zarządzane. Toocreate rekordów DNS może być konieczne dla maszyn, które nie są toohello przyłączone do domeny, skonfigurować wirtualne adresy IP usługi równoważenia obciążenia, lub skonfigurować zewnętrznych usług przesyłania dalej DNS. Z tego powodu użytkownicy, którzy należą do grupy "Administratorzy kontrolera domeny usługi AAD" toohello są przyznawane uprawnienia administracyjne DNS domeny zarządzanej hello.

## <a name="before-you-begin"></a>Przed rozpoczęciem
zadania hello tooperform wymienione w tym artykule, potrzebne są:

1. Prawidłowy **subskrypcji platformy Azure**.
2. **Katalog usługi Azure AD** -albo synchronizowane z katalogu lokalnego lub w katalogu tylko w chmurze.
3. **Usługi domenowe Azure AD** musi być włączona dla katalogu hello Azure AD. Jeśli nie zostało to jeszcze zrobione, należy wykonać wszystkie zadania hello opisane w hello [Przewodnik wprowadzający](active-directory-ds-getting-started.md).
4. A **przyłączonych do domeny maszyny wirtualnej** z którego administrujesz hello domeny zarządzanej usług domenowych Azure AD. Jeśli nie masz maszynę wirtualną, należy wykonać wszystkie zadania hello opisane w artykule hello zatytułowany [Dołącz do domeny zarządzanej tooa maszyny wirtualnej systemu Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Wymagane poświadczenia hello **użytkownika konto należące toohello "AAD kontrolera domeny" Administratorzy** w katalogu tooadminister DNS dla domeny zarządzanej.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>Zadanie 1 - Provision tooremotely przyłączonych do domeny maszyny wirtualnej administrowanie DNS dla domeny zarządzanej hello
Azure domen zarządzanych w usługach domenowych AD można zarządzać zdalnie za pomocą znanych narzędzi administracyjnych usługi Active Directory takich jak hello Centrum administracyjne Active Directory (ADAC) lub AD PowerShell. Podobnie systemu DNS dla domeny zarządzanej hello można administrować zdalnie przy użyciu narzędzi administracyjnych powitania serwera DNS.

Administratorzy w katalogu usługi Azure AD nie mają uprawnień tooconnect toodomain kontrolerów na powitania domeny zarządzanej za pośrednictwem pulpitu zdalnego. Członkowie grupy "Administratorzy kontrolera domeny usługi AAD" hello mogą administrować DNS dla domen zarządzanych zdalnie przy użyciu narzędzia serwera DNS z komputera klienta serwera systemu Windows, który jest toohello przyłączone do domeny zarządzanej. Narzędzia serwera DNS można zainstalować jako część narzędzi administracji zdalnej serwera (RSAT) hello opcjonalna funkcja w systemie Windows Server i komputerów klienckich przyłączone do domeny toohello zarządzane.

pierwszym zadaniem Hello jest tooprovision maszyny wirtualnej systemu Windows Server, która jest toohello przyłączone do domeny zarządzanej. Instrukcje można znaleźć w artykule toohello zatytułowany [przyłączyć się do systemu Windows Server maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>Zadanie 2 — narzędzia do instalacji serwera DNS na maszynie wirtualnej hello
Wykonaj hello następujące narzędzia do administrowania DNS hello tooinstall kroki na maszynie wirtualnej hello przyłączony do domeny. Aby uzyskać więcej informacji na temat [instalowaniu i używaniu narzędzi administracji zdalnej serwera](https://technet.microsoft.com/library/hh831501.aspx), zobacz temat Technet.

1. Przejdź za**maszyn wirtualnych** węzła w hello klasycznego portalu Azure. Wybierz maszynę wirtualną hello utworzony w zadaniu 1, a następnie kliknij przycisk **Connect** na pasku poleceń hello u dołu okna hello hello.

    ![Połącz tooWindows maszyny wirtualnej](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. klasyczny portal Hello monit tooopen lub Zapisz plik z rozszerzeniem "RDP", który jest maszyną wirtualną toohello tooconnect używane. Kliknij plik powitania po zakończeniu pobierania.
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
9. Na powitania **funkcje** kliknij przycisk tooexpand hello **narzędzi administracji zdalnej serwera** węzła a następnie kliknij przycisk tooexpand hello **narzędzia do administrowania rolami** węzła. Wybierz **narzędzia serwera DNS** funkcję z listy hello narzędzia do administrowania rolami.

    ![Strona funkcji](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. Na powitania **potwierdzenie** kliknij przycisk **zainstalować** narzędzia serwera DNS hello tooinstall funkcji na powitania maszyny wirtualnej. Po pomyślnym zakończeniu instalacji funkcji, kliknij przycisk **Zamknij** tooexit hello **Dodaj role i funkcje** kreatora.

    ![Strona potwierdzenia](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>Zadanie 3 — uruchamianie hello DNS zarządzania konsoli tooadminister DNS
Teraz, czy narzędzia serwera DNS hello funkcje są zainstalowane na hello maszyny wirtualnej przyłączony do domeny, możemy użyć hello DNS narzędzia tooadminister DNS w domenie hello zarządzane.

> [!NOTE]
> Należy toobe członek grupy hello "Administratorzy kontrolera domeny usługi AAD" tooadminister DNS na powitania domeny zarządzanej.
>
>

1. Na ekranie startowym powitania kliknij **narzędzia administracyjne**. Powinny pojawić się hello **DNS** zainstalowana na maszynie wirtualnej hello konsoli.

    ![Narzędzia administracyjne — konsoli DNS](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. Kliknij przycisk **DNS** konsoli zarządzania DNS hello toolaunch.
3. W hello **połączyć tooDNS serwera** okna dialogowego, kliknij opcję hello zatytułowany **hello następujących komputera**i wpisz nazwę domeny DNS hello domeny zarządzanej hello (na przykład "contoso100.com").

    ![Konsolę DNS - Połącz toodomain](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. Witaj konsoli DNS łączy toohello domeny zarządzanej.

    ![Konsolę DNS - administrowania domeny](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. Można teraz używać wpisy DNS tooadd konsoli DNS powitania dla komputerów w sieci wirtualnej hello, w której włączono usługi domenowe w usłudze AAD.

> [!WARNING]
> Administrowanie systemem DNS dla hello zarządzane przy użyciu narzędzi administracyjnych DNS domeny, należy zachować ostrożność. Upewnij się, że **nie należy usuwać ani modyfikować hello wbudowanych rekordy DNS, które są używane przez usługi domenowe w domenie hello**. Wbudowane rekordy DNS obejmują rekordów DNS domeny, rekordy serwera nazw i inne rekordy lokalizacji kontrolera domeny. Modyfikując te rekordy, usług domenowych w usłudze są zakłócone na powitania sieci wirtualnej.
>
>

Zobacz hello [narzędzia DNS artykuł w witrynie Technet](https://technet.microsoft.com/library/cc753579.aspx) Aby uzyskać więcej informacji o zarządzaniu usługą DNS.

## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Przyłączanie się do systemu Windows Server maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administrowanie domeną zarządzaną usług Azure AD Domain Services](active-directory-ds-admin-guide-administer-domain.md)
* [Narzędzia administracji systemu DNS](https://technet.microsoft.com/library/cc753579.aspx)
