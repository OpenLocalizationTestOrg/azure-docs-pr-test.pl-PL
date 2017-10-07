---
title: "aaaManage zasad laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodefine laboratorium zasad, takich jak wirtualna rozmiar maksymalny maszyn wirtualnych dla poszczególnych użytkowników i zamykania automatyzacji."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a>Zarządzanie wszystkimi zasadami dla laboratorium w usłudze Azure DevTest Labs

Azure DevTest Labs umożliwia kontrolowanie kosztów i zminimalizować odpady w Twojej labs przez Zarządzanie zasadami (ustawienia) dla każdego laboratorium. W tym artykule opisano krok po kroku szczegółowo sposób tooset każdej zasady.  

## <a name="set-allowed-virtual-machine-sizes"></a>Zestaw dozwolone rozmiary maszyn wirtualnych
Witaj zasady dla hello ustawienie dozwolone rozmiary maszyn wirtualnych pomaga laboratorium toominimize odpady włączając toospecify rozmiarów maszyn wirtualnych, które są dozwolone w laboratorium hello. Jeśli zasada ta jest aktywna, tylko rozmiary maszyn wirtualnych z tej listy można toocreate używanych maszyn wirtualnych.

1. W laboratorium hello **konfiguracji i zasadach** bloku, wybierz opcję **dozwolone rozmiary maszyn wirtualnych**.
   
    ![Rozmiary maszyn wirtualnych dozwolonych](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. Wybierz **na** tooenable tych zasad i **poza** toodisable go.

1. Po włączeniu tych zasad, wybierz rozmiarów maszyn wirtualnych, które mogą zostać utworzone w laboratorium.

1. Wybierz pozycję **Zapisz**.

## <a name="set-virtual-machines-per-user"></a>Zestaw maszyn wirtualnych dla użytkownika
Witaj zasady dla **maszyn wirtualnych dla użytkownika** pozwala toospecify hello maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przez użytkownika. Jeśli użytkownik próbuje toocreate lub oświadczeń maszyny Wirtualnej, gdy limit użytkowników hello zostaną spełnione, komunikat o błędzie wskazuje powitalne tej maszyny Wirtualnej nie może być utworzone/żądane. 

1. W laboratorium hello **konfiguracji i zasadach** menu, wybierz opcję **maszyn wirtualnych dla użytkownika**.
   
    ![Maszyny wirtualne na użytkownika](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Wybierz **tak** toolimit hello liczbę maszyn wirtualnych dla poszczególnych użytkowników. Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych dla poszczególnych użytkowników, wybierz **nr**. W przypadku wybrania **tak**, wprowadź wartość liczbową wskazujący hello maksymalną liczbę maszyn wirtualnych, które można utworzyć ani przejęte przez użytkownika. 

1. Wybierz **tak** toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD (dysk SSD). Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD, wybierz **nr**. W przypadku wybrania **tak**, wprowadź wartość wskazującą maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przy użyciu dysków SSD hello. 

1. Wybierz pozycję **Zapisz**.

## <a name="set-virtual-machines-per-lab"></a>Zestaw maszyn wirtualnych dla laboratorium
Witaj zasady dla **maszyn wirtualnych dla laboratorium** pozwala toospecify hello maksymalną liczbę maszyn wirtualnych, które można utworzyć hello bieżącym laboratorium. Jeśli użytkownik próbuje toocreate maszyny Wirtualnej, gdy limit laboratorium hello zostaną spełnione, komunikat o błędzie wskazuje hello, że nie można utworzyć maszyny Wirtualnej. 

1. W laboratorium hello **konfiguracji i zasadach** menu, wybierz opcję **maszyn wirtualnych dla laboratorium**.
   
    ![Maszyn wirtualnych dla laboratorium](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. Wybierz **tak** toolimit hello liczbę maszyn wirtualnych dla laboratorium. Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych dla laboratorium, wybierz **nr**. W przypadku wybrania **tak**, wprowadź wartość liczbową wskazujący hello maksymalną liczbę maszyn wirtualnych, które można utworzyć ani przejęte przez użytkownika. 

1. Wybierz **tak** toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD (dysk SSD). Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych, które mogą używać dysków SSD, wybierz **nr**. W przypadku wybrania **tak**, wprowadź wartość wskazującą maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przy użyciu dysków SSD hello. 

1. Wybierz pozycję **Zapisz**.

## <a name="set-auto-shutdown"></a>Ustaw automatyczne zamykanie
zasady automatycznego zamykania Hello pomaga laboratorium toominimize odpady zezwalając czasu hello toospecify, zamykania maszyn wirtualnych w tym laboratorium.

1. W laboratorium hello **konfiguracji i zasadach** bloku, wybierz opcję **automatyczne zamykanie**.
   
    ![Automatyczne zamykanie](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. Wybierz **na** tooenable tych zasad i **poza** toodisable go.

1. Po włączeniu tych zasad, należy określić hello tooshut godziny (i strefy czasowej) w dół wszystkich maszyn wirtualnych w bieżącym laboratorium hello.

1. Określ **tak** lub **nr** dla toosend opcji hello toohello przed 15 minut powiadomień określona czasu automatycznego zamykania. Jeśli określisz **tak**, wprowadź powiadomienie hello tooreceive punktu końcowego adresu URL elementu webhook. Aby uzyskać więcej informacji na temat elementów webhook, zobacz [tworzenia elementu webhook lub funkcja interfejsu API Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md). 

1. Wybierz pozycję **Zapisz**.

    Domyślnie po włączeniu ta zasada dotyczy maszyn wirtualnych tooall w bieżącym laboratorium hello. tooremove tego ustawienia z określonej maszyny Wirtualnej, otwórz blok hello maszyny Wirtualnej i zmień jego **automatyczne zamykanie** ustawienie 

## <a name="set-auto-start"></a>Ustaw automatyczne uruchamianie
zasady automatycznego uruchamiania Hello umożliwia toospecify hello maszyn wirtualnych w bieżącym laboratorium hello powinna być uruchamiana.  

1. W laboratorium hello **konfiguracji i zasadach** bloku, wybierz opcję **Auto-start**.
   
    ![Automatyczne uruchamianie](./media/devtest-lab-set-lab-policy/auto-start.png)

2. Wybierz **na** tooenable tych zasad i **poza** toodisable go.

3. Po włączeniu tych zasad, określ hello zaplanowany czas rozpoczęcia, strefa czasowa i hello dni tygodnia hello, dla których hello dotyczy czas. 

4. Wybierz pozycję **Zapisz**.

    Po włączeniu tych zasad nie jest automatycznie zastosowane tooany maszyn wirtualnych w bieżącym laboratorium hello. tooapply tooa to ustawienie określonej maszyny Wirtualnej, otwórz hello wirtualna bloku i zmień jego **Auto-start** ustawienie 

## <a name="set-expiration-date"></a>Ustawianie daty wygaśnięcia
Można ustawić wygaśnięcie datę, gdy użytkownik [utworzyć hello wirtualna](devtest-lab-add-vm.md). W **Zaawansowane ustawienia**, wybierz ikonę toospecify kalendarza hello, datę, na którym hello maszyny Wirtualnej zostaną automatycznie usunięte.  Domyślnie program hello wirtualna nigdy nie wygasa.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Następne kroki
Po zdefiniowany i zastosować hello różne ustawienia zasad maszyn wirtualnych dla laboratorium, poniżej przedstawiono niektóre czynności tootry obok:

* [Zrozumienie udostępnionego adresy IP](devtest-lab-shared-ip.md) -wyjaśniono, jak udostępnione IP adresy są używane w DevTest Labs toominimize hello liczby laboratorium tooyour tooconnect wymaganych adresów IP publicznego maszyn wirtualnych.
* [Konfigurowanie kosztów zarządzania](devtest-lab-configure-cost-management.md) -ilustruje sposób toouse hello **miesięczny Trend szacowany koszt** wykresu  
  tooview hello bieżącego miesiąca szacowany koszt do daty i hello planowany koszt koniec miesiąca.
* [Tworzenie niestandardowego obrazu](devtest-lab-create-template.md) — podczas tworzenia maszyny Wirtualnej, należy określić podstawowy, który może być niestandardowy obraz lub obrazu z witryny Marketplace. W tym artykule przedstawiono sposób toocreate niestandardowego obrazu z pliku VHD.
* [Konfigurowanie portalu Marketplace obrazów](devtest-lab-configure-marketplace-images.md) — Azure DevTest Labs obsługuje tworzenie maszyn wirtualnych, oparte na obrazach portalu Azure Marketplace. W tym artykule przedstawiono sposób toospecify, którego, portalu Azure Marketplace obrazy mogą być używane podczas tworzenia maszyn wirtualnych w laboratorium.
* [Utwórz maszynę Wirtualną w laboratorium](devtest-lab-add-vm-with-artifacts.md) -ilustruje sposób toocreate maszyny Wirtualnej z obrazu podstawowego (albo niestandardowe lub Marketplace) i w jaki sposób toowork z artefaktami w maszynie Wirtualnej.

