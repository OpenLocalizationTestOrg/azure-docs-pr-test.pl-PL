---
title: "Azure Active Directory Domain Services: Administrowanie zasad grupy w domenach zarządzanych | Dokumentacja firmy Microsoft"
description: "Domeny zarządzane przez zasady grupy Administruj w usługach domenowych Azure Active Directory"
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
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>Administrowanie zasad grupy w domenie zarządzanej usług domenowych Azure AD
Azure Active Directory Domain Services zawiera wbudowane obiekty zasad grupy (GPO) dla kontenerów "Użytkownicy AADDC" i "AADDC komputery" hello. Można dostosować te wbudowane tooconfigure obiektów zasad grupy zasady grupy na powitania domeny zarządzanej. Ponadto członkowie grupy "Administratorzy kontrolera domeny usługi AAD" hello mogą tworzyć własne niestandardowe jednostek organizacyjnych w domenie zarządzanej hello. Można też tworzyć niestandardowe obiekty zasad grupy i połączyć je niestandardowe toothese jednostek organizacyjnych. Użytkownicy, którzy należą do grupy "Administratorzy kontrolera domeny usługi AAD" toohello udzielono uprawnień administracyjnych zasad grupy do domeny zarządzanej hello.

## <a name="before-you-begin"></a>Przed rozpoczęciem
zadania hello tooperform wymienione w tym artykule, potrzebne są:

