---
title: aaaBackup maszyn wirtualnych systemu Windows Azure | Dokumentacja firmy Microsoft
description: "Ochrona maszyn wirtualnych systemu Windows przez tworzenie ich kopii zapasowych za pomocą usługi Kopia zapasowa Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a>Tworzenie kopii zapasowych maszyn wirtualnych systemu Windows na platformie Azure

Możesz chronić swoje dane, tworząc kopie zapasowe w regularnych odstępach czasu. Kopia zapasowa Azure tworzy punkty odzyskiwania, które są przechowywane w magazynach odzyskiwania z magazynu geograficznie nadmiarowego. Po przywróceniu z punktu odzyskiwania, można przywrócić hello całej maszyny Wirtualnej lub po prostu określonych plików. W tym artykule opisano, jak toorestore pojedynczy plik tooa wirtualna systemem Windows Server i usług IIS. Jeśli nie masz jeszcze toouse maszyny Wirtualnej, możesz utworzyć jedną przy użyciu hello [Szybki Start systemu Windows](quick-create-portal.md). Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Utwórz kopię zapasową maszyny Wirtualnej
> * Harmonogram tworzenia codziennej kopii zapasowej
> * Przywróć plik z kopii zapasowej




## <a name="backup-overview"></a>Omówienie usługi Backup

Gdy hello usługi Kopia zapasowa Azure inicjuje zadania tworzenia kopii zapasowej, wyzwala hello zapasowy numer wewnętrzny tootake migawki punktu w czasie. Witaj usługi Kopia zapasowa Azure korzysta hello _VMSnapshot_ rozszerzenia. rozszerzenie Hello jest instalowany podczas hello pierwszej kopii zapasowej maszyny Wirtualnej, jeśli hello maszyna wirtualna jest uruchomiona. Jeśli hello maszyna wirtualna nie jest uruchomiona, hello usługi Kopia zapasowa tworzy migawkę hello bazowy magazynu (ponieważ nie zapisy aplikacji występuje podczas powitalne zatrzymaniu maszyny Wirtualnej).

Podczas wykonywania migawki maszyn wirtualnych systemu Windows, usługi Kopia zapasowa hello koordynuje z tooget usługi kopiowania woluminów w tle (VSS) hello spójne migawek dysków maszyny wirtualnej hello. Witaj usługi Kopia zapasowa Azure wykonuje migawkę hello, hello danych po toohello przekazanych magazynu. wydajność toomaximize hello usługa identyfikuje i transferuje tylko hello bloki danych, które uległy zmianie od czasu poprzedniej kopii zapasowej hello.

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

## <a name="recover-a-file"></a>Odzyskiwanie pliku

Jeśli przypadkowo usunięte lub zmiany tooa plik, można użyć pliku hello toorecover odzyskiwanie plików z magazynu kopii zapasowej. Odzyskiwanie plików używa skryptu uruchamianego na powitania maszyny Wirtualnej, punkt odzyskiwania hello toomount jako dysk lokalny. Dyski te pozostanie zainstalowanego na 12 godzin, co można kopiować pliki z punktu odzyskiwania hello i przywracać je toohello maszyny Wirtualnej.  

W tym przykładzie zostanie przedstawiony sposób toorecover hello plik obrazu, który jest używany w hello domyślnej strony sieci web dla usług IIS. 

1. Otwórz przeglądarkę i Połącz z adresu IP toohello hello wirtualna tooshow hello domyślnej IIS strony.

    ![Domyślna strona sieci web usług IIS](./media/tutorial-backup-vms/iis-working.png)

2. Połącz toohello maszyny Wirtualnej.
3. Na powitania maszyny Wirtualnej, otwórz **Eksploratora plików** Przejdź too\inetpub\wwwroot i usuń plik hello **iisstart.png**.
4. Na komputerze lokalnym toosee przeglądarki hello odświeżania, który hello obrazu na powitania domyślnej strony usług IIS został usunięty.

    ![Domyślna strona sieci web usług IIS](./media/tutorial-backup-vms/iis-broken.png)

5. Na komputerze lokalnym, otwórz nową kartę i przejdź Witaj Witaj [portalu Azure](https://portal.azure.com).
6. W menu hello powitania po lewej stronie wybierz **maszyn wirtualnych** i wybierz hello wirtualna formularza hello listy.
8. W bloku maszyny Wirtualnej hello w hello **ustawienia** kliknij **kopii zapasowej**. Witaj **kopii zapasowej** zostanie otwarty blok. 
9. Witaj menu u góry bloku hello hello wybierz **odzyskiwanie plików**. Witaj **odzyskiwanie plików** zostanie otwarty blok.
10. W **krok 1: Wybierz punkt odzyskiwania**, wybierz punkt odzyskiwania z listy rozwijanej hello.
11. W **krok 2: Pobieranie skryptu toobrowse i odzyskiwanie plików**, kliknij przycisk hello **Pobierz plik wykonywalny** przycisk. Zapisz hello pliku tooyour **pobiera** folderu.
12. Na komputerze lokalnym, otwórz **Eksploratora plików** i przejdź tooyour **pobiera** hello folderu i skopiuj pobrany plik .exe. Nazwa pliku Hello będzie ona poprzedzona przez nazwę maszyny Wirtualnej. 
13. Na maszynie Wirtualnej (za pośrednictwem połączenia RDP hello) Wklej toohello pliku .exe hello pulpitu maszyny Wirtualnej. 
14. Przejdź do pulpitu toohello maszyny wirtualnej, a następnie kliknij dwukrotnie ikonę na powitania .exe. Zostanie uruchomiony wiersz polecenia i zainstaluj punkt odzyskiwania hello jako udział pliku, który można uzyskać dostęp. Po zakończeniu tworzenia udziału hello, wpisz **q** tooclose hello poleceń.
15. Na maszynie Wirtualnej, należy otworzyć **Eksploratora plików** i przejdź toohello literę dysku, którego użyto do udziału plików hello.
16. Przejdź too\inetpub\wwwroot i skopiuj **iisstart.png** z pliku hello udziału i wklej go do \inetpub\wwwroot. Na przykład F:\inetpub\wwwroot\iisstart.png skopiuj i wklej go do pliku hello toorecover c:\inetpub\wwwroot.
17. Na komputerze lokalnym, otwórz kartę przeglądarki hello której są podłączone adres IP toohello hello wirtualna prezentująca hello IIS domyślnej strony. Naciśnij klawisze CTRL + F5 toorefresh hello przeglądarki strony. Powinien zostać wyświetlony ten hello obrazu została przywrócona.
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









