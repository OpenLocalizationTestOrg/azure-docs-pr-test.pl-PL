---
title: aaaPrepare tooAzure tooupload wirtualnego dysku twardego Windows | Dokumentacja firmy Microsoft
description: Jak tooprepare Windows VHD lub VHDX przed przekazaniem tooAzure
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Przygotowanie tooAzure tooupload Windows VHD lub VHDX
Przed przekazaniem maszyn wirtualnych systemu Windows (VM) z lokalnymi tooMicrosoft Azure, należy przygotować hello wirtualnego dysku twardego (VHD lub VHDX). Azure obsługuje tylko generacji 1 maszyn wirtualnych, które mają w formacie pliku VHD hello dysku o rozmiarze stałym. Witaj maksymalny rozmiar dozwolony dla hello wirtualny dysk twardy jest 1,023 GB. Możesz przekonwertować generacji 1 maszyny Wirtualnej z hello VHDX tooVHD systemu plików i z dynamicznie powiększający się na dysku o rozmiarze toofixed. Ale nie można zmienić generacji maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [generacji 1 lub 2 należy utworzyć maszyny Wirtualnej w funkcji Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).

Aby uzyskać więcej informacji o hello zasady udzielania pomocy technicznej dla maszyny Wirtualnej platformy Azure, zobacz [pomocy technicznej oprogramowanie serwera firmy Microsoft dla maszyn wirtualnych Azure Microsoft](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

> [!Note]
> Witaj instrukcje w tym artykule zastosować toohello 64-bitowej wersji systemu Windows Server 2008 R2 i nowszym system operacyjny Windows server. Informacje o 32-bitowej wersji systemu operacyjnego na platformie Azure, zobacz [obsługa 32-bitowych systemów operacyjnych w maszynach wirtualnych platformy Azure](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>Konwertuj hello tooVHD dysku wirtualnego i dysku o stałym rozmiarze 
Jeśli potrzebujesz tooconvert toohello Twojego dysku wirtualnego wymagany format dla platformy Azure, użyj jednej z metod hello w tej sekcji. Utwórz kopię zapasową hello maszyny Wirtualnej przed uruchomieniem procesu konwersji dysku wirtualnego hello i upewnij się, że powitalne wirtualnego dysku twardego Windows działa ona prawidłowo na lokalnym serwerze hello. Usuń wszelkie błędy w ciągu hello samej maszyny Wirtualnej, zanim spróbuj tooconvert lub przekaż go tooAzure.

Po przekonwertowaniu hello dysku, utwórz maszynę Wirtualną, która używa hello konwersji dysku. Uruchom i zaloguj się na toofinish VM toohello przygotowania hello maszyny Wirtualnej do przekazania.

### <a name="convert-disk-using-hyper-v-manager"></a>Konwertuj dysk przy użyciu Menedżera funkcji Hyper-V
1. Otwórz Menedżera funkcji Hyper-V, a następnie wybierz komputer lokalne powitania po lewej stronie. W menu hello powyżej hello listy komputerów, kliknij przycisk **akcji** > **Edytuj dysk**.
2. Na powitania **lokalizowanie wirtualnego dysku twardego** ekranu, Znajdź i zaznacz dysku wirtualnego.
3. Na powitania **wybierz akcję** ekranu, a następnie wybierz **przekonwertować** i **dalej**.
4. Jeśli potrzebujesz tooconvert z VHDX, wybierz **wirtualnego dysku twardego** , a następnie kliknij przycisk **dalej**
5. Jeśli potrzebujesz tooconvert z dynamicznie powiększających się dysków, wybierz **stały rozmiar** , a następnie kliknij przycisk **dalej**
6. Znajdź i zaznacz ścieżki toosave hello nowego wirtualnego dysku twardego pliku.
7. Kliknij przycisk **Zakończ**.

>[!NOTE]
>polecenia Hello w tym artykule muszą zostać uruchomione w sesji programu PowerShell z podwyższonym poziomem uprawnień.

### <a name="convert-disk-by-using-powershell"></a>Konwertuj dysk przy użyciu programu PowerShell
Można przekonwertować dysku wirtualnego za pomocą hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) polecenia w programie Windows PowerShell. Wybierz **Uruchom jako administrator** podczas uruchamiania programu PowerShell. 

Witaj następujące przykładowe polecenie konwertuje z VHDX tooVHD i dynamicznie powiększających się dysków toofixed, rozmiar:

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
W tym poleceniu zastąp wartość hello "-ścieżki" hello ścieżki toohello wirtualnego dysku twardego, który ma zostać zwrócona wartość tooconvert i hello dla "-Ścieżka_docelowa" hello nową ścieżkę i nazwę hello konwertowane dysku.

### <a name="convert-from-vmware-vmdk-disk-format"></a>Konwersja z formatu dysku VMware VMDK
Jeśli obraz maszyny Wirtualnej systemu Windows hello [format pliku VMDK](https://en.wikipedia.org/wiki/VMDK), przekonwertuj go tooa wirtualnego dysku twardego za pomocą hello [konwerter maszyny Wirtualnej Microsoft](https://www.microsoft.com/download/details.aspx?id=42497). Aby uzyskać więcej informacji, zobacz artykuł blogu hello [jak tooConvert dysku VHD tooHyper V VMware VMDK](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).

## <a name="set-windows-configurations-for-azure"></a>Ustawianie konfiguracji systemu Windows Azure

Na powitania maszyny Wirtualnej, który planujesz tooAzure tooupload, uruchom wszystkie polecenia w następujących hello kroków z [okno wiersza polecenia z podwyższonym poziomem uprawnień](https://technet.microsoft.com/library/cc947813.aspx):

1. Usuń wszystkie statyczne trasę w tabeli routingu hello:
   
   * Tabela tras hello tooview, uruchom `route print` hello wiersza polecenia.
   * Sprawdź hello **trasy trwałości** sekcje. Jeśli trwałą trasę, użyj [Usuń trasy](https://technet.microsoft.com/library/cc739598.apx) tooremove go.
2. Usuwanie serwera proxy WinHTTP hello:
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. Ustaw zasady sieci SAN dysku hello zbyt[Onlineall](https://technet.microsoft.com/library/gg252636.aspx). 
   
    ```PowerShell
    diskpart 
    ```
    W hello Otwórz okno wiersza polecenia wpisz następujące polecenia hello:

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Ustawianie czasu uniwersalnego czasu koordynowanego (UTC) dla systemu Windows i hello typ uruchomienia usługi Czas systemu Windows (w32time) hello zbyt**automatycznie**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Ustaw hello zasilania profilu toohello **wysokiej wydajności**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Sprawdź usługi Windows hello
Upewnij się, że ustawiono każdego z następujących usług systemu Windows hello toohello **wartości domyślnych systemu Windows**. Są to hello minimalnej liczby usług, które muszą zostać skonfigurowane toomake upewnić się, że hello maszyna wirtualna ma łączność. tooreset hello ustawień uruchamiania, uruchom następujące polecenia hello:
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>Aktualizowanie ustawień rejestru pulpitu zdalnego
Upewnij się, że hello następujące ustawienia są poprawnie skonfigurowane dla połączeń usług pulpitu zdalnego:

>[!Note] 
>Może pojawić się komunikat o błędzie podczas uruchamiania hello **ItemProperty zestaw-ścieżki "HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal usługi - nazwa &lt;nazwa obiektu&gt; &lt;wartość&gt;** w tych krokach. komunikat o błędzie Hello można bezpiecznie zignorować. Oznacza to, że w tej domenie hello nie wypycha takiej konfiguracji za pomocą obiektu zasad grupy.
>
>

1. Włączono protokołu RDP (Remote Desktop):
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. Witaj portem RDP jest poprawnie skonfigurowany (domyślny port 3389):
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    Podczas wdrażania maszyny Wirtualnej hello domyślne reguły są tworzone z portu 3389. Jeśli chcesz numer portu hello toochange, należy to zrobić, po wdrożeniu hello maszyny Wirtualnej na platformie Azure.

3. odbiornik Hello nasłuchuje w każdym interfejsu sieciowego:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Konfigurowanie hello trybu uwierzytelniania na poziomie sieci dla połączeń protokołu RDP hello:
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Ustaw wartość keep-alive hello:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. Połącz ponownie:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Ogranicz hello liczbę równoczesnych połączeń:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. Jeśli istnieją wszystkie certyfikaty z podpisem własnym powiązane toohello odbiornika protokołu RDP, usuń je:
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    Jest to toomake można łączenie na początku hello podczas wdrażania hello maszyny Wirtualnej. Można to również przejrzeć na późniejszym etapie po hello wdrożonej maszyny Wirtualnej Azure, w razie potrzeby.

9. Jeśli hello maszyna wirtualna ma być częścią domeny, sprawdź, czy wszystkie hello następujące ustawienia toomake się, że hello wcześniejsze ustawienia nie są przywracane. Witaj zasad, które muszą zostać sprawdzone są następujące hello:
    
    - Protokół RDP jest włączony:

         Komputer Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative Templates\ Windows\Usługi pulpitu usług sesji usług pulpitu zdalnego\Połączenia:
         
         **Zezwalaj użytkownikom tooconnect zdalnie przy użyciu pulpitu zdalnego**

    - Zasady grupy uwierzytelniania na poziomie sieci:

        Pulpitu sesji usług pulpitu Templates\Components\Remote Settings\Administrative zdalnego\Zabezpieczenia: 
        
        **Wymagaj uwierzytelniania użytkownika dla połączeń zdalnych za pomocą uwierzytelniania na poziomie sieci**
    
    - Zachowaj ustawienia może działa:

        Komputer Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative administracyjne\Składniki systemu Windows\Usługi pulpitu usług sesji usług pulpitu zdalnego\Połączenia: 
        
        **Skonfiguruj interwał podtrzymania połączenia.**

    - Połącz ponownie ustawienia:

        Komputer Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative administracyjne\Składniki systemu Windows\Usługi pulpitu usług sesji usług pulpitu zdalnego\Połączenia: 
        
        **Automatyczne ponowne łączenie**

    - Ogranicz liczbę hello ustawienia połączeń:

        Komputer Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative administracyjne\Składniki systemu Windows\Usługi pulpitu usług sesji usług pulpitu zdalnego\Połączenia: 
        
        **Ogranicz liczbę połączeń**

## <a name="configure-windows-firewall-rules"></a>Konfigurowanie reguł zapory systemu Windows
1. Włącz Zaporę systemu Windows hello trzy profile (domena, Standard i publicznego):

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Uruchom następujące polecenie w środowiska PowerShell tooallow WinRM za pośrednictwem hello trzy profile zapory (domeny, prywatne i publiczne) hello i Włącz hello usługi zdalne środowiska PowerShell:
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. Włącz powitania po ruch RDP hello tooallow reguły zapory 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Włącz hello plików i udostępnianie drukarki reguły hello maszyny Wirtualnej można udzielenia odpowiedzi polecenia ping tooa wewnątrz hello sieci wirtualnej:

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Jeśli hello maszyna wirtualna ma być częścią domeny, sprawdź następujące ustawienia toomake się, że nie zostaną przywrócone poprzednie ustawienia hello hello. zasady Hello AD, które muszą zostać sprawdzone są następujące hello:

    - Włączanie profilów zapory systemu Windows hello

        Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative administracyjne\Sieć\Połączenia Connection\Windows Firewall\Domain Profile\Windows zapory: **ochrony wszystkich połączeń sieciowych**

       Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative administracyjne\Sieć\Połączenia Connection\Windows Firewall\Standard Profile\Windows zapory: **ochrony wszystkich połączeń sieciowych**

    - Włącz protokół RDP 

        Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative administracyjne\Sieć\Połączenia Connection\Windows Firewall\Domain Profile\Windows zapory: **Zezwalaj na wyjątki pulpitu zdalnego dla ruchu przychodzącego**

        Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative administracyjne\Sieć\Połączenia Connection\Windows Firewall\Standard Profile\Windows zapory: **Zezwalaj na wyjątki pulpitu zdalnego dla ruchu przychodzącego**

    - Włącz protokół ICMP-V4

        Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative administracyjne\Sieć\Połączenia Connection\Windows Firewall\Domain Profile\Windows zapory: **Zezwalaj na wyjątki protokołu ICMP**

        Konfiguracja komputera\Zasady\Ustawienia systemu Settings\Administrative administracyjne\Sieć\Połączenia Connection\Windows Firewall\Standard Profile\Windows zapory: **Zezwalaj na wyjątki protokołu ICMP**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>Sprawdź, czy maszyna wirtualna jest w dobrej kondycji, bezpieczne i dostępne przy użyciu protokołu RDP 
1. Czy na dysku hello toomake jest dobrej kondycji i spójny, uruchom operację sprawdzania dysku na powitania następnym ponownym uruchomieniu maszyny Wirtualnej:

    ```PowerShell
    Chkdsk /f
    ```
    Upewnij się, że hello przedstawia dysku czyste i działa prawidłowo.

2. Ustawienia hello danych konfiguracji rozruchu (BCD). 

    > [!Note]
    > Upewnij się, uruchom następujące polecenia z podwyższonym poziomem uprawnień okna CMD i **nie** na środowiska PowerShell:
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. Sprawdź, czy tego repozytorium Instrumentations zarządzania systemu Windows hello jest spójna. tooperform tego hello uruchom następujące polecenie:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    Jeśli repozytorium hello jest uszkodzony, zobacz [WMI: uszkodzenie repozytorium lub nie](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).

4. Upewnij się, że inna aplikacja nie używa hello portu 3389. Port ten jest używany dla hello usługi protokołu RDP na platformie Azure. Można uruchomić **netstat - anob** toosee, które porty są w używane na powitania maszyny Wirtualnej:

    ```PowerShell
    netstat -anob
    ```

5. Jeśli hello dysku VHD systemu Windows, które mają tooupload jest kontrolerem domeny, następnie wykonaj następujące czynności:

    A. Postępuj zgodnie z [te dodatkowe kroki](https://support.microsoft.com/kb/2904015) tooprepare hello dysku.

    B. Upewnij się, że znasz hasła trybu DSRM hello w przypadku, gdy masz hello toostart maszyny Wirtualnej w trybie DSRM w pewnym momencie. Może być toorefer toothis link tooset hello [hasło trybu DSRM](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).

6. Upewnij się, że tooyou wiadomo hello wbudowanego konta administratora i hasła. Może mają tooreset hello bieżące hasło administratora lokalnego i upewnij się, czy możesz użyć tego konta toosign w tooWindows za pośrednictwem połączenia RDP hello. To uprawnienie dostępu jest kontrolowane przez obiekt zasad grupy "Zezwalaj na logowanie za pomocą usług pulpitu zdalnego" hello. Można wyświetlić tego obiektu w hello Edytora lokalnych zasad grupy w obszarze:

    Komputer opcji Konfiguracja komputera\Ustawienia systemu Windows\Ustawienia zabezpieczeń\Zasady Lokalne\przypisywanie praw użytkownika

7. Sprawdź, czy następujące AD hello zasady toomake się upewnić, czy nie blokuje dostępu RDP za pośrednictwem protokołu RDP ani z sieci hello:

    - Konfiguracja komputera\Ustawienia systemu Windows\Ustawienia zabezpieczeń\Zasady lokalne\Przypisywanie praw Assignment\Deny dostępu toothis komputera z sieci hello

    - Komputer logowania opcji Konfiguracja komputera\Ustawienia systemu Windows\Ustawienia zabezpieczeń\Zasady lokalne\Przypisywanie praw Assignment\Deny za pomocą usług pulpitu zdalnego


8. Ponowne uruchomienie hello wirtualna toomake się upewnić, że system Windows jest nadal działa prawidłowo przy użyciu połączenia protokołu RDP hello jest osiągalna. Na tym etapie może mają toocreate maszyny Wirtualnej w sieci lokalnej funkcji Hyper-V toomake czy powitalne całkowicie uruchamiania maszyny Wirtualnej, a następnie sprawdzić, czy jest dostępny RDP.

9. Usuń wszystkie filtry dodatkowy interfejs sterownika transportu, takiego jak oprogramowanie, która analizuje TCP pakiety lub dodatkowych zapór. Można to również przejrzeć na późniejszym etapie po hello wdrożonej maszyny Wirtualnej Azure, w razie potrzeby.

10. Odinstalować inne oprogramowanie innych firm i sterownika, który jest toophysical pokrewne składniki lub innych technologii wirtualizacji.

### <a name="install-windows-updates"></a>Instalowanie aktualizacji systemu Windows
Konfiguracja nadaje się doskonale Hello jest zbyt**ma poziom poprawki hello maszyny hello na powitania najnowszych**. Jeśli nie jest to możliwe, upewnij się, że hello następujące aktualizacje są instalowane:

|                       |                   |           |                                       Minimalna wersja x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| Składnik               | Binarne            | Windows 7 i Windows Server 2008 R2 | Windows 8 i Windows Server 2012             | Windows 8.1 i Windows Server 2012 R2 | Windows 10 i Windows Server 2016 RS1 | RS2 systemu Windows 10             |
| Magazyn                 | Disk.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 - KB3137061 | 6.3.9600.18203 - KB3137061           | -                                    | -                          |
|                         | Storport.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 - KB3018489 | 6.3.9600.18573 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.332             |
|                         | NTFS.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 - KB3121255 | 6.3.9600.18654 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 - KB3125574         | 6.2.9200.16384 - KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 - KB2995387 | 6.3.9600.18334 - KB3172614           | 10.0.14393.953 - KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 - KB2975331 | 6.3.9600.18265 - KB3145384           | -                                    | 10.0.15063.0               |
|                         | PartMgr.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.16681 - KB2877114                  | 6.3.9600.17401 - KB3000850           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.21006 - KB2955163                  | 6.3.9600.18624 - KB4022726           | 10.0.14393.1066 - KB4022715          | 10.0.15063.447             |
|                         | MSDSM.sys         | 6.1.7601.23403 - KB3125574         | 6.2.9200.21474 - KB3046101                  | 6.3.9600.18592 - KB4022726           | -                                    | -                          |
|                         | MPIO.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.21190 - KB3046101                  | 6.3.9600.18616 - KB4022726           | 10.0.14393.1198 - KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.18294 - KB3172614           | 10.0.14393.576 - KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.17415 - KB3172614           | 10.0.14393.206 - KB4022715           | -                          |
| Sieć                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 - KB4022715          | 10.0.15063.250 - KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.22108 - KB4022724                  | 6.3.9600.18603 - KB4022726           | 10.0.14393.479 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.21548 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.483             |
|                         | Mrxsmb.sys        | 6.1.7601.23816 - KB4022722         | 6.2.9200.22074 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | Tcpip.sys         | 6.1.7601.23761 - KB4022722         | 6.2.9200.22070 - KB4022724                  | 6.3.9600.18478 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.447             |
|                         | Sterownik HTTP.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17285 - KB3042553                  | 6.3.9600.18574 - KB4022726           | 10.0.14393.251 - KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 - KB4022719         | 6.2.9200.22117 - KB4022724                  | 6.3.9600.18654 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.138             |
| Podstawowe                    | Ntoskrnl.exe      | 6.1.7601.23807 - KB4022719         | 6.2.9200.22170 - KB4022718                  | 6.3.9600.18696 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.483             |
| Usługi pulpitu zdalnego | rdpcorets.dll     | 6.2.9200.21506 - KB4022719         | 6.2.9200.22104 - KB4022724                  | 6.3.9600.18619 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.0               |
|                         | Termsrv.dll       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17048 - KB2973501                  | 6.3.9600.17415 - KB3000850           | 10.0.14393.0 - KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | Win32k.sys        | 6.1.7601.23807 - KB4022719         | 6.2.9200.22168 - KB4022718                  | 6.3.9600.18698 - KB4022726           | 10.0.14393.594 - KB4022715           | -                          |
|                         | Rdpdd.dll         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | Rdpwd.sys         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
| Bezpieczeństwo                | Z powodu tooWannaCrypt | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### Gdy program sysprep toouse<a id="step23"></a>    

Sysprep to proces, który można uruchomić do instalacji systemu windows, spowoduje zresetowanie hello instalacji hello systemu, który zapewni "fabrycznej hello wystąpić" przez usunięcie wszystkich danych osobowych i zresetowanie kilka składników. Zwykle w tym przypadku ma toocreate szablon, w którym można wdrożyć kilka innych maszyn wirtualnych, które mają konkretną konfigurację. Ta metoda jest wywoływana **uogólniony obraz**.

Jeśli zamiast tego chcesz tylko toocreate, jednej maszyny Wirtualnej z jednego dysku, nie masz toouse programu sysprep. W takiej sytuacji można utworzyć maszyny Wirtualnej z tym, co jest nazywane hello **specjalne obrazu**.

Aby uzyskać więcej informacji na temat toocreate maszyny Wirtualnej z dysku specjalne, zobacz temat:

- [Utwórz maszynę Wirtualną z dyskiem specjalne](create-vm-specialized.md)
- [Tworzenie maszyny Wirtualnej z dysku VHD specjalne](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

Jeśli chcesz toocreate uogólniony obraz należy toorun programu sysprep. Aby uzyskać więcej informacji na temat narzędzia Sysprep, zobacz [jak tooUse Sysprep: wprowadzenie](http://technet.microsoft.com/library/bb457073.aspx). 

Nie każda rola lub aplikacji, która jest zainstalowana na komputerze z systemem Windows obsługuje ten generalizacji. Dlatego przed uruchomić tę procedurę, zapoznaj się toohello się, że po toomake artykułu tej roli hello tego komputera jest obsługiwana przez program sysprep. Aby uzyskać więcej informacji [Obsługa programu Sysprep dla ról serwera](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

### <a name="steps-toogeneralize-a-vhd"></a>Kroki toogeneralize wirtualnego dysku twardego

>[!NOTE]
> Po uruchomieniu sysprep.exe jako określone w hello następujące kroki, wyłącz hello maszyny Wirtualnej, a nie włączyć ją ponownie do czasu utworzenia obrazu z niego na platformie Azure.

1. Zaloguj się toohello maszyny Wirtualnej systemu Windows.
2. Uruchom **wiersza polecenia** jako administrator. 
3. Zmień katalog hello: **%windir%\system32\sysprep**, a następnie uruchom **sysprep.exe**.
3. W hello **narzędzie przygotowania systemu** okno dialogowe, wybierz opcję **wprowadź systemu Out-of-Box Experience (OOBE)**i upewnij się, że hello **Generalize** pole wyboru jest zaznaczone.

    ![Narzędzie przygotowywania systemu](media/prepare-for-upload-vhd-image/syspre.png)
4. W **opcje zamykania**, wybierz pozycję **zamknięcia**.
5. Kliknij przycisk **OK**.
6. Po zakończeniu działania programu Sysprep, zamknij hello maszyny Wirtualnej. Nie używaj **Uruchom ponownie** tooshut dół hello maszyny Wirtualnej.
7. Teraz hello wirtualnego dysku twardego jest gotowy toobe przekazany. Aby uzyskać więcej informacji na temat toocreate maszyny Wirtualnej z dyskiem uogólniony, zobacz temat [przekazać uogólniony wirtualny dysk twardy i korzystać z niego toocreate nowych maszyn wirtualnych na platformie Azure](sa-upload-generalized.md).


## <a name="complete-recommended-configurations"></a>Dokończ konfigurację zalecane
Witaj następujące ustawienia nie wpływają na przekazywanie wirtualnego dysku twardego. Zaleca się jednak skonfigurować je.

* Zainstaluj hello [agenta maszyny wirtualne Azure](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Następnie można włączyć rozszerzenia maszyny Wirtualnej. Hello rozszerzeń maszyny Wirtualnej wykonuje większość funkcji krytyczne hello czy może chcesz toouse maszyn wirtualnych np. zresetowania hasła, konfigurowanie protokołu RDP i tak dalej. Aby uzyskać więcej informacji, zobacz:

    - [Agent maszyny Wirtualnej i rozszerzenia — część 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - [Agent maszyny Wirtualnej i rozszerzenia — część 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* Hello zrzutu dziennika mogą być pomocne przy rozwiązywaniu problemów awarii systemu Windows. Włącz zbieranie danych dziennika zrzutu hello:
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    Jeśli wystąpią błędy podczas wszystkich procedur hello kroków w tym artykule, oznacza to, czy klucze rejestru hello już istnieje. W takiej sytuacji należy użyć hello zamiast tego następujące polecenia:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Po utworzeniu hello maszyny Wirtualnej na platformie Azure zaleca się umieszczenie hello pliku stronicowania na wydajność tooimprove woluminu "Dysk danych czasowych" hello. Można skonfigurować to w następujący sposób:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
W przypadku każdego dysku danych, który jest dołączony toohello maszyny Wirtualnej, literę dysku woluminu dysku danych czasowych hello jest zazwyczaj "D." Ta nazwa może być różne w zależności od liczby hello dostępne dyski i ustawienia hello, wprowadzone.

## <a name="next-steps"></a>Następne kroki
* [Przekaż tooAzure obrazu maszyny Wirtualnej systemu Windows, w przypadku wdrożeń usługi Resource Manager](upload-generalized-managed.md)