1. Prawidłowy **subskrypcji platformy Azure**.
2. **Katalog usługi Azure AD** -albo synchronizowane z katalogu lokalnego lub w katalogu tylko w chmurze.
3. **Usługi domenowe Azure AD** musi być włączona dla katalogu hello Azure AD. Jeśli nie zostało to jeszcze zrobione, należy wykonać wszystkie zadania hello opisane w hello [Przewodnik wprowadzający](active-directory-ds-getting-started.md).
4. A **przyłączonych do domeny maszyny wirtualnej** z którego administrujesz hello domeny zarządzanej usług domenowych Azure AD. Jeśli nie masz maszynę wirtualną, należy wykonać wszystkie zadania hello opisane w artykule hello zatytułowany [Dołącz do domeny zarządzanej tooa maszyny wirtualnej systemu Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Wymagane poświadczenia hello **użytkownika konto należące toohello "AAD kontrolera domeny" Administratorzy** w katalogu tooadminister zasad grupy dla domeny zarządzanej.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>Zadanie 1 - Provision tooremotely przyłączonych do domeny maszyny wirtualnej administrowanie zasad grupy dla domeny zarządzanej hello
Azure domen zarządzanych w usługach domenowych AD można zarządzać zdalnie za pomocą znanych narzędzi administracyjnych usługi Active Directory takich jak hello Centrum administracyjne Active Directory (ADAC) lub AD PowerShell. Podobnie zasady grupy dla domeny zarządzanej hello można administrować zdalnie przy użyciu narzędzi administracyjnych zasad grupy hello.

Administratorzy w katalogu usługi Azure AD nie mają uprawnień tooconnect toodomain kontrolerów na powitania domeny zarządzanej za pośrednictwem pulpitu zdalnego. Członkowie grupy "Administratorzy kontrolera domeny usługi AAD" hello można zasad grupy dla domen zarządzanych zdalnie administrować. Ich za pomocą narzędzi zasad grupy w domenie zarządzanej toohello przyłączone do komputera klienta serwera systemu Windows. Narzędzia zasad grupy można zainstalować jako część hello opcjonalna funkcja zarządzania zasadami grupy na komputerach z systemem Windows Server i klienta przyłączone do domeny zarządzanej toohello.

pierwszym zadaniem Hello jest tooprovision maszyny wirtualnej systemu Windows Server, która jest toohello przyłączone do domeny zarządzanej. Instrukcje można znaleźć w artykule toohello zatytułowany [przyłączyć się do systemu Windows Server maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>Zadanie 2 — narzędzia zasad grupy do instalacji na maszynie wirtualnej hello
Wykonaj hello następujących narzędzi administracyjnych zasad grupy hello tooinstall kroki na maszynie wirtualnej hello przyłączony do domeny.

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
9. Na powitania **funkcje** strona, wybierz hello **Zarządzanie zasadami grupy** funkcji.

    ![Strona funkcji](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. Na powitania **potwierdzenie** kliknij przycisk **zainstalować** funkcję Zarządzanie zasadami grupy hello tooinstall hello maszyny wirtualnej. Po pomyślnym zakończeniu instalacji funkcji, kliknij przycisk **Zamknij** tooexit hello **Dodaj role i funkcje** kreatora.

    ![Strona potwierdzenia](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>Zadanie 3 — uruchamianie hello zasad grupy zarządzania konsoli tooadminister zasad grupy
Można użyć konsoli zarządzania zasadami grupy hello na powitania przyłączonych do domeny maszyny wirtualnej tooadminister zasad grupy w domenie zarządzanej hello.

> [!NOTE]
> Należy toobe członek grupy hello "Administratorzy kontrolera domeny usługi AAD" tooadminister zasad grupy na powitania domeny zarządzanej.
>
>

1. Na ekranie startowym powitania kliknij **narzędzia administracyjne**. Powinny pojawić się hello **Zarządzanie zasadami grupy** zainstalowana na maszynie wirtualnej hello konsoli.

    ![Zarządzanie zasadami grupy uruchamiania](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. Kliknij przycisk **Zarządzanie zasadami grupy** konsoli zarządzania zasadami grupy hello toolaunch.

    ![Konsola zasad grupy](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>Zadanie 4 — Dostosowywanie wbudowanej obiektów zasad grupy
Istnieją dwa wbudowane obiekty zasad grupy (GPO) — jeden dla kontenerów "AADDC komputery" i "Użytkownicy AADDC" hello w domeny zarządzanej. Można dostosować zasady grupy tooconfigure tych obiektów zasad grupy na powitania domeny zarządzanej.

1. W hello **Zarządzanie zasadami grupy** konsoli, kliknij przycisk tooexpand hello **lasu: contoso100.com** i **domen** zasad grupy hello toosee węzły do domeny zarządzanej.

    ![Wbudowane obiekty zasad grupy](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. Można dostosować te zasady grupy wbudowane tooconfigure obiektów zasad grupy w domenie zarządzanej. Kliknij prawym przyciskiem myszy hello obiektu zasad grupy, a następnie kliknij przycisk **edycji...**  toocustomize hello wbudowanego obiektu zasad grupy. Narzędzie edytora konfiguracji zasad grupy Hello umożliwia możesz toocustomize hello obiektu zasad grupy.

    ![Edytowanie obiektu zasad grupy wbudowane](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. Teraz możesz używać hello **Edytor zarządzania zasadami grupy** konsoli tooedit hello wbudowanego obiektu zasad grupy. Na przykład powitania po zrzut ekranu pokazuje, jak toocustomize hello wbudowanego obiektu zasad grupy "Komputery AADDC".

    ![Dostosowywanie obiektów zasad grupy](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>Zadanie 5 — Tworzenie niestandardowego obiektu zasad grupy (GPO)
Można utworzyć lub zaimportować własne obiektów zasad grupy niestandardowe. Możesz również połączyć niestandardowe niestandardowe tooa obiektów zasad grupy zostały utworzone w domenie zarządzanej jednostki Organizacyjnej. Aby uzyskać więcej informacji na temat tworzenia niestandardowych jednostkach organizacyjnych, zobacz [Tworzenie niestandardowej jednostki Organizacyjnej w domenie zarządzanej](active-directory-ds-admin-guide-create-ou.md).

> [!NOTE]
> Należy toobe członek grupy hello "Administratorzy kontrolera domeny usługi AAD" tooadminister zasad grupy na powitania domeny zarządzanej.
>
>

1. W hello **Zarządzanie zasadami grupy** konsoli, kliknij przycisk tooselect niestandardowej jednostki organizacyjnej (OU). Kliknij prawym przyciskiem myszy hello jednostkę Organizacyjną, a następnie kliknij przycisk **Utwórz obiekt GPO w tej domenie i umieść tu łącze...** .

    ![Utworzenie niestandardowego obiektu zasad grupy](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. Określ nazwę hello nowy obiekt zasad grupy, a następnie kliknij przycisk **OK**.

    ![Określ nazwę dla obiektu zasad grupy](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. Nowy obiekt zasad grupy jest tworzony i połączone niestandardowe tooyour jednostki Organizacyjnej. Kliknij prawym przyciskiem myszy hello obiektu zasad grupy, a następnie kliknij przycisk **edycji...**  hello menu.

    ![Nowo utworzony obiekt zasad grupy](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. Można dostosować hello nowo utworzony obiekt zasad grupy przy użyciu hello **Edytor zarządzania zasadami grupy**.

    ![Dostosuj nowy obiekt zasad grupy](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


Więcej informacji o używaniu [konsoli zarządzania zasadami grupy](https://technet.microsoft.com/library/cc753298.aspx) jest dostępna w witrynie Technet.

## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Przyłączanie się do systemu Windows Server maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administrowanie domeną zarządzaną usług Azure AD Domain Services](active-directory-ds-admin-guide-administer-domain.md)
* [Konsola zarządzania zasadami grupy](https://technet.microsoft.com/library/cc753298.aspx)
