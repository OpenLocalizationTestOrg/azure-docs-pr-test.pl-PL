---
title: "Azure Active Directory Domain Services: Dołącz RHEL maszynę Wirtualną do domeny zarządzanej | Dokumentacja firmy Microsoft"
description: "Dołącz maszynę wirtualną systemu Red Hat Enterprise Linux do usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a>Przyłączanie maszyny wirtualnej z systemem Red Hat Enterprise Linux 7 do domeny zarządzanej
W tym artykule przedstawiono sposób Dołącz maszynę wirtualną Red Hat Enterprise Linux (RHEL) 7 do domeny zarządzanej usług domenowych Azure AD.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Aprowizowanie maszyny wirtualnej Red Hat Enterprise Linux
Wykonaj poniższe kroki, aby udostępnić maszynie wirtualnej RHEL 7 przy użyciu portalu Azure.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).

    ![Pulpitu nawigacyjnego portalu Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Kliknij przycisk **nowy** w okienku po lewej stronie i typ **Red Hat** na pasku wyszukiwania, jak pokazano na poniższym zrzucie ekranu. Wpisy dla Red Hat Enterprise Linux są wyświetlane w wynikach wyszukiwania. Kliknij przycisk **Red Hat Enterprise Linux 7.2**.

    ![Wybierz RHEL w wynikach](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. W wynikach wyszukiwania **wszystko** okienko powinny zawierać obrazu Red Hat Enterprise Linux 7.2. Kliknij przycisk **Red Hat Enterprise Linux 7.2** Aby uzyskać więcej informacji o obrazie maszyny wirtualnej.

    ![Wybierz RHEL w wynikach](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. W **Red Hat Enterprise Linux 7.2** okienka, należy wyświetlić więcej informacji o obrazie maszyny wirtualnej. W **wybierz model wdrożenia** listy rozwijanej wybierz **klasycznego**. Następnie kliknij przycisk **Utwórz** przycisku.

    ![Wyświetlanie szczegółów obrazu](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. W **podstawy** strony **tworzenia maszyny wirtualnej** kreatora wprowadź **nazwy hosta** dla nowej maszyny wirtualnej. Również określić nazwę użytkownika administratora lokalnego w **nazwy użytkownika** pola i **hasło**. Można również użyć klucza SSH do uwierzytelnienia użytkownika administratora lokalnego. Wybierz również **warstwy cenowej** dla maszyny wirtualnej.

    ![Tworzenie maszyny Wirtualnej — podstawy strony](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. W **rozmiar** strony **tworzenia maszyny wirtualnej** kreatora wybierz rozmiar maszyny wirtualnej.

    ![Tworzenie maszyny Wirtualnej — wybierz rozmiar](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. W **ustawienia** strony **tworzenia maszyny wirtualnej** kreatora, wybierz konto magazynu dla maszyny wirtualnej. Kliknij przycisk **sieci wirtualnej** do wybrania sieci wirtualnej, do którego można wdrożyć maszyny Wirtualnej systemu Linux. W **sieci wirtualnej** bloku, wybierz opcję sieci wirtualnej, w których usługi domenowe Azure AD jest dostępna. W tym przykładzie mamy wybierz "MyPreviewVNet" sieci wirtualnej.

    ![Tworzenie maszyny Wirtualnej — Wybieranie sieci wirtualnej](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. Na **Podsumowanie** strony **tworzenia maszyny wirtualnej** kreatora przejrzyj a kliknij **OK** przycisku.

    ![Tworzenie maszyny Wirtualnej — wybrana sieć wirtualna](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Należy zacząć wdrażania nowej maszyny wirtualnej na podstawie obrazu RHEL 7.2.

    ![Tworzenie maszyny Wirtualnej — rozpoczęto wdrażanie](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Po kilku minutach maszyny wirtualnej powinny zostać wdrożone pomyślnie i gotowe do użycia.

    ![Tworzenie maszyny Wirtualnej — wdrożony](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a>Zdalne nawiązywanie połączenia nowo aprowizowanej maszyny wirtualnej systemu Linux
Maszyna wirtualna RHEL 7.2 zainicjowano na platformie Azure. Następne zadanie jest zdalne nawiązywanie połączenia z maszyną wirtualną.

**Połącz z maszyną wirtualną RHEL 7.2** postępuj zgodnie z instrukcjami w artykule [jak zalogować się do maszyny wirtualnej z systemem Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Pozostałe kroki przyjęto założenie, że używasz klienta PuTTY SSH do nawiązania połączenia z maszyną wirtualną RHEL. Aby uzyskać więcej informacji, zobacz [strony pobierania programu PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Otwórz PuTTY program.
2. Wprowadź **nazwy hosta** dla nowo utworzonego RHEL maszyny wirtualnej. W tym przykładzie naszych maszyna wirtualna ma nazwę hosta "contoso-rhel.cloudapp .net". Jeśli nie masz pewności nazwy hosta maszyny wirtualnej, można znaleźć na pulpicie maszyny Wirtualnej w portalu Azure.

    ![Łączenie programu puTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Zaloguj się do maszyny wirtualnej przy użyciu poświadczeń administratora lokalnego możesz określić podczas tworzenia maszyny wirtualnej. W tym przykładzie użyliśmy konta administratora lokalnego "mahesh".

    ![Logowania programu puTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a>Zainstaluj wymagane pakiety na maszynie wirtualnej systemu Linux
Po nawiązaniu połączenia z maszyną wirtualną, następne zadanie jest zainstalowanie pakietów wymagane do przyłączania do domeny na maszynie wirtualnej. Wykonaj następujące czynności:

1. **Zainstaluj realmd:** pakietu realmd służy do przyłączania do domeny. W terminalu PuTTY wpisz następujące polecenie:

    sudo yum instalacji realmd

    ![Zainstaluj realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Po kilku minutach pakietu realmd powinny zostać zainstalowane na maszynie wirtualnej.

    ![realmd zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Zainstaluj sssd:** pakiet realmd zależy od sssd do wykonania operacji łączenia domeny. W terminalu PuTTY wpisz następujące polecenie:

    sudo yum instalacji sssd

    ![Zainstaluj sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Po kilku minutach pakietu sssd powinny zostać zainstalowane na maszynie wirtualnej.

    ![realmd zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Instalowanie protokołu kerberos:** w terminalu PuTTY, wpisz następujące polecenie:

    sudo yum instalacji stacji roboczej krb5 krb5-biblioteki

    ![Instalowanie protokołu kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Po kilku minutach pakietu realmd powinny zostać zainstalowane na maszynie wirtualnej.

    ![Protokół Kerberos jest zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a>Dołącz maszynę wirtualną systemu Linux do domeny zarządzanej
Teraz, wymagane pakiety są zainstalowane na maszynie wirtualnej systemu Linux, następne zadanie to można dołączyć maszyny wirtualnej do domeny zarządzanej.

1. Wykryj domeny zarządzanej usług domenowych w usłudze AAD. W terminalu PuTTY wpisz następujące polecenie:

    obszar sudo odnajdywanie CONTOSO100.COM

    ![Odnajdowanie obszaru](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Jeśli **odnajdowanie obszaru** nie może znaleźć domeny zarządzanej, upewnij się, że domena jest osiągalna z poziomu maszyny wirtualnej (ping spróbuj). Upewnij się również maszyny wirtualnej w rzeczywistości został wdrożony do tej samej sieci wirtualnej, w których są dostępne domeny zarządzanej.
2. Inicjowanie protokołu kerberos. W terminalu PuTTY wpisz następujące polecenie. Upewnij się, że określ użytkownika, który należy do grupy "Administratorzy kontrolera domeny usługi AAD". Tylko ci użytkownicy mogą dołączania komputerów do domeny zarządzanej.

    kinitbob@CONTOSO100.COM

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Zapewnienia, że należy określić nazwę domeny wielkimi literami, else kinit nie powiedzie się.
3. Dołącz maszynę do domeny. W terminalu PuTTY wpisz następujące polecenie. Określ tego samego użytkownika określonego w poprzednim kroku (kinit).

    sudo obszaru sprzężenia — pełne CONTOSO100.COM -U "bob@CONTOSO100.COM"

    ![Dołącz do obszaru](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

Należy pobrać wiadomości ("pomyślnie zarejestrowane maszyny w obszarze") po maszyna jest pomyślnie dołączona do domeny zarządzanej.

## <a name="verify-domain-join"></a>Sprawdź, przyłączanie do domeny
Można szybko sprawdzić, czy maszyna została pomyślnie dołączona do domeny zarządzanej. Połączyć się z nowo RHEL maszyny Wirtualnej przy użyciu SSH i konto użytkownika domeny, a następnie sprawdź, aby zobaczyć, czy konto użytkownika jest poprawnie rozpoznać przyłączonych do domeny.

1. W terminalu PuTTY, wpisz następujące polecenie, aby połączyć się z nowo RHEL maszyny wirtualnej przy użyciu protokołu SSH przyłączonych do domeny. Użyj konta domeny, który należy do domeny zarządzanej (na przykład "bob@CONTOSO100.COM" w tym przypadku.)

    SSH -l bob@CONTOSO100.COM rhel.cloudapp.net firmy contoso
2. W terminalu PuTTY wpisz następujące polecenie, aby zobaczyć, czy katalog macierzysty został poprawnie zainicjowany.

    pwd
3. W terminalu PuTTY wpisz następujące polecenie, aby zobaczyć, czy członkostwa w grupach są rozpoznawane poprawnie.

    id

Następujące przykładowe dane wyjściowe tych poleceń:

![Sprawdź, przyłączanie do domeny](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Rozwiązywanie problemów z przyłączania do domeny
Zapoznaj się [przyłączenie do domeny Rozwiązywanie problemów](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artykułu.

## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Dołącz maszynę wirtualną systemu Windows Server do domeny zarządzanej usług domenowych Azure AD](active-directory-ds-admin-guide-join-windows-vm.md)
* [Jak zalogować się do maszyny wirtualnej z systemem Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Instalowanie protokołu Kerberos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 — przewodnik integracji systemu Windows](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
