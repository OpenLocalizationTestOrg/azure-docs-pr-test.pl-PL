---
title: "aaaUnderstanding połączeń wychodzących na platformie Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak Azure umożliwia toocommunicate maszyn wirtualnych z publicznej usługi internetowe."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Informacje o połączeniach wychodzących na platformie Azure

Maszyna wirtualna (VM) na platformie Azure mogą komunikować się z punktami końcowymi poza platformą Azure w publicznej przestrzeni adresów IP. Gdy maszyna wirtualna inicjuje docelowego tooa przepływu ruchu wychodzącego w publicznej przestrzeni adresów IP, Azure mapuje hello wirtualna prywatnego adresu IP adres tooa publicznego adresu IP i umożliwia hello tooreach zwracany ruch maszyny Wirtualnej.

Platforma Azure udostępnia trzy różne metody tooachieve łączność wychodząca. Każda metoda ma swoją własną możliwości i ograniczeń. Należy dokładnie przejrzeć każdej metody toochoose, która odpowiada Twoim potrzebom.

| Scenariusz | Metoda | Uwaga |
| --- | --- | --- |
| Maszyna wirtualna autonomiczne (Brak usługi równoważenia obciążenia, żaden adres publiczny adres IP na poziomie wystąpienia) |Domyślne SNAT |Azure kojarzy publicznego adresu IP dla SNAT |
| Maszyna wirtualna z równoważeniem obciążenia (nie wystąpienia poziomu publicznego adresu IP na maszynie Wirtualnej) |Przy użyciu usługi równoważenia obciążenia hello SNAT |Azure używa publicznego adresu IP usługi równoważenia obciążenia hello SNAT |
| Maszyna wirtualna o wystąpieniu poziomu publicznego adresu IP (z lub bez modułu równoważenia obciążenia) |SNAT nie jest używany. |Azure używa publicznego adresu IP hello przypisane toohello maszyny Wirtualnej |

