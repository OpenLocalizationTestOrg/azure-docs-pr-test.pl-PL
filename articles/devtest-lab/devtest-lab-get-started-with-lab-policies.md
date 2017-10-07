---
title: "aaaManage zasady podstawowe laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset niektóre hello podstawowych zasad (ustawienia) dla laboratorium w usłudze DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a>Zarządzanie zasadami podstawowe dla laboratorium w usłudze Azure DevTest Labs

Azure DevTest Labs umożliwia toocontrol kosztów i zminimalizować odpady w Twojej labs przez Zarządzanie zasadami (ustawienia) dla każdego laboratorium. W tym artykule należy Rozpoczynanie pracy z zasadami przez learning, jak tooset dwóch najważniejszych zasad hello — ograniczenie hello liczbę maszyn wirtualnych (VM), które zostały utworzone lub żądane przez pojedynczego użytkownika i Konfigurowanie automatycznego zamykania. tooview jak tooset każdych zasad laboratorium, zobacz artykuł hello [Definiowanie zasad laboratorium w usłudze Azure DevTest Labs](devtest-lab-set-lab-policy.md).  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a>Uzyskiwanie dostępu do zasad laboratorium w usłudze Azure DevTest Labs
Witaj następujące kroki informacje pomocne przy konfigurowaniu zasad dla laboratorium w usłudze Azure DevTest Labs:

zasady hello tooview (i zmiana) dla laboratorium, wykonaj następujące kroki:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.

1. Z listy hello labs wybierz żądany laboratorium hello.   

1. Wybierz **konfiguracji i zasadach**.

    ![Blok ustawień zasad](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. Witaj **konfiguracji i zasadach** blok zawiera menu Ustawienia, które można określić. W tym artykule opisano tylko hello ustawienia **maszyn wirtualnych dla użytkownika** i **automatyczne zamykanie**. toolearn o hello pozostałych ustawień, zobacz [zarządzanie wszystkimi zasadami dla laboratorium w usłudze Azure DevTest Labs](./devtest-lab-set-lab-policy.md). 
   
## <a name="set-virtual-machines-per-user"></a>Zestaw maszyn wirtualnych dla użytkownika
Witaj zasady dla **maszyn wirtualnych dla użytkownika** pozwala toospecify hello maksymalną liczbę maszyn wirtualnych, które mogą zostać utworzone przez użytkownika. Jeśli użytkownik próbuje toocreate lub oświadczeń maszyny Wirtualnej, gdy limit użytkowników hello zostaną spełnione, komunikat o błędzie wskazuje powitalne tej maszyny Wirtualnej nie może być utworzone/żądane. 

1. W laboratorium hello **konfiguracji i zasadach** menu, wybierz opcję **maszyn wirtualnych dla użytkownika**.
   
    ![Maszyny wirtualne na użytkownika](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. Wybierz **tak** toolimit hello liczbę maszyn wirtualnych dla poszczególnych użytkowników. Jeśli nie chcesz, aby toolimit hello liczbę maszyn wirtualnych dla poszczególnych użytkowników, wybierz **nr**. W przypadku wybrania **tak**, wprowadź wartość liczbową wskazujący hello maksymalną liczbę maszyn wirtualnych, które można utworzyć ani przejęte przez użytkownika. 

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

## <a name="next-steps"></a>Następne kroki

- [Definiowanie zasad laboratorium w usłudze Azure DevTest Labs](devtest-lab-set-lab-policy.md) — Dowiedz się, jak toomodify innych zasad laboratorium 
