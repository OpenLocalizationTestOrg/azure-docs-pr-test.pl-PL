---
title: "Tworzenie niestandardowego obrazu szablonu usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć obraz niestandardowy szablon dla usługi Azure RemoteApp. Można użyć tego szablonu z kolekcji hybrydowej lub chmury."
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
ms.openlocfilehash: f529a5526f266c7dbac3c719b244d05ab7705941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-custom-template-image-for-azure-remoteapp"></a>Tworzenie niestandardowego obrazu szablonu usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Usługa Azure RemoteApp używa obrazu szablonu systemu Windows Server 2012 R2 do obsługi wszystkich programów, które chcesz udostępniać użytkownikom. Aby utworzyć niestandardowego obrazu szablonu usługi RemoteApp, można rozpoczynać się od istniejącego obrazu lub Utwórz nową. 

> [!TIP]
> Czy wiesz, że można utworzyć obrazu z maszyny Wirtualnej platformy Azure? TRUE wątku który ogranicza ilość czasu go przyjmuje do zaimportowania obrazu. Sprawdź kroki [tutaj](remoteapp-image-on-azurevm.md).
> 
> 

Wymagania dotyczące obrazu, który można przekazać do użycia z usługą Azure RemoteApp są:

* Rozmiar obrazu powinna być wielokrotnością liczby MB. Jeśli spróbujesz Przekaż obraz, który nie jest wielokrotnością przekazywania zakończy się niepowodzeniem.
* Rozmiar obrazu musi mieć 127 GB lub mniej.
* Musi znajdować się na plik VHD (pliki VHDX [funkcji Hyper-V wirtualnych dysków twardych] nie są obecnie obsługiwane).
* Dysk VHD nie może być maszyny wirtualnej generacji 2.
* Wirtualny dysk twardy może być stałym rozmiarze lub dynamicznie powiększających się. Dynamicznie powiększających się dysków VHD jest zalecane, ponieważ zajmuje mniej czasu na platformie Azure niż ustalony rozmiar pliku VHD.
* Dysk musi być zainicjowany przy użyciu główny rekord rozruchowy (MBR) partycjonowania. Styl partycji GUID partycji (GPT tabela) nie jest obsługiwana.
* Wirtualny dysk twardy musi zawierać jednej instalacji systemu Windows Server 2012 R2. Nazwa może zawierać wiele woluminów, ale tylko jeden zawartych w instalacji systemu Windows.
* Musi być zainstalowana rola hosta sesji zdalnego pulpitu (RDSH) i funkcja Środowisko pulpitu.
* Roli Broker połączeń usług pulpitu zdalnego musi *nie* można zainstalować.
* System szyfrowania plików (EFS) musi być wyłączona.
* Obraz musi być przetworzonej przez program Sysprep przy użyciu parametrów **/oobe / generalize/shutdown** (Użyj nie **/mode:vm** parametru).
* Przekazywanie dysk VHD z łańcucha migawek nie jest obsługiwane.

**Przed rozpoczęciem**

Należy wykonać następujące czynności przed utworzeniem usługi:

