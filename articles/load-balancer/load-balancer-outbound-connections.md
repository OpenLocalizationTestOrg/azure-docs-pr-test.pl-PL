---
title: "Opis połączeń wychodzących na platformie Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak Azure umożliwia maszyny wirtualne do komunikowania się z publicznej usługi internetowe."
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
ms.openlocfilehash: 03cb14b5710b6dd17599a3c4eab21380c76c2b40
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Informacje o połączeniach wychodzących na platformie Azure

Maszyna wirtualna (VM) na platformie Azure mogą komunikować się z punktami końcowymi poza platformą Azure w publicznej przestrzeni adresów IP. Gdy maszyna wirtualna inicjuje przepływu wychodzącego do miejsca docelowego w publicznej przestrzeni adresów IP, Azure mapuje prywatnego adresu IP maszyny Wirtualnej do publicznego adresu IP i zezwala na ruch zwracany nawiązać połączenie z maszyną Wirtualną.

Platforma Azure udostępnia trzy różnych metod na osiągnięcie łączność wychodząca. Każda metoda ma swoją własną możliwości i ograniczeń. Przejrzyj każdej metody dokładnie, aby wybrać, które spełni wymagania organizacji.

| Scenariusz | Metoda | Uwaga |
| --- | --- | --- |
| Maszyna wirtualna autonomiczne (Brak usługi równoważenia obciążenia, żaden adres publiczny adres IP na poziomie wystąpienia) |Domyślne SNAT |Azure kojarzy publicznego adresu IP dla SNAT |
| Maszyna wirtualna z równoważeniem obciążenia (nie wystąpienia poziomu publicznego adresu IP na maszynie Wirtualnej) |SNAT przy użyciu usługi równoważenia obciążenia |Azure używa publicznego adresu IP usługi równoważenia obciążenia dla SNAT |
| Maszyna wirtualna o wystąpieniu poziomu publicznego adresu IP (z lub bez modułu równoważenia obciążenia) |SNAT nie jest używany. |Azure używa publicznego adresu IP, przypisane do maszyny Wirtualnej |

