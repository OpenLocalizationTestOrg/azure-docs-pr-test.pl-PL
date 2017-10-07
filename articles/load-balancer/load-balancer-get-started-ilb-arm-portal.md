---
title: "aaaCreate wewnętrznego modułu równoważenia obciążenia - portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate wewnętrznego modułu równoważenia w Menedżerze zasobów przy użyciu portalu Azure hello obciążenia"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a>Utworzyć wewnętrznego modułu równoważenia obciążenia w hello portalu Azure

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [Program PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Szablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>Rozpoczęcie tworzenia wewnętrznego modułu równoważenia obciążenia w witrynie Azure Portal

Użyj hello poniższych kroków toocreate wewnętrznego modułu równoważenia obciążenia z hello portalu Azure.

1. Otwórz przeglądarkę, przejdź toohello [portalu Azure](http://portal.azure.com)i zaloguj się przy użyciu konta platformy Azure.
2. Lewy górny powitania po stronie powitania ekranu, kliknij przycisk **nowy** > **sieci** > **modułu równoważenia obciążenia**.
3. W hello **modułu równoważenia obciążenia Utwórz** bloku, wprowadź **nazwa** dla Twojej usługi równoważenia obciążenia.
4. W obszarze **Schemat** kliknij pozycję **Wewnętrzny**.
5. Kliknij przycisk **sieci wirtualnej**, a następnie wybierz hello miejscu modułu równoważenia obciążenia hello toocreate sieci wirtualnej.

   > [!NOTE]
   > Jeśli nie ma sieci wirtualnej hello ma toouse, sprawdź hello **lokalizacji** dla usługi równoważenia obciążenia hello jest używany i odpowiednio je zmienić.

6. Kliknij przycisk **podsieci**, a następnie wybierz miejsce modułu równoważenia obciążenia hello toocreate podsieci hello.
7. W obszarze **przypisywania adresów IP**, kliknij opcję **dynamiczne** lub **statycznych**, w zależności od tego, czy chcesz hello adresu IP dla hello obciążenia równoważenia toobe stałej (statyczny) lub nie.

   > [!NOTE]
   > W przypadku wybrania toouse statycznego adresu IP, konieczne będzie tooprovide adres usługi równoważenia obciążenia hello.

8. W obszarze **grupy zasobów** Określ hello nazwę nowej grupy zasobów dla usługi równoważenia obciążenia hello, lub kliknij przycisk **wybierz istniejącą** i wybierz istniejącą grupę zasobów.
9. Kliknij przycisk **Utwórz**.

## <a name="configure-load-balancing-rules"></a>Konfigurowanie reguł równoważenia obciążenia

Po hello załadować tworzenia równoważenia, przejdź tooconfigure zasobów usługi równoważenia obciążenia toohello go.
Należy tooconfigure najpierw puli adresów zaplecza i badanie przed rozpoczęciem konfigurowania reguły równoważenia obciążenia.

### <a name="step-1-configure-a-back-end-pool"></a>Krok 1. Konfigurowanie puli zaplecza

1. W portalu Azure hello, kliknij przycisk **Przeglądaj** > **usługi równoważenia obciążenia**, a następnie kliknij przycisk modułu równoważenia obciążenia hello utworzone powyżej.
2. W hello **ustawienia** bloku, kliknij przycisk **pul zaplecza**.
3. W hello **pul adresów zaplecza** bloku, kliknij przycisk **Dodaj**.
4. W hello **Dodaj pulę zaplecza** bloku, wprowadź **nazwa** hello puli zaplecza, a następnie kliknij przycisk **OK**.

### <a name="step-2-configure-a-probe"></a>Krok 2. Konfigurowanie sondy

1. W portalu Azure hello, kliknij przycisk **Przeglądaj** > **usługi równoważenia obciążenia**, a następnie kliknij przycisk modułu równoważenia obciążenia hello utworzone powyżej.
2. W hello **ustawienia** bloku, kliknij przycisk **sondy**.
3. W hello **sondy** bloku, kliknij przycisk **Dodaj**.
4. W hello **sondowania Dodaj** bloku, wprowadź **nazwa** hello sondy.
5. W obszarze **Protokół** wybierz pozycję **HTTP** (w przypadku witryn sieci Web) lub **TCP** (w przypadku innych aplikacji działających w oparciu o protokół TCP).
6. W obszarze **portu**, określ hello portu toouse podczas uzyskiwania dostępu do badania hello.
7. W obszarze **ścieżki** (dla protokołu HTTP sondy tylko), określ toouse ścieżka hello jako badanie.
8. W obszarze **interwał** Określ, jak często tooprobe hello aplikacji.
9. W obszarze **próg złej kondycji**, określ liczbę prób powinna zakończyć się niepowodzeniem przed maszyny wirtualnej hello wewnętrznej bazy danych jest oznaczona jako w złej kondycji.
10. Kliknij przycisk **OK** toocreate sondowania.

### <a name="step-3-configure-load-balancing-rules"></a>Krok 3. Konfigurowanie reguł równoważenia obciążenia

1. W portalu Azure hello, kliknij przycisk **Przeglądaj** > **usługi równoważenia obciążenia**, a następnie kliknij przycisk modułu równoważenia obciążenia hello utworzone powyżej.
2. W hello **ustawienia** bloku, kliknij przycisk **reguły równoważenia obciążenia**.
3. W hello **reguły równoważenia obciążenia** bloku, kliknij przycisk **Dodaj**.
4. W hello **reguły równoważenia obciążenia Dodaj** bloku, wprowadź **nazwa** hello reguły.
5. W obszarze **Protokół** wybierz pozycję **HTTP** (w przypadku witryn sieci Web) lub **TCP** (w przypadku innych aplikacji działających w oparciu o protokół TCP).
6. W obszarze **portu**, określ hello portu klienci łączą się moduł równoważenia obciążenia hello tooin.
7. W obszarze **portu zaplecza**, określ hello toobe port używany w puli zaplecza hello (zazwyczaj port usługi równoważenia obciążenia hello i port zaplecza hello są hello sam).
8. W obszarze **puli zaplecza**, wybierz pozycję zaplecza hello puli utworzonego powyżej.
9. W obszarze **trwałości sesji**, wybierz sposób toopersist sesji.
10. W obszarze **limit czasu bezczynności (w minutach)**, określ hello limit czasu bezczynności.
11. W obszarze **Zmienny adres IP (bezpośredni zwrot serwera)** kliknij pozycję **Wyłączony** lub **Włączony**.
12. Kliknij przycisk **OK**.

## <a name="next-steps"></a>Następne kroki

[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)

[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)

