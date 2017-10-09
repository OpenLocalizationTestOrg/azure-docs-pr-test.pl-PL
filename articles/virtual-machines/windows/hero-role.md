---
title: aaaInstall IIS na pierwszej maszyny Wirtualnej systemu Windows | Dokumentacja firmy Microsoft
description: "Poeksperymentuj z pierwszej maszyny wirtualnej systemu Windows przez zainstalowanie usług IIS i otwieranie za pomocą portu 80 hello portalu Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>Poeksperymentuj z instalacją roli na maszynie Wirtualnej systemu Windows
Po utworzeniu pierwszą maszynę wirtualną (VM) w górę i działa, możesz przejść na tooinstalling oprogramowania i usług. W tym samouczku zamierzamy toouse Menedżera serwera na powitania tooinstall maszyny Wirtualnej serwera systemu Windows usług IIS. Następnie utworzymy grupy zabezpieczeń sieci (NSG) przy użyciu hello Azure tooopen portalu port 80 tooIIS ruchu. 

Jeśli nie utworzono już pierwszej maszyny Wirtualnej, należy przejść wstecz zbyt[tworzenie pierwszej maszyny wirtualnej systemu Windows w portalu Azure hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) przed kontynuowaniem w tym samouczku.

## <a name="make-sure-hello-vm-is-running"></a>Upewnij się, że maszyna wirtualna działa, powitalne
1. Otwórz hello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **maszyn wirtualnych**. Wybierz maszynę wirtualną hello z listy hello.
3. Jeśli stan hello jest **zatrzymane (Deallocated)**, kliknij hello **Start** przycisk na powitania **Essentials** bloku hello maszyny Wirtualnej. Jeśli jest w stanie hello **systemem**, można przenieść na toohello następnego kroku.

## <a name="connect-toohello-virtual-machine-and-sign-in"></a>Podłącz maszynę wirtualną toohello i zaloguj się
1. W menu Centrum powitania kliknij **maszyn wirtualnych**. Wybierz maszynę wirtualną hello z listy hello.
2. W bloku hello hello maszyny wirtualnej, kliknij **Connect**. To powoduje utworzenie i pobranie pliku Remote Desktop Protocol (plik RDP) przypomina maszynę tooyour tooconnect skrótów. Możesz toosave hello pliku tooyour pulpitu łatwy dostęp. **Otwórz** tooyour tooconnect ten plik maszyny Wirtualnej.
   
    ![Zrzut ekranu przedstawiający portal Azure hello jak tooyour tooconnect maszyny Wirtualnej](./media/hero-role/connect.png)
3. Zostanie wyświetlone ostrzeżenie, że hello plik RDP pochodzi od nieznanego wydawcy. Jest to normalne. W oknie pulpitu zdalnego powitania kliknij **Connect** toocontinue.
   
    ![Zrzut ekranu przedstawiający ostrzeżenie o nieznanym wydawcy](./media/hero-role/rdp-warn.png)
4. W oknie zabezpieczenia systemu Windows hello Nazwa typu hello użytkownika i hasło dla konta lokalne powitania utworzonego podczas tworzenia hello maszyny Wirtualnej. Nazwa użytkownika Hello jest wprowadzana jako *vmname*&#92; *Nazwa użytkownika*, następnie kliknij przycisk **OK**.
   
    ![Zrzut ekranu przedstawiający wprowadzanie nazwy maszyny Wirtualnej hello, nazwę użytkownika i hasło](./media/hero-role/credentials.png)
5. Zostanie wyświetlone ostrzeżenie nie można zweryfikować certyfikatu hello. Jest to normalne. Kliknij przycisk **tak** tooverify hello tożsamości hello maszyny wirtualnej i zakończyć logowanie.
   
   ![Zrzut ekranu przedstawiający komunikat dotyczący, potwierdzenia tożsamości hello hello maszyny Wirtualnej](./media/hero-role/cert-warning.png)