Jeśli nie chcesz, aby maszyny Wirtualnej do komunikowania się z punktami końcowymi poza platformą Azure w publicznej przestrzeni adresów IP, można użyć grup zabezpieczeń sieci (NSG) w celu zablokowania dostępu. Za pomocą grup NSG omówiono bardziej szczegółowo w [zapobieganie łączności publicznej w zakresie](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>Autonomiczny maszynę Wirtualną za pomocą żaden adres publiczny adres IP na poziomie wystąpienia

W tym scenariuszu maszyna wirtualna nie jest częścią puli usługi równoważenia obciążenia Azure i nie ma adresu wystąpienia poziomu publicznego adresu IP (ILPIP) przypisane do niej. Gdy maszyna wirtualna tworzy przepływu wychodzącego, Azure tłumaczy prywatnej źródłowy adres IP przepływu wychodzącego do źródłowego publicznego adresu IP. Publiczny adres IP używany dla tego przepływu ruchu wychodzącego nie można skonfigurować, nie będą uwzględniane względem subskrypcji publicznego adresu IP limit zasobów. Platforma Azure korzysta źródła sieci adresu tłumaczenia (SNAT) do tej funkcji. Porty efemeryczne publicznego adresu IP są używane do rozróżniania poszczególnych przepływów pochodzi przez maszynę Wirtualną. Podczas tworzenia przepływów SNAT dynamicznie przydziela porty efemeryczne. W tym kontekście tymczasowych portów używanych do SNAT są określane jako porty SNAT.

Porty SNAT są ograniczone zasób, który może być wyczerpany. Należy zrozumieć, jak są używane. Jeden port SNAT jest używany na przepływ do pojedynczego adresu IP. Każdy przepływ zajmują jednego portu SNAT wiele przepływów do tego samego adresu IP. Dzięki temu, że strumienie są unikatowe, jeśli pochodzi z tego samego publicznego adresu IP do tego samego adresu IP. Wiele przepływów, każdy z nich do innego adresu IP korzystać z jednego portu SNAT na docelowym. Docelowy adres IP zapewnia unikatowość przepływów.

Można użyć [analizy dzienników dla usługi równoważenia obciążenia](load-balancer-monitor-log.md) i [alertu dzienniki zdarzeń, aby monitorować SNAT portu wiadomości wyczerpania](load-balancer-monitor-log.md#alert-event-log). Gdy wyczerpania zasobów portu SNAT przepływów wychodzących niepowodzeniem, dopóki SNAT porty są wydawane przez przepływów. Moduł równoważenia obciążenia używa limit czasu bezczynności 4-minutowy odzyskiwanie SNAT portów.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>Równoważeniem obciążenia maszyny Wirtualnej z żaden adres publiczny adres IP na poziomie wystąpienia

W tym scenariuszu maszyna wirtualna jest częścią puli usługi równoważenia obciążenia Azure.  Maszyna wirtualna nie ma publicznego adresu IP przypisane do niej. Zasób usługi równoważenia obciążenia musi być skonfigurowany z regułą, aby połączyć publicznego frontonu IP z puli zaplecza.  Jeśli nie wykonasz tej konfiguracji, zachowanie jest zgodnie z opisem w sekcji powyżej dla [autonomiczny maszynę Wirtualną za pomocą wystąpienia poziomu publiczny adres IP nie](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Gdy maszyna wirtualna z równoważeniem obciążenia tworzy przepływu wychodzącego, Azure tłumaczy prywatnej źródłowy adres IP przepływu wychodzącego do publicznego adresu IP publiczny moduł równoważenia obciążenia serwera sieci Web. Platforma Azure korzysta źródła sieci adresu tłumaczenia (SNAT) do tej funkcji. Porty efemeryczne publicznego adresu IP usługi równoważenia obciążenia są używane do rozróżniania poszczególnych przepływów pochodzi przez maszynę Wirtualną. SNAT dynamicznie przydziela porty efemeryczne, podczas tworzenia przepływów wychodzących. W tym kontekście tymczasowych portów używanych do SNAT są określane jako porty SNAT.

Porty SNAT są ograniczone zasób, który może być wyczerpany. Należy zrozumieć, jak są używane. Jeden port SNAT jest używany na przepływ do pojedynczego adresu IP. Każdy przepływ zajmują jednego portu SNAT wiele przepływów do tego samego adresu IP. Dzięki temu, że strumienie są unikatowe, jeśli pochodzi z tego samego publicznego adresu IP do tego samego adresu IP. Wiele przepływów, każdy z nich do innego adresu IP korzystać z jednego portu SNAT na docelowym. Docelowy adres IP zapewnia unikatowość przepływów.

Można użyć [analizy dzienników dla usługi równoważenia obciążenia](load-balancer-monitor-log.md) i [alertu dzienniki zdarzeń, aby monitorować SNAT portu wiadomości wyczerpania](load-balancer-monitor-log.md#alert-event-log). Gdy wyczerpania zasobów portu SNAT przepływów wychodzących niepowodzeniem, dopóki SNAT porty są wydawane przez przepływów. Moduł równoważenia obciążenia używa limit czasu bezczynności 4-minutowy odzyskiwanie SNAT portów.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>Maszyna wirtualna o wystąpieniu poziomu publicznego adresu IP (z lub bez modułu równoważenia obciążenia)

W tym scenariuszu maszyna wirtualna ma wystąpienie poziomu publicznego adresu IP (ILPIP) przypisane do niej. Nie ma znaczenia, czy maszyna wirtualna jest równoważone, czy nie. W przypadku ILPIP źródła sieci adresu tłumaczenia (SNAT) nie jest używany. Maszyna wirtualna używa ILPIP dla wszystkich przepływów wychodzących. Jeśli wystąpią wyczerpania SNAT aplikacji inicjuje wiele przepływów wychodzących, należy rozważyć przypisywanie ILPIP, aby uniknąć SNAT ograniczenia.

## <a name="discovering-the-public-ip-used-by-a-given-vm"></a>Odnajdywanie publiczny adres IP używany przez danego maszyny Wirtualnej

Istnieje wiele sposobów, aby określić źródłowy publiczny adres IP połączeń wychodzących. OpenDNS zapewnia usługę, które mogą być prezentowane z publicznego adresu IP maszyny Wirtualnej. Używanie polecenia nslookup, możesz wysłać zapytanie DNS dla nazwy myip.opendns.com OpenDNS program rozpoznawania nazw. Usługa zwraca źródłowy adres IP użyty do wysłania zapytania. Podczas wykonywania następującego zapytania z maszyny Wirtualnej, odpowiedź jest publiczny adres IP używany dla tej maszyny Wirtualnej.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Zapobieganie łączności publicznej w zakresie

Czasami jest niepożądanych dla maszyny Wirtualnej, aby można było utworzyć przepływ wychodzący lub może być wymagane do zarządzania, które miejsc docelowych jest osiągalna z przepływów wychodzących. W takim przypadku należy użyć [grup zabezpieczeń sieci (NSG)](../virtual-network/virtual-networks-nsg.md) do zarządzania miejsc docelowych, które maszyna wirtualna może nawiązać połączenie. Po zastosowaniu grupy NSG z maszyną wirtualną z równoważeniem obciążenia, należy zwrócić uwagę na [domyślne znaczniki](../virtual-network/virtual-networks-nsg.md#default-tags) i [domyślne zasady](../virtual-network/virtual-networks-nsg.md#default-rules).

Należy się upewnić, czy maszyny Wirtualnej może odbierać żądań sondy kondycji z modułu równoważenia obciążenia Azure. Jeśli grupy NSG blokuje żądania sondy kondycji z AZURE_LOADBALANCER domyślny znacznik, sondy kondycji Twojej maszyny Wirtualnej nie powiedzie się i maszyny Wirtualnej jest oznaczony w dół. Moduł równoważenia obciążenia zatrzymuje wysyłanie nowych przepływów z tą maszyną Wirtualną.

## <a name="limitations"></a>Ograniczenia

Jeśli [wielu adresów IP (publicznymi) są skojarzone z modułem równoważenia obciążenia](load-balancer-multivip-overview.md), wszystkie te publicznego adresu IP, adresy są kandydatem do przepływów wychodzących.

Azure używa nieobsługiwanego algorytmu, aby określić liczbę dostępnych portów SNAT, zależnie od rozmiaru puli.  To nie konfiguruje się w tej chwili.

Należy koniecznie rememember, który liczbę dostępnych portów SNAT nie przekłada się bezpośrednio do liczby połączeń. Zobacz powyżej kątem specyfiki na kiedy i jak SNAT porty są przydzielane i jak zarządzać wyczerpującymi zasobem.
