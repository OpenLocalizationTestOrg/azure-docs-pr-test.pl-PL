---
title: "toocreate aaaHow niestandardowego obrazu szablonu usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate szablonu niestandardowego obrazu usługi Azure RemoteApp. Można użyć tego szablonu z kolekcji hybrydowej lub chmury."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a>Jak toocreate szablonu niestandardowego obrazu usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp używa toohost obrazu szablonu systemu Windows Server 2012 R2, wszystkie programy hello mają tooshare z użytkownikami. toocreate niestandardowego obrazu szablonu usługi RemoteApp można rozpoczynać się od istniejącego obrazu lub Utwórz nową. 

> [!TIP]
> Czy wiesz, że można utworzyć obrazu z maszyny Wirtualnej platformy Azure? TRUE wątku który ogranicza hello ilość czasu go przyjmuje tooimport hello obrazu. Zapoznaj się z kroki hello [tutaj](remoteapp-image-on-azurevm.md).
> 
> 

Witaj wymagania dotyczące obrazu hello, które mogą być przekazywane do użycia z usługą Azure RemoteApp są:

* rozmiar obrazu Hello powinna być wielokrotnością liczby MB. Jeśli spróbujesz tooupload obrazu, który nie jest wielokrotnością hello przekazywanie zakończy się niepowodzeniem.
* Witaj, rozmiar obrazu musi być 127 GB lub mniej.
* Musi znajdować się na plik VHD (pliki VHDX [funkcji Hyper-V wirtualnych dysków twardych] nie są obecnie obsługiwane).
* Witaj wirtualnego dysku twardego nie może być maszyny wirtualnej generacji 2.
* Witaj wirtualnego dysku twardego może być stałym rozmiarze lub dynamicznie powiększających się. Dynamicznie powiększających się dysków VHD jest zalecane, ponieważ trwa tooAzure tooupload mniej czasu niż ustalony rozmiar pliku VHD.
* dysk Hello musi zostać zainicjowany przy użyciu stylu partycjonowania hello główny rekord rozruchowy (MBR). Witaj stylu partycji (GPT tabela) partycji GUID nie jest obsługiwane.
* Witaj dysku VHD musi zawierać jednej instalacji systemu Windows Server 2012 R2. Nazwa może zawierać wiele woluminów, ale tylko jeden zawartych w instalacji systemu Windows.
* Witaj zdalnego pulpitu sesji hosta ról i funkcji Środowisko pulpitu hello musi być zainstalowany.
* Witaj roli Broker połączeń usług pulpitu zdalnego musi *nie* można zainstalować.
* Witaj system szyfrowania plików (EFS) musi być wyłączona.
* Witaj obrazu musi być przetworzonej przez program Sysprep przy użyciu parametrów hello **/oobe / generalize/shutdown** (nie należy używać hello **/mode:vm** parametru).
* Przekazywanie dysk VHD z łańcucha migawek nie jest obsługiwane.

**Przed rozpoczęciem**

Potrzebne są następujące hello toodo przed utworzeniem usługi hello:

