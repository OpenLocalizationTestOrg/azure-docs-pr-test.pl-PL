---
title: tooa pulpitu aaaRemote maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall i konfigurowanie pulpitu zdalnego tooconnect tooa maszyny Wirtualnej systemu Linux Azure firmy Microsoft dla hello klasycznego modelu wdrożenia"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a>Przy użyciu pulpitu zdalnego tooconnect tooa maszyny Wirtualnej systemu Linux programu Microsoft Azure
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Witaj zaktualizowanej wersji Menedżera zasobów w tym artykule, można znaleźć [tutaj](../use-remote-desktop.md).

## <a name="overview"></a>Omówienie
RDP (Remote Desktop Protocol) jest zastrzeżonym protokołem używane dla systemu Windows. Jak możemy użyć tooa tooconnect RDP maszyny Wirtualnej systemu Linux (maszyna wirtualna) zdalnie?

W tych wskazówkach zapewni hello odpowiedzi! Ułatwi to xrdp tooinstall i konfiguracji na programu Microsoft Azure maszyny Wirtualnej systemu Linux, które umożliwia nawiązanie połączenia tooit przy użyciu pulpitu zdalnego na komputerze z systemem Windows. Używamy systemem Ubuntu lub OpenSUSE jako przykład Witaj w tych wskazówkach maszyny Wirtualnej systemu Linux.

Narzędzie xrdp Hello jest typu open source, serwer protokołu RDP, któremu tooconnect serwera systemu Linux przy użyciu pulpitu zdalnego na komputerze z systemem Windows. RDP ma lepszą wydajność niż VNC (wirtualnych sieci przetwarzania danych). VNC renderuje przy użyciu grafiki jakość JPEG i może działać powoli, protokołu RDP jest szybkie i krystalicznie czyste.

> [!NOTE]
> Musi już mieć maszyny Wirtualnej platformy Microsoft Azure systemem Linux. toocreate i skonfiguruj Maszynę wirtualną systemu Linux, zobacz hello [samouczek maszyny Wirtualnej systemu Linux Azure](createportal.md).
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a>Tworzenie punktu końcowego dla pulpitu zdalnego
Używamy hello domyślny punkt końcowy 3389 dla pulpitu zdalnego w tym dokumencie. Konfigurowanie 3389 punktu końcowego jako `Remote Desktop` tooyour maszyny Wirtualnej systemu Linux, takich jak poniżej:

![Obraz](./media/remote-desktop/endpoint-for-linux-server.png)

Jeśli nie znasz tooset się punkt końcowy dla maszyny Wirtualnej, zobacz temat [w tych wskazówkach](setup-endpoints.md).

## <a name="install-gnome-desktop"></a>Zainstaluj Gnome pulpitu
Połącz tooyour maszyny Wirtualnej systemu Linux za pomocą `putty`i zainstaluj `Gnome Desktop`.

Ubuntu użyć:

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


Dla OpenSUSE użyj polecenia:

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a>Zainstaluj xrdp
Ubuntu użyć:

    #sudo apt-get install xrdp

Dla OpenSUSE użyj polecenia:

> [!NOTE]
> Zaktualizuj wersję OpenSUSE hello wersją hello używanego w hello następujące polecenia. w poniższym przykładzie Hello jest przeznaczony dla `OpenSUSE 13.2`.
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a>Uruchom xrdp i skonfiguruj xdrp w górę rozruchu
Dla OpenSUSE użyj polecenia:

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

Dla Ubuntu, zostanie rozpoczęta xrdp i eanbled w górę rozruchu automatycznie po zakończeniu instalacji.

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a>Przy użyciu xfce, jeśli używasz wersji Ubuntu później niż Ubuntu 12.04LTS
Ponieważ bieżąca wersja xrdp hello nie obsługuje Gnome pulpitu dla wersji Ubuntu później niż Ubuntu 12.04LTS, będziemy używać `xfce` pulpitu zamiast tego.

tooinstall `xfce`, użyj tego polecenia:

    #sudo apt-get install xubuntu-desktop

Następnie Włącz `xfce` za pomocą tego polecenia:

    #echo xfce4-session >~/.xsession

Edytuj plik konfiguracji hello `/etc/xrdp/startwm.sh`:

    #sudo vi /etc/xrdp/startwm.sh   

Dodaj wiersz hello `xfce4-session` przed wierszem hello `/etc/X11/Xsession`.

toorestart hello xrdp usługi, użyj tego:

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a>Połączenie z maszyną Wirtualną systemu Linux z komputera z systemem Windows
Na maszynie z systemem Windows uruchom klienta pulpitu zdalnego hello i wprowadź nazwę DNS maszyny Wirtualnej systemu Linux. Lub przejdź toohello pulpitu nawigacyjnego w portalu Azure hello maszyny wirtualnej i kliknij polecenie `Connect` tooconnect maszyny Wirtualnej systemu Linux. W takim przypadku zostaną wyświetlone powitalne okno logowania:

![Obraz](./media/remote-desktop/no2.png)

Zaloguj się za pomocą hello nazwy użytkownika i hasła maszyny wirtualnej systemu Linux.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat używania xrdp, zobacz [http://www.xrdp.org/](http://www.xrdp.org/).
