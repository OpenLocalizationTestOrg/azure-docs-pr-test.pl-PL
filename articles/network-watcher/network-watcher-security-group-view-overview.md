---
title: Widok grupy toosecurity aaaIntroduction w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie hello możliwości widoku zabezpieczeń obserwatora sieciowego"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a>Widok grupy zabezpieczeń toonetwork wprowadzenie w obserwatora sieciowego Azure

Na poziomie podsieci lub na poziomie karty Sieciowej skojarzonych grup zabezpieczeń sieci. Skojarzone na poziomie podsieci, zastosowanie wystąpień maszyn wirtualnych hello tooall w hello podsieci. Widok grupy zabezpieczeń sieci zwraca wszystkie grupy NSG hello skonfigurowane i reguł, które są skojarzone na poziomie podsieci i karty na maszynie wirtualnej, zapewniając wgląd w konfiguracji hello. Ponadto zasady efektywnym elementem systemu zabezpieczeń hello są zwracane dla każdej z kart sieciowych hello na maszynie wirtualnej. Widok przy użyciu grup zabezpieczeń sieci można ocenić maszyny Wirtualnej dla luk w zabezpieczeniach sieci takich jak otwartych portów. Można również sprawdzić czy grupy zabezpieczeń sieci działa zgodnie z oczekiwaniami, na podstawie [porównanie hello skonfigurowane i hello reguły efektywnym elementem systemu zabezpieczeń](network-watcher-nsg-auditing-powershell.md).

Przypadek użycia dłuższy jest zabezpieczeń, zgodności i inspekcji. Przetestowanego zestaw reguł zabezpieczeń można zdefiniować jako model ładu zabezpieczeń w organizacji. Inspekcja okresowe zgodności można zaimplementować w sposób programowy porównując hello przetestowanego reguły z hello skuteczne reguły dla poszczególnych maszyn wirtualnych hello w sieci.

W hello portalu reguły są podzielone według obowiązującej, podsieci interfejsu sieciowego i domyślne. Zapewnia to prosty widok do maszyny wirtualnej tooa zasady stosowane hello. Przycisk Pobierz jest udostępniane tooeasily Pobierz wszystkie reguły zabezpieczeń hello bez względu na karcie hello w postaci pliku CSV.

![Widok grupy zabezpieczeń][1]

Zasady można wybrać i otwiera nowy blok hello tooshow prefiksy sieciowej grupy zabezpieczeń i źródłowym i docelowym. Z tego bloku można przejść bezpośrednio toohello zasób grupy zabezpieczeń sieci.

![Przechodzenie do szczegółów][2]

### <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooaudit zabezpieczenia sieci grupy ustawień, odwiedzając [ustawienia inspekcji sieciowej grupy zabezpieczeń przy użyciu programu PowerShell](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