* [Zarejestruj się](https://azure.microsoft.com/services/remoteapp/) usługi RemoteApp.
* Utwórz konto użytkownika w usłudze Active Directory toouse jako hello konta usługi RemoteApp. Ogranicz uprawnienia hello dla tego konta, tak aby tylko można przyłączyć maszyny toohello domeny. Zobacz [Konfigurowanie usługi Azure Active Directory dla usługi RemoteApp](remoteapp-ad.md) Aby uzyskać więcej informacji.
* Zbieranie informacji o sieci lokalnej: adres IP informacje i szczegóły urządzenia sieci VPN.
* Zainstaluj hello [programu Azure PowerShell](/powershell/azure/overview) modułu.
* Zbierz informacje o hello użytkowników, którzy mają dostęp toogrant do. Może to być informacje o koncie Microsoft lub informacje o koncie pracy usługi Active Directory dla użytkowników.

## <a name="create-a-template-image"></a>Tworzenie obrazu szablonu
Są to hello wysokiego poziomu kroków toocreate nowego obrazu szablonu od początku:

1. Zlokalizuj obraz dysku DVD systemu Windows Server 2012 R2 Update lub ISO.
2. Utwórz plik wirtualnego dysku twardego.
3. Instalowanie systemu Windows Server 2012 R2.
4. Instalowanie roli hosta sesji zdalnego pulpitu (RDSH) hello i hello funkcja Środowisko pulpitu.
5. Zainstaluj dodatkowe funkcje wymagane przez aplikacje.
6. Instalowanie i konfigurowanie aplikacji. aplikacje udostępniania toomake łatwiejsze, Dodaj wszelkie aplikacje lub programy, które mają tooshare toohello **Start** menu Obraz powitania w szczególności w **%systemdrive%\ProgramData\Microsoft\Windows\Start Start\Programy.
7. Wykonywać żadnych dodatkowych konfiguracji systemu Windows wymagane przez aplikacje.
8. Wyłącz hello system szyfrowania plików (EFS).
9. **WYMAGANE:** Przejdź tooWindows aktualizacji i zainstalować wszystkie ważne aktualizacje.
10. Obraz powitania programu SYSPREP.

Witaj szczegółowe procedury tworzenia nowego obrazu są:

1. Zlokalizuj obraz dysku DVD systemu Windows Server 2012 R2 Update lub ISO.
2. Utwórz plik VHD za pomocą przystawki Zarządzanie dyskami.
   
   1. Uruchamianie przystawki Zarządzanie dyskami (diskmgmt.msc).
   2. Utwórz dynamicznie powiększających się wirtualny dysk twardy 40 GB lub więcej rozmiar. (Oszacować hello ilość miejsca dla systemu Windows, aplikacje i dostosowania. Windows Server z hello RDSH roli i funkcji Środowisko pulpitu wymaga około 10 GB miejsca).
      
      1. Kliknij przycisk **akcji > tworzenia wirtualnego dysku twardego**.
      2. Określ lokalizację hello, rozmiar i formatu wirtualnego dysku twardego. Wybierz **dynamicznie powiększających się**, a następnie kliknij przycisk **OK**.
      
      Spowoduje to uruchomienie przez kilka sekund. Po zakończeniu hello tworzenia dysku VHD powinien zostać wyświetlony nowy dysk bez dowolnej litery dysku i jest w stanie "Nie jest zainicjowana" w konsoli Zarządzanie dyskami hello.
      
      * Kliknij prawym przyciskiem myszy hello (nie hello nieprzydzielone miejsce) na dysku, a następnie kliknij przycisk **Inicjowanie dysku**. Wybierz **MBR** (główny rekord rozruchowy) hello styl partycji, a następnie kliknij przycisk **OK**.
      * Utwórz nowy wolumin: kliknij prawym przyciskiem myszy nieprzydzielone miejsce hello, a następnie kliknij przycisk **nowy wolumin prosty**. Można zaakceptować ustawienia domyślne powitania w Kreatorze hello, ale upewnij się, że dysk litery tooavoid potencjalnych problemów po przypisaniu przekazania obrazu szablonu hello.
      * Kliknij prawym przyciskiem myszy dysk hello, a następnie kliknij przycisk **Odłącz dysk VHD**.
3. Instalowanie systemu Windows Server 2012 R2:
   
   1. Tworzenie nowej maszyny wirtualnej. Użyj hello Kreatora nowej maszyny wirtualnej w Menedżerze funkcji Hyper-V lub funkcji Hyper-V dla klienta.
      1. Na stronie Określanie generacji hello wybierz **generacja 1**.
      2. Na stronie Podłączanie wirtualnego dysku twardego hello zaznacz **Użyj istniejącego wirtualnego dysku twardego**i Przeglądaj toohello utworzony w poprzednim kroku hello wirtualnego dysku twardego.
      3. Na stronie opcji instalacji hello zaznacz **zainstalować system operacyjny z rozruchowego dysku CD/DVD-ROM**, a następnie wybierz hello lokalizację nośnika instalacyjnego systemu Windows Server 2012 R2.
      4. Wybierz inne opcje w hello kreatora niezbędne tooinstall systemu Windows i aplikacji. Kreator hello Zakończ.
   2. Po zakończeniu pracy Kreatora hello, Edytuj ustawienia hello hello maszyny wirtualnej i wprowadzić inne zmiany konieczne tooinstall systemu Windows i programów, takich jak hello liczba procesorów wirtualnych, a następnie kliknij przycisk **OK**.
   3. Połącz toohello maszynę wirtualną i zainstaluj system Windows Server 2012 R2.
4. Instalowanie roli hosta sesji zdalnego pulpitu (RDSH) hello i hello funkcja Środowisko pulpitu:
   1. Uruchom Menedżera serwera.
   2. Kliknij przycisk **Dodaj role i funkcje** na ekranie powitalnym hello lub hello **Zarządzaj** menu.
   3. Kliknij przycisk **dalej** na stronie przed rozpoczęciem powitalne.
   4. Wybierz **Instalacja roli lub funkcji**, a następnie kliknij przycisk **dalej**.
   5. Wybierz z listy hello hello komputera lokalnego, a następnie kliknij przycisk **dalej**.
   6. Wybierz **usług pulpitu zdalnego**, a następnie kliknij przycisk **dalej**.
   7. Rozwiń węzeł **infrastruktura i interfejsy użytkownika** i wybierz **środowisko pulpitu**.
   8. Kliknij przycisk **Dodaj funkcje**, a następnie kliknij przycisk **dalej**.
   9. Na stronie powitania usług pulpitu zdalnego kliknij **dalej**.
   10. Kliknij przycisk **hosta sesji usług pulpitu zdalnego**.
   11. Kliknij przycisk **Dodaj funkcje**, a następnie kliknij przycisk **dalej**.
   12. Na stronie Opcje instalacji, potwierdź hello, wybierz **ponowne uruchomienie serwera docelowego hello automatycznie w razie potrzeby**, a następnie kliknij przycisk **tak** na powitania ostrzeżenie o ponownym uruchomieniu.
   13. Kliknij pozycję **Zainstaluj**. Witaj komputer zostanie uruchomiony ponownie.
5. Zainstaluj dodatkowe funkcje wymagane przez aplikacje, takie jak hello .NET Framework 3.5. Funkcje hello tooinstall, uruchom Kreatora hello dodawania ról i funkcji.
6. Instalowanie i konfigurowanie hello programy i aplikacje mają toopublish za pośrednictwem usługi RemoteApp.

> [!IMPORTANT]
> Zainstaluj rolę RDSH hello przed zainstalowaniem aplikacji tooensure odnaleziono wszelkie problemy ze zgodnością aplikacji przed obraz powitania jest przekazywane tooRemoteApp.
> 
> Upewnij się, że aplikacja tooyour skrótów (**lnk** plików) jest wyświetlana w hello **Start** menu dla wszystkich użytkowników (%systemdrive%\ProgramData\Microsoft\Windows\Start Start\Programy). Upewnij się również tę ikonę hello w hello **Start** menu ma toosee użytkowników. Jeśli nie, należy ją zmienić. (Nie *ma* menu Start toohello aplikacji hello tooadd, ale ułatwia znacznie łatwiejsze aplikacji hello toopublish w usłudze RemoteApp. W przeciwnym razie należy tooprovide hello ścieżka instalacji aplikacji hello podczas publikowania aplikacji hello.)
> 
> 

1. Wykonywać żadnych dodatkowych konfiguracji systemu Windows wymagane przez aplikacje.
2. Wyłącz hello system szyfrowania plików (EFS). Uruchom następujące polecenie w oknie polecenia z podwyższonym poziomem uprawnień hello:
   
     Działanie polecenia fsutil ustawić disableencryption 1
   
   Alternatywnie możesz ustawić lub Dodaj następujące wartości DWORD w rejestrze hello hello:
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Jeśli tworzysz obraz wewnątrz maszyny wirtualnej platformy Azure, Zmień nazwę hello  **\%windir%\Panther\Unattend.xml** pliku, ponieważ spowoduje to zablokowanie skryptu przekazywania hello użycia później w pracy. Tak, aby nadal będziesz mieć hello pliku, w razie potrzeby toorevert wdrożenia, należy zmienić nazwę hello tooUnattend.old tego pliku.
4. Przejdź tooWindows aktualizacji i zainstalować wszystkie ważne aktualizacje. Wszystkie aktualizacje mogą wymagać toorun usługi Windows Update tooget wiele razy. (Czasami zainstalowania aktualizacji, i tej samej aktualizacji wymaga aktualizacji).
5. Obraz powitania programu SYSPREP. W wierszu polecenia z podwyższonym poziomem uprawnień uruchom następujące polecenie hello:
   
   **C:\Windows\System32\sysprep\sysprep.exe / generalize/shutdown/oobe**
   
   **Uwaga:** nie należy używać hello **/mode:vm** przełącznika hello polecenia SYSPREP nawet, jeśli jest to maszyny wirtualnej.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz obrazu niestandardowego szablonu należy tooupload tooyour tego obrazu kolekcji usługi RemoteApp. Użyj informacji hello w hello następujące artykuły toocreate kolekcji:

* [Jak toocreate kolekcji hybrydowej RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Jak toocreate kolekcji usługi RemoteApp w chmurze](remoteapp-create-cloud-deployment.md)

