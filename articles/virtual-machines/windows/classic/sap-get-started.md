---
title: aaaUsing SAP na maszynach wirtualnych z systemem Windows | Dokumentacja firmy Microsoft
description: "Wyczyść o korzystaniu z programu SAP na maszynach wirtualnych systemu Windows (VM) w systemie Microsoft Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>W przypadku maszyn wirtualnych systemu Windows na platformie Azure przy użyciu SAP
Chmura obliczeniowa terminem powszechnie używane, który jest uzyskanie coraz więcej znaczenia w ramach hello branży IT z małych firm się toolarge i wielonarodowych firmy. Microsoft Azure to hello platformy usług w chmurze firmy Microsoft, która oferuje szeroką gamę nowe możliwości. Teraz klienci są toorapidly może udostępnić i usuwanie aplikacji jako usługi w chmurze, więc nie są ograniczone tootechnical lub ograniczeń budżetowych. Zamiast inwestowanie czas i pieniądze na infrastrukturę sprzętu, firmy mogą skupić się na aplikacji hello, procesy biznesowe i korzyści dla klientów i użytkowników.

Maszynom wirtualnym Microsoft Azure firma Microsoft oferuje kompleksowe infrastruktura jako usługa (IaaS) platformy. Aplikacje oparte na oprogramowaniu SAP NetWeaver są obsługiwane w usłudze Azure Virtual Machines (IaaS). oficjalne dokumenty Hello poniżej opisano, jak tooplan i wdrożenia SAP NetWeaver aplikacji opartych na maszynach wirtualnych systemu Windows na platformie Azure. Można też wdrożyć aplikacje SAP NetWeaver oparte na [maszyn wirtualnych systemu Linux](../../linux/classic/sap-get-started.md).

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>SAP NetWeaver na platformie Azure - HA
title: aaaSAP NetWeaver na platformie Azure - SAP ASCS/SCS wystąpień klastrowania przy użyciu klastra trybu Failover systemu Windows Server na platformie Azure za pomocą SIOS DataKeeper

Podsumowanie: "w tym dokumencie opisano sposób tooset SIOS DataKeeper toouse konfiguracji SAP ASCS/SCS wysokiej dostępności na platformie Azure. SAP chroni ich pojedynczego punktu awarii składników, takich jak SAP ASCS/SCS lub umieścić w kolejce replikacji usługi z konfiguracji klastra trybu Failover systemu Windows Server, które wymagają udostępnione dyski. Te składniki SAP są istotne dla funkcji hello systemu SAP. W związku z tym musi funkcji wysokiej dostępności toobe umieścić w umieścić toomake się, że te składniki może wytrzymać awarii serwera lub maszyny Wirtualnej jako odbywa się za pomocą konfiguracji klastra systemu Windows bez systemu operacyjnego i w środowiskach funkcji Hyper-V. Począwszy od sierpnia 2015 Azure na sama nie udostępnia udostępnione dyski, które będą wymagane dla systemu Windows hello na podstawie konfiguracji wysokiej dostępności, wymagane dla tych krytycznych składników SAP. Jednak za pomocą hello produktu hello DataKeeper przez SIOS, konfiguracje klastra pracy awaryjnej systemu Windows Server, w razie potrzeby dla SAP ASCS/SCS mogą być tworzone na platformie Azure IaaS hello. W tym dokumencie opisano w podejściu krok do kroku, jak tooinstall konfiguracji klastra trybu Failover systemu Windows Server z udostępnionego dysku podał Datakeeper SIOS na platformie Azure. po stronie Azure, Windows i SAP hello, które działają w optymalny sposób konfiguracji wysokiej dostępności hello papieru Hello objaśnia szczegółów w konfiguracji. Hello papieru uzupełnia hello SAP instalacji dokumentacji i notatki SAP, reprezentujące hello głównej zasobów dla instalacji i wdrożenia oprogramowania SAP na podane platform.

Zaktualizowano: Sierpień 2015

[Pobierz teraz ten przewodnik](http://go.microsoft.com/fwlink/?LinkId=613056)