Jeśli zostanie uruchomione w tootrouble podczas próby tooconnect, zobacz [tooa połączeń pulpitu zdalnego Rozwiązywanie problemów z maszyny wirtualnej z systemem Windows Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="install-iis-on-your-vm"></a>Instalowanie usług IIS na maszynie wirtualnej
Teraz, gdy użytkownik jest zalogowany toohello maszyny Wirtualnej, dzięki czemu możesz eksperymentować zostanie zainstalowany roli serwera.

1. Otwórz **Menedżera serwera**, jeśli nie jest otwarty. Kliknij przycisk hello **Start** menu, a następnie kliknij przycisk **Menedżera serwera**.
2. W **Menedżera serwera**, wybierz pozycję **lokalnego serwera** w okienku po lewej stronie powitania. 
3. Wybierz hello menu **Zarządzaj** > **Dodaj role i funkcje**.
4. W hello Dodaj role i funkcje kreatora na powitania **typu instalacji** wybierz pozycję **Instalacja roli lub funkcji**, a następnie kliknij przycisk **dalej**.
   
    ![Zrzut ekranu przedstawiający hello Kreatora dodawania ról i funkcji kartę typu instalacji](./media/hero-role/role-wizard.png)
5. Wybierz z puli serwerów hello hello maszyny Wirtualnej, a następnie kliknij przycisk **dalej**.
6. Na powitania **ról serwera** wybierz pozycję **serwer sieci Web (IIS)**.
   
    ![Zrzut ekranu przedstawiający hello Kreatora dodawania ról i funkcji kartę dla ról serwera](./media/hero-role/add-iis.png)
7. Upewnij się, że w hello wyskakującego o dodawaniu funkcje wymagane dla usług IIS, **dołączyć narzędzia do zarządzania** jest zaznaczone, a następnie kliknij przycisk **Dodaj funkcje**. Po zamknięciu hello wyskakującego, kliknij przycisk **dalej** hello kreatora.
   
    ![Zrzut ekranu przedstawiający wyskakujących tooconfirm Dodawanie roli IIS hello](./media/hero-role/confirm-add-feature.png)
8. Na stronie funkcji powitania kliknij **dalej**.
9. Na powitania **roli Serwer sieci Web (IIS)** kliknij przycisk **dalej**. 
10. Na powitania **usług ról** kliknij przycisk **dalej**. 
11. Na powitania **potwierdzenie** kliknij przycisk **zainstalować**. 
12. Po zakończeniu instalacji powitania kliknij **Zamknij** na powitania Kreatora.

## <a name="open-port-80"></a>Otwieranie portu 80
Aby tooaccept Twojego wirtualna ruchu przychodzącego ruchu za pośrednictwem portu 80, należy tooadd reguły dla ruchu przychodzącego toohello sieciowej grupy zabezpieczeń. 

1. Otwórz hello [portalu Azure](https://portal.azure.com).
2. W **maszyn wirtualnych** wybierz hello maszyny Wirtualnej, który został utworzony.
3. W ustawieniach maszyny wirtualnej hello, wybierz **interfejsy sieciowe** , a następnie wybierz hello istniejącego interfejsu sieciowego.
   
    ![Zrzut ekranu przedstawiający hello maszyny wirtualnej ustawienie hello interfejsy sieciowe](./media/hero-role/network-interface.png)
4. W **Essentials** hello interfejsu sieciowego, kliknij przycisk hello **sieciowej grupy zabezpieczeń**.
   
    ![Zrzut ekranu przedstawiający sekcji podstawowe elementy hello hello interfejsu sieciowego](./media/hero-role/select-nsg.png)
5. W hello **Essentials** bloku hello NSG, powinien mieć jeden domyślny istniejącej reguły dla ruchu przychodzącego **domyślny — Zezwalaj rdp** co pozwala toolog w toohello maszyny Wirtualnej. Należy dodać innego ruchu IIS tooallow reguły dla ruchu przychodzącego. Kliknij pozycję **Inbound security rule** (Reguła zabezpieczeń ruchu przychodzącego).
   
    ![Zrzut ekranu przedstawiający sekcji Essentials hello hello NSG](./media/hero-role/inbound.png)
6. W obszarze **Inbound security rules** (Reguły zabezpieczeń ruchu przychodzącego) kliknij przycisk **Dodaj**.
   
    ![Zrzut ekranu przedstawiający tooadd przycisk hello regułę zabezpieczeń](./media/hero-role/add-rule.png)
7. W obszarze **Inbound security rules** (Reguły zabezpieczeń ruchu przychodzącego) kliknij przycisk **Dodaj**. Typ **80** w hello zakres portów i upewnij się, że **Zezwalaj** jest zaznaczone. Gdy skończysz, kliknij przycisk **OK**.
   
    ![Zrzut ekranu przedstawiający tooadd przycisk hello regułę zabezpieczeń](./media/hero-role/port-80.png)

Aby uzyskać więcej informacji na temat grup NSG, reguły ruchu przychodzącego i wychodzącego, zobacz [Zezwalaj dostępu zewnętrznego tooyour maszynę Wirtualną przy użyciu hello portalu Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="connect-toohello-default-iis-website"></a>Połącz toohello domyślna usług IIS witryna sieci Web
1. W portalu Azure hello, kliknij przycisk **maszyn wirtualnych** , a następnie wybierz maszyny Wirtualnej.
2. W hello **Essentials** bloku, kopia programu **publicznego adresu IP**.
   
    ![Zrzut ekranu pokazujący, gdzie toofind hello publicznego adresu IP maszyny Wirtualnej](./media/hero-role/ipaddress.png)
3. Otwórz przeglądarkę i na pasku adresu hello, wpisz w publiczny adres IP, w następujący sposób: http://<publicIPaddress> i kliknij przycisk **Enter** toogo toothat adresu.
4. Przeglądarka należy otwierać hello domyślnej strony sieci web usług IIS. Wygląda mniej więcej tak:
   
    ![Zrzut ekranu przedstawiający stronę IIS domyślne jakie hello wygląda w przeglądarce](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>Następne kroki
* Poeksperymentuj z [dołączenie dysku danych](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour maszyny wirtualnej. Dyski danych zapewniają więcej pamięci masowej dla maszyny wirtualnej.

