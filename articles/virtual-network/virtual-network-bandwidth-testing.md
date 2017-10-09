---
title: "przepustowość sieci maszyny Wirtualnej Azure aaaTesting | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootest maszyny wirtualnej platformy Azure sieci przepływności."
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
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>Przepustowość/przepływność, testowanie (NTTTCP)

Podczas testowania przepustowość sieci na platformie Azure, jest najlepszym toouse narzędzie, które dotyczy sieci hello do testowania i minimalizuje użycie hello inne zasoby, które mogą wpłynąć na wydajność. NTTTCP jest zalecane.

Skopiuj tootwo narzędzie hello maszynach wirtualnych Azure hello sam rozmiar. Jedna maszyna wirtualna działa jako NADAWCĘ i hello innych jako ODBIORNIK.

#### <a name="deploying-vms-for-testing"></a>Wdrażanie maszyn wirtualnych na potrzeby testowania
Dla celów hello ten test Witaj dwie maszyny wirtualne powinny znajdować się na hello tej samej usługi w chmurze lub hello tego samego zestawu dostępności, dzięki czemu możemy użyć ich wewnętrznych adresów IP i wykluczyć hello usługi równoważenia obciążenia z hello testu. Jest możliwe tootest z hello VIP, ale tego rodzaju testowania jest poza zakresem hello tego dokumentu.
 
Zanotuj adres IP hello odbiorcy. Umożliwia wywołanie tego adresu IP "a.b.c.r"

Zanotuj hello liczba rdzeni na powitania maszyny Wirtualnej. Umożliwia to wywołanie "\#num\_rdzeni"
 
Uruchom hello NTTTCP testowania 300 sekund (czyli 5 minut) na powitania nadawcy maszyny Wirtualnej i odbiorcy maszyny Wirtualnej.

Porada: Podczas konfigurowania tego testu dla powitania po raz pierwszy, spróbuj krótszą opinii okresu tooget testu wcześniej. Po narzędzia hello działa zgodnie z oczekiwaniami, rozszerzanie hello testu okresu too300 sekund na powitania najdokładniejszych wyników.

> [!NOTE]
> nadawca Hello **i** odbiornika należy określić **hello sam** parametru czas trwania testu (-t).

tootest jednego strumienia TCP przez 10 sekund:

Odbiornik parametrów: - r ntttcp -t 10 - P 1

Nadawca parametry: ntttcp-s10.27.33.7 metoda "-t 10 - n" 1 -P 1

> [!NOTE]
> Hello poprzedzających próbki powinien mieć tylko tooconfirm używanej konfiguracji. Prawidłowe przykłady testów są uwzględnione w dalszej części tego dokumentu.

## <a name="testing-vms-running-windows"></a>Testowanie maszyn wirtualnych z systemem WINDOWS:

#### <a name="get-ntttcp-onto-hello-vms"></a>Pobierz NTTTCP na powitania maszyn wirtualnych.

Pobieranie najnowszej wersji hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Lub wyszukaj go w przypadku przeniesienia: <https://www.bing.com/search?q=ntttcp+download> \< — należy najpierw trafień

Należy rozważyć umieszczenie w oddzielnym folderze, takich jak c: NTTTCP\\narzędzia

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>Zezwalaj na NTTTCP przez zaporę systemu Windows hello
Na powitania ODBIORNIK należy utworzyć regułę zezwalającą na tooallow zapory systemu Windows hello NTTTCP tooarrive ruchu. Jest najprostszym tooallow hello cały NTTTCP według nazwy, a nie tooallow określone porty TCP ruchu przychodzącego.

Zezwalaj na ntttcp za pośrednictwem zapory systemu Windows hello, jak to:

netsh advfirewall zapory Dodawanie reguły programu =\<ścieżki\>\\ntttcp.exe nazwa = "ntttcp" protokołu żadnych dir = = w akcji = Zezwalaj enable = yes profile = ANY

Na przykład, jeśli został skopiowany ntttcp.exe toohello "c:\\narzędzia" folder, to polecenie hello: 

netsh advfirewall zapory Dodawanie reguły programu = c:\\narzędzia\\ntttcp.exe nazwa = "ntttcp" protokołu żadnych dir = = w akcji = Zezwalaj enable = yes profile = ANY

#### <a name="running-ntttcp-tests"></a>Uruchamianie testów NTTTCP

Uruchom NTTTCP na powitania ODBIORNIKA (**Uruchom w powłoce CMD z**, a nie z programu PowerShell):

ntttcp - r — m [2\*\#num\_rdzeni],\*, a.b.c.r -t 300

Jeśli hello maszyna wirtualna ma cztery rdzeni i adres IP 10.0.0.4, będzie wyglądać następująco:

ntttcp - r — m 8,\*, 10.0.0.4 -t 300


Uruchom NTTTCP na powitania nadawcy (**Uruchom w powłoce CMD z**, a nie z programu PowerShell):

ntttcp -s — m 8,\*, 10.0.0.4 -t 300 

Poczekaj na powitania wyników.


## <a name="testing-vms-running-linux"></a>Testowanie maszyn wirtualnych z systemem LINUX:

Użyj nttcp dla systemu linux. Jest ona dostępna z <https://github.com/Microsoft/ntttcp-for-linux>

Na powitania maszyn wirtualnych systemu Linux (NADAWCĄ i odbiorcą) uruchom następujące polecenia, aby przygotować ntttcp dla linux na maszyny wirtualne:

CentOS - Install Git:
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu - Install Git:
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
Wprowadź, a następnie zainstalować zarówno:
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

Co w przykładzie Windows hello przyjęto założenie, że adres IP ODBIORNIKA Linux hello jest 10.0.0.4

Uruchom NTTTCP dla systemu Linux na powitania ODBIORNIK:

``` bash
ntttcp -r -t 300
```

I na powitania nadawcy, uruchom:

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Podano testu długość wartości domyślne too60 sekund, jeśli nie parametru czasu

## <a name="testing-between-vms-running-windows-and-linux"></a>Testowanie między maszynami wirtualnymi z systemem Windows i LINUX:

W tym scenariuszy firma Microsoft włącza tryb niesynchronizowanej hello, więc można uruchomić testu hello. Jest to zrobić za pomocą hello **flagi -N** dla systemu Linux i **flagi -ns** dla systemu Windows.

#### <a name="from-linux-toowindows"></a>Z Linux tooWindows:

Odbiornik <Windows>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Nadawca <Linux> :

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>Z tooLinux systemu Windows:

Odbiornik <Linux>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Nadawca <Windows>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Następne kroki
* W zależności od wyników, może być miejsca zbyt[zoptymalizować maszyny przepustowość sieci](virtual-network-optimize-network-bandwidth.md) dla danego scenariusza.
* Dowiedz się więcej o [sieci wirtualnej platformy Azure — często zadawane pytania (FAQ)](virtual-networks-faq.md)
