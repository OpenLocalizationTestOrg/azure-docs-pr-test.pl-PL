---
title: "wyników testu porównawczego aaaCompute dla maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft"
description: "Porównaj wyniki testu porównawczego obliczeń CoreMark dla maszyn wirtualnych Azure systemem Linux"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 93e812c1-79dd-40c5-b97b-aa79f5cd7d76
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cynthn
ms.openlocfilehash: b2c1ca5fbd80cea030ac2cc22156c4e9444c6726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="compute-benchmark-scores-for-linux-vms"></a>Obliczenia bazy danych wyników testów porównawczych dla maszyn wirtualnych systemu Linux
powitania po Pokaż wyniki testów porównawczych CoreMark obliczeniowe wydajności dla zestawienia maszyny Wirtualnej platformy Azure wysokiej wydajności z systemem Ubuntu. Wyniki testu porównawczego obliczeniowe są także dostępne dla [maszyn wirtualnych systemu Windows](../windows/compute-benchmark-scores.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="a-series---compute-intensive"></a>A-series obliczeniowych
| Rozmiar | Vcpu | Węzły NUMA | Procesor CPU | Uruchamia | Iteracje na sekundę | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8 |8 |1 |Procesor Intel Xeon E5 procesora CPU — 2670 0 @ 2.6 GHz |179 |110,294 |554 |
| Standard_A9 |16 |2 |Procesor Intel Xeon E5 procesora CPU — 2670 0 @ 2.6 GHz |189 |210,816 |2,126 |
| Standardowa_A10 |8 |1 |Procesor Intel Xeon E5 procesora CPU — 2670 0 @ 2.6 GHz |188 |110,025 |1,045 |
| Standardowa_A11 |16 |2 |Procesor Intel Xeon E5 procesora CPU — 2670 0 @ 2.6 GHz |188 |210,727 |2,073 |

## <a name="dv2-series"></a>Seria Dv2
| Rozmiar | Vcpu | Węzły NUMA | Procesor CPU | Uruchamia | Iteracje na sekundę | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standardowa_D1_v2 |1 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |140 |14,852 |780 |
| Standardowa_D2_v2 |2 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |133 |29,467 |1,863 |
| Standardowa_D3_v2 |4 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |139 |56,205 |1,167 |
| Standardowa_D4_v2 |8 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |126 |108,543 |3,446 |
| Standardowa_D5_v2 |16 |2 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |126 |205,332 |9,998 |
| Standardowa_D11_v2 |2 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |125 |28,598 |1,510 |
| Standardowa_D12_v2 |4 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |131 |55,673 |1,418 |
| Standardowa_D13_v2 |8 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |140 |107,986 |3,089 |
| Standardowa_D14_v2 |16 |2 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |140 |208,186 |8,839 |
| Standard_D15_v2 |20 |2 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |28 |268,560 |4,667 |

## <a name="f-series"></a>Seria F
| Rozmiar | Vcpu | Węzły NUMA | Procesor CPU | Uruchamia | Iteracje na sekundę | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standardowa_F1 |1 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |154 |15,602 |787 |
| Standardowa_F2 |2 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |126 |29,519 |1,233 |
| Standardowa_F4 |4 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |147 |58,709 |1,227 |
| Standardowa_F8 |8 |1 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |224 |112,772 |3,006 |
| Standardowa_F16 |16 |2 |Procesor Intel Xeon E5-2673 v3 @ 2,4 GHz |42 |218,571 |5,113 |

## <a name="g-series"></a>Seria G
| Rozmiar | Vcpu | Węzły NUMA | Procesor CPU | Uruchamia | Iteracje na sekundę | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standardowa_G1 |2 |1 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |83 |31,310 |2,891 |
| Standardowa_G2 |4 |1 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |84 |60,112 |3,537 |
| Standardowa_G3 |8 |1 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |84 |107,522 |4,537 |
| Standardowa_G4 |16 |1 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |83 |195,116 |5,024 |
| Standard_G5 |32 |2 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |84 |360,329 |14,212 |

## <a name="gs-series"></a>Seria GS
| Rozmiar | Vcpu | Węzły NUMA | Procesor CPU | Uruchamia | Iteracje na sekundę | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standardowa_GS1 |2 |1 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |84 |28,613 |1,884 |
| Standardowa_GS2 |4 |1 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |83 |54,348 |3,474 |
| Standardowa_GS3 |8 |1 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |83 |104,564 |1,834 |
| Standardowa_GS4 |16 |1 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |84 |194,111 |4,735 |
| Standard_GS5 |32 |2 |Procesor Intel Xeon E5-2698B v3 @ 2 GHz |84 |357,396 |16,228 |

## <a name="h-series"></a>Seria H
| Rozmiar | Vcpu | Węzły NUMA | Procesor CPU | Uruchamia | Iteracje na sekundę | StdDev |
| --- | --- | --- | --- | --- | --- | --- |
| Standardowa_H8 |8 |1 |Procesor Intel Xeon E5-2667 v3 @ 3,2 GHz |28 |140,782 |2,512 |
| Standardowa_H16 |16 |2 |Procesor Intel Xeon E5-2667 v3 @ 3,2 GHz |35 |275,289 |7,110 |
| Standard_H18m |8 |1 |Procesor Intel Xeon E5-2667 v3 @ 3,2 GHz |28 |139,071 |3,988 |
| Standardowa_H16m |16 |2 |Procesor Intel Xeon E5-2667 v3 @ 3,2 GHz |28 |275,988 |6,963 |
| Warstwie standardowa_h16r |16 |2 |Procesor Intel Xeon E5-2667 v3 @ 3,2 GHz |28 |273,982 |6,069 |
| Warstwie standardowa_h16mr |16 |2 |Procesor Intel Xeon E5-2667 v3 @ 3,2 GHz |28 |274,523 |5,698 |

## <a name="about-coremark"></a>O CoreMark
Numery Linux zostały obliczone, uruchamiając [CoreMark](http://www.eembc.org/coremark/faq.php) na Ubuntu. CoreMark został skonfigurowany z hello liczba wątków zestaw toohello liczba procesorów wirtualnych i tooPThreads Ustaw współbieżności. docelowy Hello liczba iteracji została dostosowana oparte na tooprovide obniżenie wydajności środowiska wykonawczego co najmniej 20 sekund (zwykle znacznie dłużej). końcowy wynik Hello reprezentuje hello liczby iteracji ukończone rozdzielonych hello liczbę sekund, jaki zajęło toorun hello testu. Każdy test zostało uruchomione co najmniej siedmiu razy na każdej maszynie Wirtualnej. Testy (z wyjątkiem dla H series_ zostały uruchomione października 2015 wiele maszyn wirtualnych w każdej maszyny Wirtualnej jest obsługiwana w dniu hello Uruchom powitalne publiczny region platformy Azure.

## <a name="next-steps"></a>Następne kroki
* Pojemność, dysku szczegóły i dodatkowe uwagi dotyczące wybierania rozmiarów maszyn wirtualnych, zobacz [rozmiary maszyn wirtualnych](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* skrypty CoreMark hello toorun na maszynach wirtualnych systemu Linux, Pobierz hello [CoreMark pakiet skryptu](http://download.microsoft.com/download/3/0/5/305A3707-4D3A-4599-9670-AAEB423B4663/AzureCoreMarkScriptPack.zip).

