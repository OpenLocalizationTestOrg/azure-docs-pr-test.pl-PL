---
title: "serwery aaaRemove i Wyłącz ochronę | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak magazyn toounregister serwerów z usługi Site Recovery i toodisable ochrony dla maszyn wirtualnych i serwerów fizycznych."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>Usuwanie serwerów i wyłączanie ochrony

Witaj usługi Azure Site Recovery przyczynia się tooyour ciągłość i strategia odzyskiwania (BCDR). Usługa Hello uruchamia replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Maszyny można replikowanych tooAzure lub tooa dodatkowej w lokalnym centrum danych. Aby zapoznać się z szybkim omówieniem, przeczytaj temat [Co to jest usługa Azure Site Recovery?](site-recovery-overview.md)

W tym artykule opisano sposób toounregister serwerów usług odzyskiwania magazynu w portalu Azure hello i jak toodisable ochrony maszyn chronione przez usługę Site Recovery.

Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="unregister-a-connected-configuration-server"></a>Wyrejestruj serwer konfiguracji połączenia

Jeśli replikujesz maszyny wirtualne VMware lub tooAzure serwerach fizycznych systemu Windows i Linux, serwer konfiguracji połączonych z magazynu można wyrejestrować w następujący sposób:

1. Wyłącz ochronę maszyny. W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**.
2. Usuń skojarzenie żadnych zasad. W **infrastruktura usługi Site Recovery** > **dla VMWare i maszyn fizycznych** > **zasady replikacji**, kliknij dwukrotnie hello skojarzonych zasad. Serwer konfiguracji powitania kliknij prawym przyciskiem myszy > **usuwanie skojarzenia**.
3. Usuń wszelkie dodatkowe lokalnymi procesu lub głównych serwerów docelowych. W **infrastruktura usługi Site Recovery** > **dla VMWare i maszyn fizycznych** > **serwery konfiguracji**, kliknij prawym przyciskiem myszy powitania serwera > **Usunąć**.
4. Usuń powitania serwera konfiguracji.
5. Ręcznie odinstalować usługi mobilności hello uruchomionej na powitania główny serwer docelowy (są to albo oddzielnym serwerze lub uruchomiona na serwerze konfiguracji hello).
6. Odinstaluj wszystkie serwery dodatkowych procesów.
7. Odinstaluj powitania serwera konfiguracji.
8. Na serwerze konfiguracji hello odinstalować hello wystąpienie MySQL, która została zainstalowana przez usługę Site Recovery.
9. W rejestrze hello powitania serwera konfiguracji należy usunąć klucz hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Wyrejestruj serwer odłączony konfiguracji

Jeśli replikujesz maszyny wirtualne VMware lub tooAzure serwerach fizycznych systemu Windows i Linux można wyrejestrować serwera konfiguracji odłączony z magazynu w następujący sposób:

1. Wyłącz ochronę maszyny. W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**. Wybierz **zatrzymywanie zarządzania hello maszyny**.
2. Usuń wszelkie dodatkowe lokalnymi procesu lub głównych serwerów docelowych. W **infrastruktura usługi Site Recovery** > **dla VMWare i maszyn fizycznych** > **serwery konfiguracji**, kliknij prawym przyciskiem myszy powitania serwera > **Usunąć**.
3. Usuń powitania serwera konfiguracji.
4. Ręcznie odinstalować usługi mobilności hello uruchomionej na powitania główny serwer docelowy (są to albo oddzielnym serwerze lub uruchomiona na serwerze konfiguracji hello).
5. Odinstaluj wszystkie serwery dodatkowych procesów.
6. Odinstaluj powitania serwera konfiguracji.
7. Na serwerze konfiguracji hello odinstalować hello wystąpienie MySQL, która została zainstalowana przez usługę Site Recovery.
8. W rejestrze hello powitania serwera konfiguracji należy usunąć klucz hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Wyrejestruj połączony z serwerem VMM

