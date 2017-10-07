---
title: "Galerie aaaRunbook i moduł usługi Automatyzacja Azure | Dokumentacja firmy Microsoft"
description: "Elementy Runbook i modułów od społeczności firmy Microsoft i hello są dostępne do tooinstall należy i w środowisku usługi Automatyzacja Azure.  W tym artykule opisano, jak można pobrać tych zasobów i toocontribute galerii toohello elementów runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Galeria elementów Runbook i modułów dla usługi Automatyzacja Azure
Zamiast tworzenia własnych elementów runbook i modułów w automatyzacji Azure, można uzyskać dostępu do szerokiej gamy scenariuszy, które zostały już utworzone przez firmę Microsoft i hello społeczność.  Możesz użyć tych scenariuszy bez żadnych modyfikacji lub można ich używać jako punktu wyjścia i edytować je do swoich specyficznych wymagań.

Elementy runbook można uzyskać z hello [galerię elementów Runbook](#runbooks-in-runbook-gallery) i modułów hello [galerii programu PowerShell](#modules-in-powerShell-gallery).  Również może przyczynić się toohello społeczności, udostępniając scenariusze, które można rozwijać.

## <a name="runbooks-in-runbook-gallery"></a>Elementy Runbook w galerii elementu Runbook
Witaj [galerię elementów Runbook](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) od firmy Microsoft i hello społeczności, który można zaimportować do usługi Automatyzacja Azure jest dostępnych wiele elementów runbook. Możesz pobrać elementu runbook z galerii hello, która jest hostowana w hello [Centrum skryptów w witrynie TechNet](https://gallery.technet.microsoft.com/scriptcenter/site/upload), lub bezpośrednio można zaimportować elementy runbook z galerii hello hello klasycznego portalu Azure lub portalu Azure.

Można importować tylko bezpośrednio z galerii Runbook hello przy użyciu klasycznego portalu Azure hello lub portalu Azure. Nie można wykonać tej funkcji za pomocą środowiska Windows PowerShell.

> [!NOTE]
> Należy sprawdzić, czy zawartość hello żadnych elementów runbook, możesz uzyskać z hello galerię elementów Runbook i należy zachować szczególną ostrożność przy instalacji i uruchamiania ich w środowisku produkcyjnym. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport elementu runbook z hello galerię elementów Runbook z hello klasycznego portalu Azure
1. W hello portalu Azure kliknij przycisk, **nowy**, **usługi aplikacji**, **automatyzacji**, **Runbook**, **z galerii**.
2. Wybierz tooview kategorii powiązane elementy runbook i wybierz tooview elementu runbook z jego szczegóły. Po wybraniu hello elementu runbook, który ma kliknij przycisk strzałki w prawo hello.
   
    ![Galeria elementów Runbook](media/automation-runbook-gallery/runbook-gallery.png)
3. Przejrzyj zawartość hello hello runbook i zapisz wszelkie wymagania w opisie hello. Gdy wszystko będzie gotowe, kliknij przycisk strzałki w prawo hello.
4. Wprowadź szczegóły elementu runbook hello, a następnie kliknij przycisk wyboru hello. Nazwa elementu runbook Hello będzie już wypełnione.
5. Witaj element runbook będzie wyświetlany na powitania **elementów Runbook** kartę hello konta automatyzacji.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport elementu runbook z hello galerię elementów Runbook z hello portalu Azure
1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.
2. Polecenie hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.
3. Kliknij przycisk **galerii przeglądania** przycisku.
   
    ![Galeria przycisk Przeglądaj](media/automation-runbook-gallery/browse-gallery-button.png)
4. Znajdź element galerii hello mają i wybierz ją tooview jego szczegóły.
   
    ![Przejrzyj galerię](media/automation-runbook-gallery/browse-gallery.png)
5. Polecenie **widoku Projekt źródłowy** tooview elementu hello hello [Centrum skryptów w witrynie TechNet](http://gallery.technet.microsoft.com/).
6. tooimport element, kliknij go tooview jego szczegóły, a następnie kliknij przycisk hello **importu** przycisku.
   
    ![Przycisk Importuj](media/automation-runbook-gallery/gallery-item-detail.png)
7. Opcjonalnie można zmienić nazwę hello hello elementu runbook, a następnie kliknij przycisk **OK** tooimport hello runbook.
8. Witaj element runbook będzie wyświetlany na powitania **elementów Runbook** kartę hello konta automatyzacji.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>Dodawanie elementu runbook toohello elementu runbook z galerii
Firma Microsoft zachęca tooadd elementów runbook toohello galerię elementów Runbook, w którym prawdopodobnie będą przydatne tooother klientów.  Można dodać elementu runbook przez [przekazać go toohello Centrum skryptów](http://gallery.technet.microsoft.com/site/upload) uwzględnieniu hello konta poniższe informacje.

* Należy określić *systemu Windows Azure* dla hello **kategorii** i *automatyzacji* dla hello **podkategorii** dla toobe runbook hello wyświetlane w Kreatorze hello.  
* przekazywanie Hello musi być jednego pliku .ps1 lub graphrunbook.  Jeśli element runbook hello wymaga żadnych modułów podrzędnych elementów runbook i zasoby, następnie dodaj w opisie hello złożenia hello, a także w sekcji komentarzy hello hello elementu runbook.  Jeśli masz scenariusza wymagające wielu elementów runbook, Przekaż każdego oddzielnie i listy nazw hello hello powiązane elementy runbook w każdym z opisami. Należy upewnić się, że sama tagów, dzięki czemu będą one widoczne w hello hello tej samej kategorii. Użytkownik będzie miał tooknow opis hello tooread czy inne elementy runbook są wymagane hello toowork scenariusza.
* Dodaj tag hello "GraphicalPS", w przypadku publikowania **graficznym elementem runbook** (nie graficzny przepływ pracy). 
* Włóż hello opis przy użyciu programu PowerShell lub przepływ pracy programu PowerShell fragment kodu **Wstawianie kodu sekcji** ikony.
* Witaj hello przekazywania zostanie wyświetlone podsumowanie w hello, dlatego należy podać szczegółowe informacje, które pomogą zidentyfikować hello funkcje elementu hello runbook użytkownika w wynikach galerię elementów Runbook.
* Należy przypisać jedną toothree z hello następujące znaczniki toohello przekazywania.  Hello runbook będzie wyświetlane w Kreatorze hello w kategorii hello, odpowiadających jej tagów.  Wszystkie tagi nie na tej liście zostaną zignorowane przez kreatora hello. Jeśli nie określono żadnych pasujących tagów, hello runbook będą wyświetlane w obszarze hello innych kategorii.
  
  * Tworzenie kopii zapasowych
  * Zarządzanie pojemnością
  * Zmiana kontroli
  * Zgodność
  * Deweloperów i testowania środowisk
  * Odzyskiwanie po awarii
  * Monitorowanie
  * Stosowanie poprawek
  * Inicjowanie obsługi
  * Korygowania
  * Zarządzanie cyklem życia maszyny Wirtualnej
* Automatyzacja aktualizuje galerii hello raz na godzinę, nie będą widzieć Twój wkład natychmiast.

## <a name="modules-in-powershell-gallery"></a>Moduły w galerii programu PowerShell
Moduły programu PowerShell zawierają polecenia cmdlet, których można używać w elementach runbook, a istniejące modułów, które można zainstalować w automatyzacji Azure są dostępne w hello [galerii programu PowerShell](http://www.powershellgallery.com).  Można uruchomić tej galerii z hello portalu Azure i zainstaluj je bezpośrednio do usługi Automatyzacja Azure, lub można je pobrać i zainstalować je ręcznie.  Nie można zainstalować moduły hello bezpośrednio z hello klasycznego portalu Azure, ale można je pobrać je zainstalować, jak w przypadku innych modułów.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport modułu z hello galerię modułów automatyzacji z hello portalu Azure
1. Otwórz hello portalu Azure, Twoje konto usługi Automatyzacja.
2. Polecenie hello **zasoby** kafelka tooopen hello Lista zasobów.
3. Polecenie hello **modułów** kafelka tooopen hello listy modułów.
4. Polecenie hello **galerii przeglądania** przycisk i hello blok galerii przeglądania jest uruchamiana.
   
    ![Galeria modułów](media/automation-runbook-gallery/modules-blade.png) <br>
5. Po uruchomieniu bloku galerii przeglądania hello można wyszukiwać według hello następujące pola:
   
   * Nazwa modułu
   * Tagi
   * Autor
   * Nazwa zasobu polecenia cmdlet/DSC
6. Znajdź moduł interesuje i zaznacz go tooview jego szczegóły.  
   Podczas przechodzenia do określonego modułu można wyświetlić więcej informacji o module hello, w tym toohello wstecz łącze galerii programu PowerShell, wszystkie wymagane zależności i zawiera wszystkie polecenia cmdlet hello i/lub DSC zasobów, które hello modułu.
   
    ![Szczegóły modułu programu PowerShell](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. Moduł hello tooinstall bezpośrednio do usługi Automatyzacja Azure, kliknij przycisk hello **importu** przycisku.
   
    ![Przycisk Importuj moduł](media/automation-runbook-gallery/module-import-button.png)
8. Jeśli klikniesz przycisk Importuj hello, zobaczysz hello nazwę modułu, który zamierzasz tooimport. Jeśli są zainstalowane wszystkie zależności hello, hello **OK** przycisk jest aktywny. Brak zależności, należy najpierw tooimport te przed zaimportowaniem tego modułu.
9. Kliknij przycisk **OK** uruchomi moduł hello tooimport i hello modułu bloku. Automatyzacja Azure importuje konta tooyour modułu, umożliwia wyodrębnianie metadanych dotyczących modułu hello i hello poleceń cmdlet.
   
    ![Importowanie modułu bloku](media/automation-runbook-gallery/module-import-blade.png)
   
    Może to potrwać kilka minut, ponieważ każde działanie musi toobe wyodrębnione.
10. Otrzymasz powiadomienie o hello module jest wdrażany i powiadomienie po zakończeniu.
11. Po zaimportowaniu modułu hello zobaczysz hello działań dostępnych i można jej zasobów w elementy runbook i konfiguracji żądanego stanu.

## <a name="requesting-a-runbook-or-module"></a>Żądanie runbook lub modułu
Możesz wysłać żądania za[User Voice](https://feedback.azure.com/forums/246290-azure-automation/).  Jeśli muszą pomocy zapisywania elementu runbook lub masz pytania dotyczące programu PowerShell, post tooour pytanie [forum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Następne kroki
* tooget pracy z elementami runbook, zobacz [Tworzenie lub importowanie elementu runbook automatyzacji Azure](automation-creating-importing-runbook.md)
* toounderstand hello różnice między środowiska PowerShell i przepływ pracy programu PowerShell z elementami runbook, zobacz [przepływu pracy programu PowerShell Learning](automation-powershell-workflow.md)

