---
title: "Wykonaj kopię zapasową maszyn wirtualnych systemu Linux platformy Azure | Dokumentacja firmy Microsoft"
description: "Ochrona maszyn wirtualnych systemu Linux przez tworzenie ich kopii zapasowych za pomocą usługi Kopia zapasowa Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Tworzenie kopii zapasowych maszyn wirtualnych systemu Linux na platformie Azure

Możesz chronić swoje dane, tworząc kopie zapasowe w regularnych odstępach czasu. Kopia zapasowa Azure tworzy punkty odzyskiwania, które są przechowywane w magazynach odzyskiwania z magazynu geograficznie nadmiarowego. Po przywróceniu z punktu odzyskiwania, można przywrócić hello całej maszyny Wirtualnej lub po prostu określonych plików. W tym artykule opisano, jak toorestore pojedynczy plik tooa nginx uruchomionej maszyny Wirtualnej systemu Linux. Jeśli nie masz jeszcze toouse maszyny Wirtualnej, możesz utworzyć jedną przy użyciu hello [szybkiego startu Linux](quick-create-cli.md). Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Utwórz kopię zapasową maszyny Wirtualnej
> * Harmonogram tworzenia codziennej kopii zapasowej
> * Przywróć plik z kopii zapasowej



## <a name="backup-overview"></a>Omówienie usługi Backup

Gdy hello usługi Kopia zapasowa Azure inicjuje kopii zapasowej, wyzwala hello zapasowy numer wewnętrzny tootake migawki punktu w czasie. Witaj usługi Kopia zapasowa Azure korzysta hello _VMSnapshotLinux_ rozszerzenia w systemie Linux. rozszerzenie Hello jest instalowany podczas hello pierwszej kopii zapasowej maszyny Wirtualnej, jeśli hello maszyna wirtualna jest uruchomiona. Jeśli hello maszyna wirtualna nie jest uruchomiona, hello usługi Kopia zapasowa tworzy migawkę hello bazowy magazynu (ponieważ nie zapisy aplikacji występuje podczas powitalne zatrzymaniu maszyny Wirtualnej).

Domyślnie kopia zapasowa Azure przyjmuje kopia zapasowa spójna systemu plików dla maszyny Wirtualnej systemu Linux, ale może być skonfigurowany tootake [przy użyciu platformy skryptów przed i po skrypt kopii zapasowej spójnej aplikacji](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). Witaj usługi Kopia zapasowa Azure wykonuje migawkę hello, hello danych po toohello przekazanych magazynu. wydajność toomaximize hello usługa identyfikuje i transferuje tylko hello bloki danych, które uległy zmianie od czasu poprzedniej kopii zapasowej hello.

Po ukończeniu transferu danych hello hello migawka zostanie usunięta i utworzenia punktu odzyskiwania.


## <a name="create-a-backup"></a>Tworzenie kopii zapasowej
Tworzenie prostego zaplanowanego codziennego tworzenia kopii zapasowej tooa magazynu usług odzyskiwania. 

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. W menu hello powitania po lewej stronie wybierz **maszyn wirtualnych**. 
3. Wybierz tooback maszyny Wirtualnej z listy hello się.
4. W bloku maszyny Wirtualnej hello w hello **ustawienia** kliknij **kopii zapasowej**. Witaj **kopii zapasowej Włącz** zostanie otwarty blok.
5. W **magazyn usług odzyskiwania i**, kliknij przycisk **Utwórz nowy** i podaj nazwę hello hello nowego magazynu. Nowy magazyn jest tworzony w hello sam lokalizacji jako maszyna wirtualna hello i grupy zasobów.
6. Kliknij przycisk **kopii zapasowej zasad**. W tym przykładzie należy zachować hello wartości domyślne, a następnie kliknij przycisk **OK**.
7. Na powitania **kopii zapasowej Włącz** bloku, kliknij przycisk **Włącz kopię zapasową**. Spowoduje to utworzenie kopii zapasowej codziennie na podstawie hello domyślnego harmonogramu.
10. toocreate początkowego punktu odzyskiwania, na powitania **kopii zapasowej** kliknij bloku **wykonaj kopię zapasową teraz**.
11. Na powitania **Utwórz kopię zapasową teraz** bloku, kliknij ikonę kalendarza hello, użyj hello kalendarza kontroli tooselect hello ostatni dzień tego punktu odzyskiwania jest zachowywana, a następnie kliknij przycisk **kopii zapasowej**.
12. W hello **kopii zapasowej** bloku dla maszyny Wirtualnej, zobaczysz hello liczbę punktów odzyskiwania, które są spełnione.

    ![Punkty odzyskiwania](./media/tutorial-backup-vms/backup-complete.png)

Hello pierwszej kopii zapasowej trwa około 20 minut. Po zakończeniu tworzenia kopii zapasowej, należy kontynuować toohello następnej części tego samouczka.

## <a name="restore-a-file"></a>Przywróć plik