Jako najlepsze rozwiązanie zaleca się wyrejestrować serwera VMM hello, gdy jest podłączone tooAzure. Daje to pewność, że ustawienia na serwerach VMM hello (i na innych serwerach VMM z pary chmur) są prawidłowo czyszczone. Odłączony serwer należy usunąć tylko wtedy, gdy stałe problem z łącznością. Jeśli serwer VMM hello nie jest połączony, konieczne będzie toomanually Uruchom skrypt tooclean ustawień.

1. Zatrzymaj replikowanie maszyn wirtualnych w chmurach na powitania serwera VMM ma tooremove.
2. Usuń wszystkie używane przez chmury na powitania serwera VMM ma toodelete mapowania sieci. W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **mapowania sieci**, kliknij prawym przyciskiem myszy mapowania sieci hello >  **Usuń**.
3. Usuń skojarzenia zasad replikacji z chmury na powitania serwera VMM ma tooremove.  W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** >  **zasady replikacji**, kliknij dwukrotnie hello skojarzonych zasad. Kliknij prawym przyciskiem myszy chmury hello > **usuwanie skojarzenia**.
4. Usuń serwer VMM hello lub aktywny węzeł programu VMM. W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **serwery VMM**, kliknij prawym przyciskiem myszy serwer hello >  **Usuń**.
5. Odinstaluj hello dostawcy ręcznie na serwerze VMM hello. Jeśli masz klaster, Usuń z dowolnych węzłów.
6. Jeśli replikujesz tooAzure, Usuń ręcznie agenta usług odzyskiwania Microsoft hello z hostów funkcji Hyper-V w chmurach hello usunięte.



### <a name="unregister-an-unconnected-vmm-server"></a>Wyrejestruj odłączony serwer programu VMM