Jeśli nie chcesz, aby toocommunicate maszyny Wirtualnej z punktami końcowymi poza platformą Azure w publicznej przestrzeni adresów IP, można użyć grup zabezpieczeń sieci (NSG) tooblock dostępu. Za pomocą grup NSG omówiono bardziej szczegółowo w [zapobieganie łączności publicznej w zakresie](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>Autonomiczny maszynę Wirtualną za pomocą żaden adres publiczny adres IP na poziomie wystąpienia

W tym scenariuszu hello maszyny Wirtualnej nie jest częścią puli usługi równoważenia obciążenia Azure i nie ma przypisanego tooit adresu wystąpienia poziomu publicznego adresu IP (ILPIP). Gdy hello wirtualna tworzy przepływu wychodzącego, Azure tłumaczy hello prywatnej źródłowy adres IP hello przepływu wychodzącego tooa publicznego źródłowego adresu IP. Hello publiczny adres IP używany dla tego przepływu ruchu wychodzącego nie można skonfigurować, nie będą uwzględniane względem subskrypcji hello publicznego adresu IP limit zasobów. Platforma Azure korzysta tooperform źródła sieci adresu tłumaczenia (SNAT) tej funkcji. Porty efemeryczne hello publicznego adresu IP są używane toodistinguish przepływów poszczególnych zainicjowany przez hello maszyny Wirtualnej. Podczas tworzenia przepływów SNAT dynamicznie przydziela porty efemeryczne. W tym kontekście hello porty efemeryczne używane na potrzeby SNAT są porty SNAT tooas określony.

Porty SNAT są ograniczone zasób, który może być wyczerpany. Jest ważne toounderstand, sposobie ich używania. Jeden port SNAT jest używany na przepływ tooa pojedynczego adresu IP. Dla wielu przepływów toohello jednego portu SNAT korzysta z tego samego adresu IP, każdego przepływu. Dzięki temu przepływów hello są unikatowe gdy pochodzi z hello sam publicznego toohello adres IP tego samego adresu IP. Wiele przepływów każdy inny docelowy adres IP tooa korzystać z jednego portu SNAT na docelowy. docelowy adres IP Hello zapewnia unikatowość hello przepływów.

Można użyć [analizy dzienników dla usługi równoważenia obciążenia](load-balancer-monitor-log.md) i [toomonitor alertu dzienniki zdarzeń komunikatów wyczerpania portu SNAT](load-balancer-monitor-log.md#alert-event-log). Gdy wyczerpania zasobów portu SNAT przepływów wychodzących niepowodzeniem, dopóki SNAT porty są wydawane przez przepływów. Moduł równoważenia obciążenia używa limit czasu bezczynności 4-minutowy odzyskiwanie SNAT portów.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>Równoważeniem obciążenia maszyny Wirtualnej z żaden adres publiczny adres IP na poziomie wystąpienia

W tym scenariuszu hello maszyna wirtualna jest częścią puli usługi równoważenia obciążenia Azure.  Witaj maszyny Wirtualnej nie ma publiczny adres IP przypisany tooit. Witaj zasobów usługi równoważenia obciążenia musi być skonfigurowany z reguły toolink hello publicznego adresu IP frontonu hello puli wewnętrznej bazy danych.  Jeśli nie wykonasz tej konfiguracji, zachowanie hello jest zgodnie z opisem w sekcji hello powyżej dla [autonomiczny maszynę Wirtualną za pomocą wystąpienia poziomu publiczny adres IP nie](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Gdy hello maszyn wirtualnych z równoważeniem obciążenia tworzy przepływu wychodzącego, Azure tłumaczy hello prywatnej źródłowy adres IP hello przepływu wychodzącego toohello publicznego adresu IP hello publiczny moduł równoważenia obciążenia frontonu. Platforma Azure korzysta tooperform źródła sieci adresu tłumaczenia (SNAT) tej funkcji. Porty efemeryczne równoważenia obciążenia hello publicznego adresu IP są używane toodistinguish przepływów poszczególnych zainicjowany przez hello maszyny Wirtualnej. SNAT dynamicznie przydziela porty efemeryczne, podczas tworzenia przepływów wychodzących. W tym kontekście hello porty efemeryczne używane na potrzeby SNAT są porty SNAT tooas określony.

Porty SNAT są ograniczone zasób, który może być wyczerpany. Jest ważne toounderstand, sposobie ich używania. Jeden port SNAT jest używany na przepływ tooa pojedynczego adresu IP. Dla wielu przepływów toohello jednego portu SNAT korzysta z tego samego adresu IP, każdego przepływu. Dzięki temu przepływów hello są unikatowe gdy pochodzi z hello sam publicznego toohello adres IP tego samego adresu IP. Wiele przepływów każdy inny docelowy adres IP tooa korzystać z jednego portu SNAT na docelowy. docelowy adres IP Hello zapewnia unikatowość hello przepływów.

Można użyć [analizy dzienników dla usługi równoważenia obciążenia](load-balancer-monitor-log.md) i [toomonitor alertu dzienniki zdarzeń komunikatów wyczerpania portu SNAT](load-balancer-monitor-log.md#alert-event-log). Gdy wyczerpania zasobów portu SNAT przepływów wychodzących niepowodzeniem, dopóki SNAT porty są wydawane przez przepływów. Moduł równoważenia obciążenia używa limit czasu bezczynności 4-minutowy odzyskiwanie SNAT portów.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>Maszyna wirtualna o wystąpieniu poziomu publicznego adresu IP (z lub bez modułu równoważenia obciążenia)

W tym scenariuszu hello maszyna wirtualna ma wystąpienie poziomu publicznego adresu IP (ILPIP) przypisany tooit. Nie ma znaczenia, czy hello maszyny Wirtualnej jest równoważone, czy nie. W przypadku ILPIP źródła sieci adresu tłumaczenia (SNAT) nie jest używany. Witaj maszyna wirtualna używa hello ILPIP dla wszystkich przepływów wychodzących. Jeśli wystąpią wyczerpania SNAT aplikacji inicjuje wiele przepływów wychodzących, należy rozważyć przypisywanie tooavoid ILPIP SNAT ograniczenia.

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>Odnajdujący hello publiczny adres IP używany przez danego maszyny Wirtualnej

Istnieje wiele sposobów toodetermine hello publicznego źródłowy adres IP połączenia wychodzącego. OpenDNS udostępnia usługi, które mogą być prezentowane hello publicznego adresu IP maszyny Wirtualnej. Używanie polecenia nslookup hello, możesz wysłać zapytanie DNS dla hello nazwa myip.opendns.com toohello OpenDNS programu rozpoznawania nazw. Usługa Hello zwraca hello źródłowy adres IP, który był używany toosend hello zapytania. Podczas wykonywania hello następującego zapytania z maszyny Wirtualnej, odpowiedź hello jest powitalne publiczny adres IP używany dla tej maszyny Wirtualnej.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Zapobieganie łączności publicznej w zakresie

Czasami jest niepożądanych toobe maszyn wirtualnych dozwolona toocreate przepływu wychodzącego lub może być toomanage wymagania, które miejsc docelowych jest osiągalna z przepływów wychodzących. W takim przypadku należy użyć [grup zabezpieczeń sieci (NSG)](../virtual-network/virtual-networks-nsg.md) toomanage hello miejsc docelowych hello, że maszyna wirtualna może nawiązać połączenie. Kiedy stosować grupy NSG tooa równoważeniem obciążenia maszyny Wirtualnej, należy toohello uwagi toopay [domyślne znaczniki](../virtual-network/virtual-networks-nsg.md#default-tags) i [domyślne zasady](../virtual-network/virtual-networks-nsg.md#default-rules).

Należy zapewnić, że hello maszyny Wirtualnej może odbierać żądań sondy kondycji z modułu równoważenia obciążenia Azure. Jeśli grupa NSG bloki kondycji żądaniami badań z hello AZURE_LOADBALANCER domyślny znacznik, sondy kondycji Twojej maszyny Wirtualnej nie powiedzie się i hello maszyny Wirtualnej jest oznaczony w dół. Moduł równoważenia obciążenia zatrzymuje wysyłanie toothat przepływów nowej maszyny Wirtualnej.

## <a name="limitations"></a>Ograniczenia

Jeśli [wielu adresów IP (publicznymi) są skojarzone z modułem równoważenia obciążenia](load-balancer-multivip-overview.md), wszystkie te publicznego adresu IP, adresy są kandydatem do przepływów wychodzących.

Azure używa algorytmu toodetermine hello liczbę dostępnych portów SNAT na podstawie rozmiaru hello hello puli.  To nie konfiguruje się w tej chwili.

Jest ważne toorememember, który hello liczbę dostępnych portów SNAT nie przekłada się bezpośrednio toonumber połączeń. Zobacz powyżej kątem specyfiki i w jaki sposób SNAT porty są przydzielane sposobu i sytuacji toomanage wyczerpującymi zasobu.