Jeśli przypadkowo usunięte lub zmiany tooa plik, można użyć pliku hello toorecover odzyskiwanie plików z magazynu kopii zapasowej. Odzyskiwanie plików używa skryptu uruchamianego na powitania maszyny Wirtualnej, punkt odzyskiwania hello toomount jako dysk lokalny. Dyski te pozostanie zainstalowanego na 12 godzin, co można kopiować pliki z punktu odzyskiwania hello i przywracać je toohello maszyny Wirtualnej.  

W tym przykładzie zostanie przedstawiony sposób toorecover hello /var/www/html/index.nginx-debian.html strony sieci web nginx domyślne. publiczny adres IP Hello naszych maszyny wirtualnej w tym przykładzie jest *13.69.75.209*. Można znaleźć adres IP hello przy użyciu maszyny wirtualnej:

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. Na komputerze lokalnym otwórz przeglądarkę i typ hello publiczny adres IP maszyny Wirtualnej toosee hello domyślne nginx strony sieci web.

    ![Domyślna strona sieci web nginx](./media/tutorial-backup-vms/nginx-working.png)

1. Nawiąż połączenie z maszyną Wirtualną.

    ```bash
    ssh 13.69.75.209
    ```
2. Usuń /var/www/html/index.nginx-debian.html.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. Na komputerze lokalnym, Odśwież przeglądarkę hello przez naciśnięcie klawiszy CTRL + F5 toosee, że domyślna strona nginx został usunięty.

    ![Domyślna strona sieci web nginx](./media/tutorial-backup-vms/nginx-broken.png)
    
1. Na komputerze lokalnym, zaloguj się toohello [portalu Azure](https://portal.azure.com/).
6. W menu hello powitania po lewej stronie wybierz **maszyn wirtualnych**. 
7. Z listy hello wybierz hello maszyny Wirtualnej.
8. W bloku maszyny Wirtualnej hello w hello **ustawienia** kliknij **kopii zapasowej**. Witaj **kopii zapasowej** zostanie otwarty blok. 
9. Witaj menu u góry bloku hello hello wybierz **odzyskiwanie plików**. Witaj **odzyskiwanie plików** zostanie otwarty blok.
10. W **krok 1: Wybierz punkt odzyskiwania**, wybierz punkt odzyskiwania z listy rozwijanej hello.
11. W **krok 2: Pobieranie skryptu toobrowse i odzyskiwanie plików**, kliknij przycisk hello **Pobierz plik wykonywalny** przycisk. Zapisz hello pobrany plik tooyour lokalnego komputera.
7. Kliknij przycisk **pobrać skryptu** pliku skryptu hello toodownload lokalnie.
8. Otwórz Bash wiersz i wpisz powitania po, zastępując *Linux_myVM_05-05-2017.sh* z hello Popraw ścieżkę i nazwę skryptu hello, który został pobrany, *azureuser* z nazwą użytkownika hello hello maszyny Wirtualnej i *13.69.75.209* hello publicznego adresu IP dla maszyny Wirtualnej.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. Na komputerze lokalnym otwórz toohello połączenia SSH maszyny Wirtualnej.

    ```bash
    ssh 13.69.75.209
    ```
    
10. Na maszynie Wirtualnej, należy dodać wykonać pliku skryptu toohello uprawnienia.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. Na maszynie Wirtualnej należy uruchomić punkt odzyskiwania hello hello skryptu toomount jako system plików.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. Witaj ścieżkę punktu instalacji hello Hello danych wyjściowych z hello zapewnia skryptu. dane wyjściowe Hello wygląda podobnie toothis:

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. Na maszynie Wirtualnej, skopiuj hello nginx domyślnej strony sieci web z toowhere zapasowego punktu instalacji hello usunięte hello pliku.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. Na komputerze lokalnym, otwórz kartę przeglądarki hello której są podłączone adres IP toohello hello wirtualna prezentująca hello nginx domyślnej strony. Naciśnij klawisze CTRL + F5 toorefresh hello przeglądarki strony. Tego hello powinna zostać wyświetlona domyślna strona działa ponownie.

    ![Domyślna strona sieci web nginx](./media/tutorial-backup-vms/nginx-working.png)

18. Na komputerze lokalnym, przejdź wstecz karty przeglądarki toohello hello portalu Azure i w **krok 3: odinstaluj dyski powitania po odzyskaniu** kliknij hello **odinstalować dyski** przycisku. Jeśli zapomnisz toodo ten krok, punktu instalacji toohello połączenia hello jest automatycznie Zamknij po 12 godzinach. Po zakończeniu tych 12 godzin wymagane toodownload nowe toocreate skryptu nowego punktu instalacji.


## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Utwórz kopię zapasową maszyny Wirtualnej
> * Harmonogram tworzenia codziennej kopii zapasowej
> * Przywróć plik z kopii zapasowej

Przejdź dalej toolearn samouczka toohello dotyczące monitorowania maszyn wirtualnych.

> [!div class="nextstepaction"]
> [Monitorowanie maszyn wirtualnych](tutorial-monitoring.md)