* [Zarejestruj się](https://azure.microsoft.com/services/remoteapp/) usługi RemoteApp.
* Utwórz konto użytkownika w usłudze Active Directory do użycia jako konto usługi RemoteApp. Ograniczyć uprawnienia dla tego konta, tak aby tylko można przyłączyć maszyny do domeny. Zobacz [Konfigurowanie usługi Azure Active Directory dla usługi RemoteApp](remoteapp-ad.md) Aby uzyskać więcej informacji.
* Zbieranie informacji o sieci lokalnej: adres IP informacje i szczegóły urządzenia sieci VPN.
* Zainstaluj [programu Azure PowerShell](/powershell/azure/overview) modułu.
* Zbierz informacje o użytkownikach, które chcesz udzielić dostępu do. Może to być informacje o koncie Microsoft lub informacje o koncie pracy usługi Active Directory dla użytkowników.

## <a name="create-a-template-image"></a>Tworzenie obrazu szablonu
Poniżej przedstawiono kroki wysokiego poziomu do utworzenia nowego obrazu szablonu od początku:

1. Zlokalizuj obraz dysku DVD systemu Windows Server 2012 R2 Update lub ISO.
2. Utwórz plik wirtualnego dysku twardego.
3. Instalowanie systemu Windows Server 2012 R2.
4. Zainstalowanie roli hosta sesji zdalnego pulpitu (RDSH) i funkcja Środowisko pulpitu.
5. Zainstaluj dodatkowe funkcje wymagane przez aplikacje.
6. Instalowanie i konfigurowanie aplikacji. Aby ułatwić udostępniania aplikacji, Dodaj wszelkie aplikacje lub programy, które chcesz udostępnić **Start** menu obrazu, w szczególności w **%systemdrive%\ProgramData\Microsoft\Windows\Start Start\Programy.
7. Wykonywać żadnych dodatkowych konfiguracji systemu Windows wymagane przez aplikacje.
8. Wyłącz System szyfrowania plików (EFS).
9. **WYMAGANE:** przejdź do witryny Windows Update i zainstalować wszystkie ważne aktualizacje.
10. Obraz SYSPREP.

Szczegółowe kroki tworzenia nowego obrazu są:

1. Zlokalizuj obraz dysku DVD systemu Windows Server 2012 R2 Update lub ISO.
2. Utwórz plik VHD za pomocą przystawki Zarządzanie dyskami.
   
   1. Uruchamianie przystawki Zarządzanie dyskami (diskmgmt.msc).
   2. Utwórz dynamicznie powiększających się wirtualny dysk twardy 40 GB lub więcej rozmiar. (Oszacować ilość miejsca potrzebnego do systemu Windows, aplikacje i dostosowania. Windows Server z rolą RDSH i zainstalowana funkcja Środowisko pulpitu wymaga około 10 GB miejsca).
      
      1. Kliknij przycisk **akcji > tworzenia wirtualnego dysku twardego**.
      2. Określ lokalizację, rozmiar i formatu wirtualnego dysku twardego. Wybierz **dynamicznie powiększających się**, a następnie kliknij przycisk **OK**.
      
      Spowoduje to uruchomienie przez kilka sekund. Po zakończeniu tworzenia dysku VHD powinien zostać wyświetlony nowy dysk bez dowolnej litery dysku i jest w stanie "Nie jest zainicjowana" w konsoli Zarządzanie dyskami.
      
      * Kliknij prawym przyciskiem myszy dysk (nie nieprzydzielone miejsce), a następnie kliknij przycisk **Inicjowanie dysku**. Wybierz **MBR** (główny rekord rozruchowy) styl partycji, a następnie kliknij przycisk **OK**.
      * Utwórz nowy wolumin: kliknij prawym przyciskiem myszy nieprzydzielone miejsce, a następnie kliknij przycisk **nowy wolumin prosty**. Można zaakceptować wartości domyślne kreatora, ale upewnij się, że przypisać literę dysku, aby uniknąć potencjalnych problemów podczas ładowania obrazu szablonu.
      * Kliknij prawym przyciskiem myszy dysk, a następnie kliknij przycisk **Odłącz dysk VHD**.
3. Instalowanie systemu Windows Server 2012 R2:
   
   1. Tworzenie nowej maszyny wirtualnej. Użyj Kreatora nowej maszyny wirtualnej w funkcji Hyper-V klienta lub Menedżera funkcji Hyper-V.
      1. Na stronie Określanie generacji, wybierz **generacja 1**.
      2. Na stronie Podłączanie wirtualnego dysku twardego wybierz **Użyj istniejącego wirtualnego dysku twardego**, a następnie przejdź do wirtualnego dysku twardego utworzonego w poprzednim kroku.
      3. Na stronie opcji instalacji wybierz **zainstalować system operacyjny z rozruchowego dysku CD/DVD-ROM**, a następnie wybierz lokalizację nośnika instalacyjnego systemu Windows Server 2012 R2.
      4. Wybierz inne opcje w Kreatorze niezbędne do zainstalowania systemu Windows i aplikacji. Zakończ pracę kreatora.
   2. Po zakończeniu pracy kreatora, Edytuj ustawienia maszyny wirtualnej i wprowadzić inne zmiany niezbędne do zainstalowania systemu Windows i programów, takich jak liczba procesorów wirtualnych, a następnie kliknij przycisk **OK**.
   3. Połącz z maszyną wirtualną i zainstaluj system Windows Server 2012 R2.
4. Instalowanie roli hosta sesji zdalnego pulpitu (RDSH) i funkcja Środowisko pulpitu:
   1. Uruchom Menedżera serwera.
   2. Kliknij przycisk **Dodaj role i funkcje** na ekranie powitalnym lub z **Zarządzaj** menu.
   3. Kliknij przycisk **dalej** na stronie zanim rozpoczniesz.
   4. Wybierz **Instalacja roli lub funkcji**, a następnie kliknij przycisk **dalej**.
   5. Wybierz z listy komputera lokalnego, a następnie kliknij przycisk **dalej**.
   6. Wybierz **usług pulpitu zdalnego**, a następnie kliknij przycisk **dalej**.
   7. Rozwiń węzeł **infrastruktura i interfejsy użytkownika** i wybierz **środowisko pulpitu**.
   8. Kliknij przycisk **Dodaj funkcje**, a następnie kliknij przycisk **dalej**.
   9. Na stronie usługi pulpitu zdalnego kliknij **dalej**.
   10. Kliknij przycisk **hosta sesji usług pulpitu zdalnego**.
   11. Kliknij przycisk **Dodaj funkcje**, a następnie kliknij przycisk **dalej**.
   12. Na stronie Potwierdzanie opcji instalacji wybierz **automatycznie ponownie uruchom serwer docelowy, jeśli jest to wymagane**, a następnie kliknij przycisk **tak** na ostrzeżenie ponownego uruchomienia.
   13. Kliknij pozycję **Zainstaluj**. Komputer zostanie uruchomiony ponownie.
5. Zainstaluj dodatkowe funkcje wymagane przez aplikacje, takie jak program .NET Framework 3.5. Aby zainstalować funkcje, uruchom dodawania ról i funkcji — Kreator.
6. Instalowanie i konfigurowanie programy i aplikacje, które mają być opublikowane za pośrednictwem usługi RemoteApp.

> [!IMPORTANT]
> Zainstaluj rolę RDSH przed zainstalowaniem aplikacji, aby upewnić się, że wszelkie problemy ze zgodnością aplikacji są wykrywane przed obraz jest przekazywany do usługi RemoteApp.
> 
> Upewnij się, że skrót aplikacji (**lnk** plików) jest wyświetlana w **Start** menu dla wszystkich użytkowników (%systemdrive%\ProgramData\Microsoft\Windows\Start Start\Programy). Ponadto upewnij się, że ikona pojawi się w **Start** menu ma być widoczny dla użytkowników. Jeśli nie, należy ją zmienić. (Nie *ma* do dodania aplikacji do uruchomienia menu, ale ułatwia publikowanie aplikacji w usłudze RemoteApp. W przeciwnym razie należy podać ścieżkę instalacji dla aplikacji po opublikowaniu aplikacji.)
> 
> 

1. Wykonywać żadnych dodatkowych konfiguracji systemu Windows wymagane przez aplikacje.
2. Wyłącz System szyfrowania plików (EFS). Uruchom następujące polecenie w oknie polecenia z podwyższonym poziomem uprawnień:
   
     Działanie polecenia fsutil ustawić disableencryption 1
   
   Alternatywnie możesz ustawić lub Dodaj następującą wartość DWORD rejestru:
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Jeśli tworzysz obraz wewnątrz maszyny wirtualnej platformy Azure, Zmień nazwę  **\%windir%\Panther\Unattend.xml** pliku, ponieważ spowoduje to zablokowanie skryptu przekazywania użycia później w pracy. Zmień nazwę tego pliku na Unattend.old, dzięki czemu nadal będziesz mieć plik, w razie potrzeby można przywrócić wdrożenia.
4. Przejdź do witryny Windows Update i zainstalować wszystkie ważne aktualizacje. Może być konieczne uruchomienie usługi Windows Update kilka razy, aby pobrać wszystkie aktualizacje. (Czasami zainstalowania aktualizacji, i tej samej aktualizacji wymaga aktualizacji).
5. Obraz SYSPREP. W wierszu polecenia z podwyższonym poziomem uprawnień uruchom następujące polecenie:
   
   **C:\Windows\System32\sysprep\sysprep.exe / generalize/shutdown/oobe**
   
   **Uwaga:** nie używaj **/mode:vm** przełącznika polecenia SYSPREP nawet wtedy, gdy jest to maszyny wirtualnej.

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz obrazu niestandardowego szablonu, musisz przekazać go do kolekcji usługi RemoteApp. Do utworzenia kolekcji, użyj informacji w następujących artykułach:

* [Jak utworzyć kolekcję hybrydową RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Jak utworzyć kolekcję usługi RemoteApp w chmurze](remoteapp-create-cloud-deployment.md)

