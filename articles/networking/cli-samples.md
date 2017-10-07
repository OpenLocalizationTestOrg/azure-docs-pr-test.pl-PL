---
title: "aaaAzure przykłady interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Przykłady Azure CLI"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a>Przykładów dla interfejsu wiersza polecenia platformy Azure do obsługi sieci

Witaj Poniższa tabela zawiera linki toobash skrypty utworzone przy użyciu interfejsu wiersza polecenia Azure hello.

| | |
|-|-|
|**Łączność między zasobami Azure**||
| [Tworzenie sieci wirtualnej dla aplikacji wielowarstwowych](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Tworzy sieć wirtualną z podsieci frontonu i zaplecza. Podsieci frontonu toohello ruchu jest ograniczony tooHTTP i SSH, podczas toohello ruchu podsieci wewnętrznej jest ograniczona tooMySQL, port 3306. |
| [Dwie wirtualne sieci równorzędne](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Tworzy i łączy dwie sieci wirtualne w hello tego samego regionu. |
| [Kierować ruchem przez urządzenie wirtualne sieci](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Tworzy sieć wirtualną z podsieci frontonu i zaplecza i maszynę Wirtualną, która jest możliwe tooroute ruch między podsieciami hello dwa. |
| [Filtrowanie ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Tworzy sieć wirtualną z podsieci frontonu i zaplecza. Ruchu przychodzącego ruchu sieciowego podsieci frontonu toohello jest ograniczona tooHTTP, HTTPS i SSH. Ruch wychodzący toohello Internet z podsieci wewnętrznej hello jest niedozwolone. |
|**Kierunek ruchu i równoważenia obciążenia**||
| [Ładowanie równowagi ruchu tooVMs wysokiej dostępności](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Tworzy kilka maszyny wirtualne o wysokiej dostępności i konfiguracji równoważenia obciążenia. |
| [Wiele witryn sieci Web na maszynach wirtualnych Równoważenie obciążenia](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Tworzy dwie maszyny wirtualne z wielu konfiguracji adresów IP, połączone tooan Azure zestawu dostępności, dostępny za pośrednictwem usługi równoważenia obciążenia Azure. |
| [Bezpośrednie ruchu w różnych regionach aplikacji wysokiej dostępności](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  Tworzy dwa planów usługi aplikacji, dwie aplikacje sieci web profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu. |
| | |
