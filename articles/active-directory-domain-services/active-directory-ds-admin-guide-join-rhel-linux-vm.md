---
title: "Azure Active Directory Domain Services: Przyłącz do domeny zarządzanej tooa wirtualna RHEL | Dokumentacja firmy Microsoft"
description: "Dołącz maszynę wirtualną systemu Red Hat Enterprise Linux usług domenowych w usłudze tooAzure AD"
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
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a>Dołącz do domeny zarządzanej tooa Red Hat Enterprise Linux 7 maszyny wirtualnej
W tym artykule opisano sposób toojoin Red Hat Enterprise Linux (RHEL) 7 tooan maszyny wirtualnej usługi domenowe Azure AD zarządzania domeny.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Aprowizowanie maszyny wirtualnej Red Hat Enterprise Linux
Wykonaj hello następującej maszyny wirtualnej tooprovision systemów RHEL 7 czynności przy użyciu hello portalu Azure.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

    ![Pulpitu nawigacyjnego portalu Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Kliknij przycisk **nowy** na powitania lewe okienko i typ **Red Hat** na pasku wyszukiwania hello pokazane na powitania po zrzut ekranu. Wpisy dla Red Hat Enterprise Linux są wyświetlane w wynikach wyszukiwania hello. Kliknij przycisk **Red Hat Enterprise Linux 7.2**.

    ![Wybierz RHEL w wynikach](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. wyniki wyszukiwania Hello w hello **wszystko** okienko powinny zawierać obraz powitania Red Hat Enterprise Linux 7.2. Kliknij przycisk **Red Hat Enterprise Linux 7.2** tooview więcej informacji na temat hello obraz maszyny wirtualnej.

    ![Wybierz RHEL w wynikach](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. W hello **Red Hat Enterprise Linux 7.2** okienku powinien zostać wyświetlony więcej informacji na temat hello obraz maszyny wirtualnej. W hello **wybierz model wdrożenia** listy rozwijanej wybierz **klasycznego**. Następnie kliknij przycisk hello **Utwórz** przycisku.

    ![Wyświetlanie szczegółów obrazu](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. W hello **podstawy** strony hello **tworzenia maszyny wirtualnej** kreatora wprowadź hello **nazwy hosta** hello nowej maszyny wirtualnej. Również określić nazwę użytkownika administratora lokalnego w hello **nazwy użytkownika** pola i **hasło**. Można również wybrać toouse użytkownik lokalny administrator hello tooauthenticate klucza SSH. Wybierz również **warstwy cenowej** hello maszyny wirtualnej.

    ![Tworzenie maszyny Wirtualnej — podstawy strony](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. W hello **rozmiar** strony hello **tworzenia maszyny wirtualnej** hello kreatora, wybierz rozmiar maszyny wirtualnej hello.

    ![Tworzenie maszyny Wirtualnej — wybierz rozmiar](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. W hello **ustawienia** strony hello **tworzenia maszyny wirtualnej** hello kreatora, wybierz konto magazynu dla maszyny wirtualnej hello. Kliknij przycisk **sieci wirtualnej** tooselect hello sieci wirtualnej toowhich hello maszyny Wirtualnej systemu Linux powinny zostać wdrożone. W hello **sieci wirtualnej** bloku, wybierz hello sieci wirtualnej, w których są dostępne usługi domenowe Azure AD. W tym przykładzie mamy wybierz sieć wirtualną "MyPreviewVNet" hello.

    ![Tworzenie maszyny Wirtualnej — Wybieranie sieci wirtualnej](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. Na powitania **Podsumowanie** strony hello **tworzenia maszyny wirtualnej** hello kreatora przejrzyj a kliknij **OK** przycisku.

    ![Tworzenie maszyny Wirtualnej — wybrana sieć wirtualna](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Należy zacząć wdrożenia hello nowej maszyny wirtualnej na podstawie obrazu hello RHEL 7.2.

    ![Tworzenie maszyny Wirtualnej — rozpoczęto wdrażanie](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Po kilku minutach hello maszyny wirtualnej należy pomyślnie wdrożone i gotowa do użycia.

    ![Tworzenie maszyny Wirtualnej — wdrożony](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a>Nawiązanie połączenia zdalnego maszyny wirtualnej systemu Linux toohello nowo udostępnione
maszyny wirtualnej Hello RHEL 7.2 zainicjowano na platformie Azure. następne zadanie Hello jest tooconnect zdalnie toohello maszyny wirtualnej.

**Podłącz maszynę wirtualną toohello RHEL 7.2** hello instrukcjami w artykule hello [jak toolog na tooa maszyny wirtualnej z systemem Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Witaj pozostałe kroki hello przyjęto założenie, że używasz hello PuTTY SSH klienta tooconnect toohello RHEL maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz hello [strony pobierania programu PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Otwórz hello PuTTY program.
2. Wprowadź hello **nazwy hosta** dla hello nowo utworzony RHEL maszyny wirtualnej. W tym przykładzie naszych maszyna wirtualna ma hello nazwy hosta "contoso-rhel.cloudapp .net". Jeśli nie masz pewności hello nazwy hosta maszyny Wirtualnej, można znaleźć pulpitu nawigacyjnego wirtualna toohello hello portalu Azure.

    ![Łączenie programu puTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Zaloguj się na maszynie wirtualnej toohello przy użyciu poświadczeń administratora lokalnego hello określone podczas tworzenia maszyny wirtualnej hello. W tym przykładzie użyliśmy konta administratora lokalnego hello "mahesh".

    ![Logowania programu puTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a>Zainstaluj wymagane pakiety na maszynie wirtualnej systemu Linux hello
Po łączącego toohello maszyny wirtualnej hello następne zadanie jest wymagane do przyłączania do domeny na maszynie wirtualnej hello pakiety tooinstall. Wykonaj następujące kroki hello:

1. **Zainstaluj realmd:** pakietu realmd hello jest używany do przyłączania do domeny. W terminalu PuTTY wpisz hello następujące polecenie:

    sudo yum instalacji realmd

    ![Zainstaluj realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Po kilku minutach hello realmd pakietu powinny zostać zainstalowane na maszynie wirtualnej hello.

    ![realmd zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Zainstaluj sssd:** hello realmd pakiet jest zależny od operacji łączenia domeny tooperform sssd. W terminalu PuTTY wpisz hello następujące polecenie:

    sudo yum instalacji sssd

    ![Zainstaluj sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Po kilku minutach hello sssd pakietu powinny zostać zainstalowane na maszynie wirtualnej hello.

    ![realmd zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Instalowanie protokołu kerberos:** w terminalu PuTTY wpisz hello następujące polecenie:

    sudo yum instalacji stacji roboczej krb5 krb5-biblioteki

    ![Instalowanie protokołu kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Po kilku minutach hello realmd pakietu powinny zostać zainstalowane na maszynie wirtualnej hello.

    ![Protokół Kerberos jest zainstalowany](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a>Dołącz do domeny zarządzanej toohello maszyny wirtualnej systemu Linux hello
Obecnie pakiety hello wymagane są zainstalowane na maszynie wirtualnej systemu Linux hello, następne zadanie hello jest domeny zarządzanej toohello toojoin hello maszyny wirtualnej.

1. Wykryj domeny zarządzanej usług domenowych w usłudze AAD hello. W terminalu PuTTY wpisz hello następujące polecenie:

    obszar sudo odnajdywanie CONTOSO100.COM

    ![Odnajdowanie obszaru](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Jeśli **odnajdowanie obszaru** jest toofind domeny zarządzanej, upewnij się, ta domena hello jest dostępny z maszyny wirtualnej hello (ping spróbuj). Upewnij się również hello maszyny wirtualnej w rzeczywistości został wdrożony toohello tej samej sieci wirtualnej, w których hello domeny zarządzanej jest dostępna.
2. Inicjowanie protokołu kerberos. W terminalu PuTTY wpisz hello następujące polecenia. Upewnij się, że podajesz użytkownik, który należy toohello "AAD kontrolera domeny" Administratorzy. Tylko ci użytkownicy można przyłączyć do domeny zarządzanej toohello komputerów.

    kinitbob@CONTOSO100.COM

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Upewnij się, że Określ nazwę domeny hello wielkimi literami, else kinit nie powiedzie się.
3. Dołącz hello maszyny toohello domeny. W terminalu PuTTY wpisz hello następujące polecenia. Określ hello tego samego użytkownika określonego w hello poprzedzających krok (kinit).

    sudo obszaru sprzężenia — pełne CONTOSO100.COM -U "bob@CONTOSO100.COM"

    ![Dołącz do obszaru](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

Należy pobrać wiadomości ("pomyślnie zarejestrowane maszyny w obszarze") gdy komputer hello jest toohello pomyślnie przyłączone do domeny zarządzanej.

## <a name="verify-domain-join"></a>Sprawdź, przyłączanie do domeny
Można szybko sprawdzić, czy maszyna hello została toohello pomyślnie przyłączone do domeny zarządzanej. Połącz toohello nowo RHEL maszyny Wirtualnej przy użyciu SSH i konto użytkownika domeny, a następnie toosee wyboru, jeśli konto użytkownika hello jest poprawnie rozpoznać przyłączonych do domeny.

1. W terminalu, PuTTY hello typu następujące polecenia tooconnect toohello nowo przyłączone do domeny RHEL maszyny wirtualnej przy użyciu protokołu SSH. Użycie konta domeny należącego do domeny zarządzanej toohello (na przykład "bob@CONTOSO100.COM" w tym przypadku.)

    SSH -l bob@CONTOSO100.COM rhel.cloudapp.net firmy contoso
2. W terminalu PuTTY wpisz powitania po toosee polecenia w katalogu macierzystego hello został poprawnie zainicjowany.

    pwd
3. W terminalu PuTTY wpisz powitania po toosee polecenia członkostwa w grupach hello są rozpoznawane poprawnie.

    id

Następujące przykładowe dane wyjściowe tych poleceń:

![Sprawdź, przyłączanie do domeny](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Rozwiązywanie problemów z przyłączania do domeny
Zobacz toohello [przyłączenie do domeny Rozwiązywanie problemów](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artykułu.

## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Przyłączanie się do systemu Windows Server maszyny wirtualnej tooan usług domenowych Azure AD zarządzanej domeny](active-directory-ds-admin-guide-join-windows-vm.md)
* [Jak toolog na tooa maszyny wirtualnej z systemem Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Instalowanie protokołu Kerberos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 — przewodnik integracji systemu Windows](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