1. Zatrzymaj replikowanie maszyn wirtualnych w chmurach na powitania serwera VMM ma tooremove.
2. Usuń wszystkie używane przez chmury na serwerze VMM hello, które mają toodelete mapowania sieci. W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **mapowania sieci**, kliknij prawym przyciskiem myszy mapowania sieci hello >  **Usuń**.
3. Należy pamiętać, identyfikator hello powitania serwera VMM.
4. Usuń skojarzenia zasad replikacji z chmury na powitania serwera VMM ma tooremove.  W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** >  **zasady replikacji**, kliknij dwukrotnie hello skojarzonych zasad. Kliknij prawym przyciskiem myszy chmury hello > **usuwanie skojarzenia**.
5. Usuń serwer VMM hello lub aktywnego węzła. W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **serwery VMM**, kliknij prawym przyciskiem myszy serwer hello >  **Usuń**.
6. Pobierz i uruchom hello [skrypt czyszczący](http://aka.ms/asr-cleanup-script-vmm) na powitania serwera VMM. Otwórz program PowerShell z hello **Uruchom jako Administrator** opcji zasad wykonywania hello toochange hello zakresu domyślne (LocalMachine). W skrypcie hello Określ identyfikator hello powitania serwera VMM ma tooremove. skrypt Hello usuwa rejestrację i informacji o serwerze hello parowania w chmurze.
5. Uruchom skrypt czyszczący hello na innych serwerach VMM, które zawierają chmury, które są skojarzone z chmury na powitania serwera VMM ma tooremove.
6. Uruchom skrypt czyszczący hello na inne pasywnych węzłach klastra VMM, których powitalne zainstalowany dostawca.
7. Odinstaluj hello dostawcy ręcznie na serwerze VMM hello. Jeśli masz klaster, Usuń z dowolnych węzłów.
8. Jeśli użytkownik replikacji tooAzure, można usunąć agenta usług odzyskiwania Microsoft hello z hostów funkcji Hyper-V w chmurach hello usunięte.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Wyrejestruj hosta funkcji Hyper-V w lokacji funkcji Hyper-V

Hosty funkcji Hyper-V, które nie są zarządzane przez program VMM są zbierane w lokacji funkcji Hyper-V. Usuń hosta w lokacji funkcji Hyper-V w następujący sposób:

1. Wyłącz replikację dla maszyn wirtualnych funkcji Hyper-V znajdujących się na hoście hello.
2. Usuń skojarzenie zasad hello lokacji funkcji Hyper-V. W **infrastruktura usługi Site Recovery** > **dla Lokacje funkcji Hyper-V** >  **zasady replikacji**, kliknij dwukrotnie hello skojarzonych zasad. Kliknij prawym przyciskiem myszy witrynę hello > **usuwanie skojarzenia**.
3. Usuwanie hostów funkcji Hyper-V. W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **hosty funkcji Hyper-V**, kliknij prawym przyciskiem myszy serwer hello >  **Usuń**.
4. Usuń lokację hello funkcji Hyper-V, po wszystkie hosty zostały usunięte z niej. W **infrastruktura usługi Site Recovery** > **dla programu System Center VMM** > **Lokacje funkcji Hyper-V**, kliknij prawym przyciskiem myszy witrynę hello >  **Usuń**.
5. Uruchom hello następującego skryptu na każdym hoście funkcji Hyper-V, które zostało usunięte. skrypt Hello czyści ustawienia na serwerze hello i wyrejestrowuje je z magazynu hello.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>Wyłącz ochronę dla maszyny Wirtualnej VMware lub serwerów fizycznych

1. W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**.
2. W **Usuń maszyny**, wybierz jedną z następujących opcji:
    - **Wyłącz ochronę maszyny hello (zalecane)**. Użyj tego toostop opcji replikacji hello maszyny. Ustawienia odzyskiwania lokacji zostaną automatycznie wyczyszczone. Zobaczysz tę opcję w hello w następujących okolicznościach:
        - **Hello wirtualna woluminu został zmieniony**— podczas zmiany rozmiaru woluminu hello wirtualnych maszyny przechodzi w stan krytyczny. Wybierz tę ochronę toodisables opcji Zachowaj punkty odzyskiwania na platformie Azure. Po włączeniu ochrony dla maszyny hello ponownie dane hello hello zmiany rozmiaru woluminu zostaną przeniesione tooAzure.
        - **Ostatnio uruchomiono trybu failover**— po uruchomieniu tootest pracy awaryjnej środowisku, wybierz ten toostart opcji ochrony maszyn lokalnych ponownie. Wyłącza on funkcję każdej maszyny wirtualnej, a następnie potrzebna tooenable ochrona je ponownie. Wyłączenie maszyny hello tego ustawienia nie wpływa na powitania maszyny wirtualnej repliki na platformie Azure. Nie należy odinstalować usługi mobilności hello z komputera hello.
    - **Zatrzymywanie zarządzania hello maszyny**. Jeśli wybierzesz tę opcję, hello maszyny tylko zostaną usunięte z magazynu hello. Nie będzie mieć wpływ na ustawienia ochrony lokalne powitania maszyny. Ustawienia tooremove na komputerze hello i tooremove hello maszyny z hello subskrypcji platformy Azure, należy tooclean hello ustawień przez odinstalowanie hello usługi mobilności.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>Wyłącz ochronę dla maszyny Wirtualnej funkcji Hyper-V w chmurze VMM

1. W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**.
2. W **Usuń maszyny**, wybierz jedną z następujących opcji:

    - **Wyłącz ochronę maszyny hello (zalecane)**. Użyj tego toostop opcji replikacji hello maszyny. Ustawienia odzyskiwania lokacji zostaną automatycznie wyczyszczone.
    - **Zatrzymywanie zarządzania hello maszyny**. Jeśli wybierzesz tę opcję, hello maszyny tylko zostaną usunięte z magazynu hello. Nie będzie mieć wpływ na ustawienia ochrony lokalne powitania maszyny. Ustawienia tooremove na komputerze hello i tooremove hello maszyny z hello subskrypcji platformy Azure, należy tooclean hello ustawienia się ręcznie, przy użyciu instrukcji hello poniżej. Należy zwrócić uwagę, jeśli zostanie wybrana maszyna wirtualna hello toodelete i jej dyski twarde, zostanie usunięcia z hello lokalizacji docelowej.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>Wyczyść ustawienia ochrony — lokacja dodatkowa programu VMM tooa replikacji

W przypadku wybrania **zatrzymywanie zarządzania hello maszyny** i możesz replikowanie tooa lokacji dodatkowej, uruchom ten skrypt na powitania serwera podstawowego tooclean ustawienia hello hello głównej maszyny wirtualnej. W konsoli programu VMM powitania kliknij konsoli programu VMM PowerShell hello tooopen hello PowerShell przycisk. Zamień SQLVM1 hello nazwę maszyny wirtualnej.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Uruchom ten skrypt tooclean hello ustawień dla pomocniczej maszyny wirtualnej hello na powitania pomocniczy serwer programu VMM:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. Na powitania pomocniczy serwer programu VMM Odśwież hello maszyn wirtualnych na serwerze hosta funkcji Hyper-V hello, dzięki czemu hello dodatkowej maszyny Wirtualnej pobiera wykryte ponownie w konsoli programu VMM hello.
4. Wyczyść Hello powyżej kroki hello ustawienia replikacji na serwerze VMM hello. Jeśli chcesz, aby toostop replikacji dla maszyny wirtualnej hello, uruchom następujące skryptu Niestety hello hello głównych i dodatkowych maszyn wirtualnych. Zamień SQLVM1 hello nazwę maszyny wirtualnej.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>Wyczyść ustawienia ochrony - tooAzure replikacji

1. W przypadku wybrania **zatrzymywanie zarządzania hello maszyny** i replikowane tooAzure, uruchom ten skrypt na powitania źródłowy serwer VMM przy użyciu programu PowerShell z konsoli programu VMM hello.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Witaj powyżej kroki wyczyść hello ustawienia replikacji na serwerze VMM hello. Replikacja toostop hello maszynę wirtualną działającą na serwerze hosta funkcji Hyper-V hello, uruchom ten skrypt. Zamień SQLVM1 hello nazwę maszyny wirtualnej, a host01.contoso.com o nazwie powitania serwera hosta funkcji Hyper-V hello.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Wyłącz ochronę dla maszyny Wirtualnej funkcji Hyper-V w lokacji funkcji Hyper-V

Użyj tej procedury, Jeśli replikujesz tooAzure maszyn wirtualnych funkcji Hyper-V bez serwera VMM.

1. W **chronione elementy** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny > **usunąć**.
2. W **Usuń maszyny**, możesz wybrać hello następujące opcje:

   - **Wyłącz ochronę maszyny hello (zalecane)**. Użyj tego toostop opcji replikacji hello maszyny. Ustawienia odzyskiwania lokacji zostaną automatycznie wyczyszczone.
   - **Zatrzymywanie zarządzania hello maszyny**. Jeśli ta opcja jest zaznaczona maszyna hello tylko zostanie usunięta z magazynu hello. Nie będzie mieć wpływ na ustawienia ochrony lokalne powitania maszyny. Ustawienia tooremove na komputerze hello i tooremove hello maszyny wirtualnej na podstawie hello subskrypcji platformy Azure, należy ustawienia hello tooclean się ręcznie. W przypadku wybrania maszyny wirtualnej hello toodelete i jej dyski twarde zostaną one usunięte z lokalizacji docelowej hello.
3. W przypadku wybrania **zatrzymywanie zarządzania hello maszyny**, uruchom ten skrypt na serwerze hosta funkcji Hyper-V źródła hello, replikacja tooremove hello maszyny wirtualnej. Zamień SQLVM1 hello nazwę maszyny wirtualnej.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
