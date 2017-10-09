---
title: "przepustowość sieci VM aaaOptimize | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toooptimize maszyny wirtualnej platformy Azure sieci przepływności."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Zoptymalizować przepływność sieci maszyn wirtualnych platformy Azure

Maszyny wirtualne platformy Azure (VM) ma domyślne ustawienia sieci, które mogą być optymalizowane więcej przepustowości sieci. W tym artykule opisano, jak toooptimize sieci przepływności systemu Microsoft Azure Windows oraz maszyn wirtualnych systemu Linux, łącznie z głównych dystrybucje, takich jak Ubuntu i CentOS Red Hat.

## <a name="windows-vm"></a>Maszyna wirtualna z systemem Windows

Jeśli maszyna wirtualna systemu Windows jest obsługiwana z [przyspieszony sieci](virtual-network-create-vm-accelerated-networking.md), włączenie tej funkcji będzie hello optymalną konfigurację przepływności. Dla wszystkich innych maszyn wirtualnych systemu Windows przy użyciu skalowanie po stronie odbierającej (RSS) mogą skorzystać z wyższej przepustowości maksymalnej niż Maszynę wirtualną bez RSS. Funkcja RSS mogą być wyłączone domyślnie na maszynie wirtualnej systemu Windows. Zakończenie hello następujące kroki toodetermine, czy włączono funkcję RSS i tooenable go, jeśli jest wyłączone.

1. Wprowadź hello `Get-NetAdapterRss` toosee polecenia programu PowerShell, jeśli funkcja RSS jest włączone dla karty sieciowej. W hello następujące przykładowe dane wyjściowe zwrócone z hello `Get-NetAdapterRss`, funkcja RSS nie jest włączona.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Wprowadź następujące polecenie tooenable RSS hello:

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    poprzednie polecenie Hello nie ma danych wyjściowych. polecenie Hello zmienić ustawienia karty Sieciowej, powodując utracie połączenia tymczasowego około jednej minuty. Okno dialogowe Reconnecting pojawia się podczas hello utracie połączenia. Po próbie trzeci hello zwykle przywróceniu łączności.
3. Upewnij się, że funkcja RSS jest włączone w hello maszyny Wirtualnej, wprowadzając hello `Get-NetAdapterRss` polecenie ponownie. Jeśli to się powiedzie, jest zwracany hello następujące przykładowe dane wyjściowe:

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>Maszyny Wirtualnej systemu Linux

Funkcja RSS jest zawsze włączona domyślnie w maszynie Wirtualnej systemu Linux platformy Azure. Jądra systemu Linux wydane od stycznia 2017 r obejmują nowe opcje optymalizacji sieci, które umożliwiają wyższej przepustowości sieci maszyny Wirtualnej systemu Linux tooachieve.

### <a name="ubuntu"></a>Ubuntu

W kolejności tooget hello optymalizacji najpierw zaktualizować wersję toohello najnowsza wersja obsługiwana, począwszy od czerwca 2017, który jest:
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Po ukończeniu aktualizacji hello wprowadź następujące polecenia tooget hello najnowsze jądra hello:

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

Polecenie opcjonalne:

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Ubuntu Azure w wersji zapoznawczej jądra
> [!WARNING]
> Ta wersja zapoznawcza Linux Azure jądra nie może mieć hello sam poziom dostępności i niezawodności jako obrazy Marketplace i jądra, które są zwykle wersji dostępności. Funkcja Hello nie jest obsługiwane, mogą mieć ograniczone możliwości i nie może być tak niezawodna jak hello domyślnego jądra. Nie należy używać tego jądra dla obciążeń produkcyjnych.

Instalując hello proponowane jądra systemu Linux platformy Azure można osiągnąć znaczne przepustowość. tootry to jądra, Dodaj ten too/etc/apt/sources.list wiersza

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Następnie uruchom następujące polecenia, jako element główny.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

W kolejności tooget hello optymalizacji najpierw zaktualizuj wersję toohello najnowsza wersja obsługiwana, począwszy od 2017 lipca, który jest:
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Po ukończeniu aktualizacji hello instalacji hello usług najnowsze integracji systemu Linux (LIS).
optymalizacji przepływności Hello jest LIS, zaczynając od 4.2.2-2. Wprowadź następujące polecenia tooinstall LIS hello:

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

W kolejności tooget hello optymalizacji najpierw zaktualizuj wersję toohello najnowsza wersja obsługiwana, począwszy od 2017 lipca, który jest:
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Po ukończeniu aktualizacji hello instalacji hello usług najnowsze integracji systemu Linux (LIS).
optymalizacji przepływności Hello jest LIS, zaczynając od 4.2. Wprowadź następujące polecenia toodownload hello i instalowania usług LIS:

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Dowiedz się więcej o Linux Integration Services wersji 4.2 dla funkcji Hyper-V, wyświetlając hello [stronę pobierania](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Następne kroki
* Teraz, gdy hello maszyny Wirtualnej jest optymalizowane, zobacz wynik hello [przepustowości/przepływność, testowanie maszyny Wirtualnej Azure](virtual-network-bandwidth-testing.md) dla danego scenariusza.
* Dowiedz się więcej o [sieci wirtualnej platformy Azure — często zadawane pytania (FAQ)](virtual-networks-faq.md)
