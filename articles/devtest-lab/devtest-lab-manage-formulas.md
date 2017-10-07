---
title: "aaaManage formuły w usłudze Azure DevTest Labs toocreate maszyn wirtualnych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupdate i Usuń formuły Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a>Zarządzanie formuły Azure DevTest Labs

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

W tym artykule przedstawiono sposób toocreate formuła z podstawowej (obrazu niestandardowego obrazu z witryny Marketplace i formułą) lub istniejącej maszyny Wirtualnej. W tym artykule również przeprowadzi Cię przez zarządzanie istniejące formuły.

## <a name="create-a-formula"></a>Utwórz formułę
Każda osoba mająca DevTest Labs *użytkowników* uprawnień jest możliwe toocreate maszyn wirtualnych przy użyciu formuły jako podstawy. Istnieją dwa sposoby toocreate formuły: 

* Z podstawowej — należy użyć toodefine wszystkie właściwości hello hello formuły.
* Z istniejącego laboratorium VM - używany w toocreate formuły na podstawie hello ustawień z istniejącej maszyny Wirtualnej.

Aby uzyskać więcej informacji na temat dodawania użytkowników i uprawnień, zobacz [Dodaj właścicieli i użytkowników w usłudze Azure DevTest Labs](./devtest-lab-add-devtest-user.md).

### <a name="create-a-formula-from-a-base"></a>Utwórz formułę z podstawowej
Witaj, wykonaj czynności pomocne hello proces tworzenia formuł z niestandardowego obrazu, obrazu z witryny Marketplace lub formułą.

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

2. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.

3. Z listy hello labs wybierz żądany laboratorium hello.  

4. W bloku hello laboratorium, wybierz **formuły (podstaw wielokrotnego użytku)**.
   
    ![Formuły menu](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. Na powitania **formuły** bloku, wybierz opcję **+ Dodaj**.
   
    ![Dodawanie formuły](./media/devtest-lab-create-formulas/add-formula.png)

6. Na powitania **wybierz podstawowej** bloku base wybierz hello (obrazu niestandardowego obrazu z witryny Marketplace i formuły) z którego mają zostać toocreate hello formuły.
   
    ![Lista podstawowa](./media/devtest-lab-create-formulas/base-list.png)

7. Na powitania **utworzyć formuły** bloku, określ hello następujące wartości:
   
    * **Nazwa formuły** — wprowadź nazwę dla formuły. Ta wartość jest wyświetlana w hello listy obrazów podstawowej podczas tworzenia maszyny Wirtualnej. Nazwa Hello jest weryfikowana go, a jeśli jest on nieprawidłowy komunikat wskazuje hello wymagania dotyczące prawidłową nazwę.
    * **Opis elementu** — wpisz zrozumiały opis dla formuły. Ta wartość jest dostępna z menu kontekstowego hello formuły, podczas tworzenia maszyny Wirtualnej.
    * **Nazwa użytkownika** — wprowadź nazwę użytkownika, któremu udzielono uprawnień administratora.
    * **Hasło** — wprowadź - lub wybierz z listy rozwijanej hello - wartość, która jest skojarzona z hello hasło, mają toouse dla hello określonego użytkownika. Aby uzyskać więcej informacji na temat kluczy tajnych hello, zobacz [Azure DevTest Labs: tajne magazynie osobistym](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).
    * **Typ dysku maszyny wirtualnej** — określ albo dysk twardy (dysk twardy) lub tooindicate dysków SSD (SSD) typ dysku magazynu, który jest dozwolony dla maszyn wirtualnych hello udostępniane przy użyciu tego obrazu podstawowego.
    * ** Maszyny wirtualnej rozmiar ** — wybierz jedną z hello wstępnie zdefiniowane elementy, które Określ hello rdzeni procesora, rozmiar pamięci RAM i rozmiar dysku twardego hello hello toocreate maszyny Wirtualnej. 
    * **Artefakty** -hello wybierz tooopen **dodać artefakty** bloku, w którym wybierz i skonfiguruj artefakty hello, które mają tooadd toohello podstawowy obraz. Aby uzyskać więcej informacji na temat artefaktów, zobacz [artefakty zarządzania maszyny Wirtualnej w usłudze Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).
    * **Zaawansowane ustawienia** -hello wybierz tooopen **zaawansowane** bloku, w którym skonfigurować hello następujące ustawienia:
        * **Sieć wirtualna** — Określ hello potrzeby sieci wirtualnej.
        * **Podsieci** — Określ podsieć hello potrzebne.    
        * **Adres IP** -określić adresy hello Public, Private lub udostępnione IP. Aby uzyskać więcej informacji na temat udostępnionych adresów IP, zobacz [omówienie udostępnionych adresów IP w usłudze Azure DevTest Labs](./devtest-lab-shared-ip.md).
        * **Przydziel tej maszynie claimable** — co maszyna "claimable" oznacza, że go nie zostaną przypisane prawa własności w czasie hello tworzenia. Zamiast tego użytkownicy laboratorium będą mogli tootake własność ("roszczenie") hello maszyny w bloku hello laboratorium.     
    * **Obraz** -wyświetlana nazwa obrazu podstawowego hello wybranego na powitania poprzedniego bloku. 
     
       ![Utwórz formułę](./media/devtest-lab-create-formulas/create-formula.png)

8. Wybierz **Utwórz** toocreate hello formuły.

9. Tworzona formuła hello wyświetla na liście hello na powitania **formuły** bloku.

### <a name="create-a-formula-from-a-vm"></a>Utwórz formułę z maszyny Wirtualnej
Witaj następujące kroki przedstawiono hello proces tworzenia formułę opartą na istniejącej maszyny Wirtualnej. 

> [!NOTE]
> toocreate formuły z maszyny Wirtualnej, hello maszyny Wirtualnej musi być utworzony po 30 marca 2016 r. 
> 
> 

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
3. Z listy hello labs wybierz żądany laboratorium hello.  
4. W laboratorium hello **omówienie** bloku, wybierz hello maszyny Wirtualnej, z którego chcesz toocreate hello formuły.
   
    ![Maszyny wirtualne laboratoria](./media/devtest-lab-create-formulas/my-vms.png)
5. W bloku hello wirtualna wybierz **utworzyć formuły (base wielokrotnego użytku)**.
   
    ![Utwórz formułę](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. Na powitania **utworzyć formuły** bloku, wprowadź **nazwa** i **opis** dla nowej formuły.
   
    ![Tworzenie formuły bloku](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. Wybierz **OK** toocreate hello formuły.

## <a name="modify-a-formula"></a>Zmodyfikuj formułę
toomodify formuły, wykonaj następujące kroki:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
3. Z listy hello labs wybierz żądany laboratorium hello.  
4. W bloku hello laboratorium, wybierz **formuły (podstaw wielokrotnego użytku)**.
   
    ![Formuły menu](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Na powitania **formuły laboratorium** bloku, wybierz hello formuły mają toomodify.
6. Na powitania **zaktualizować formułę** bloku, dokonaj edycji hello potrzebne, a następnie wybierz **aktualizacji**.

## <a name="delete-a-formula"></a>Usuwanie formuły
toodelete formuły, wykonaj następujące kroki:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
3. Z listy hello labs wybierz żądany laboratorium hello.  
4. W laboratorium hello **ustawienia** bloku, wybierz opcję **formuły**.
   
    ![Formuły menu](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. Na powitania **formuły laboratorium** bloku, wybierz hello wielokropka toohello rogu formuła hello mają toodelete.
   
    ![Formuły menu](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. W menu kontekstowym hello formuły, wybierz **usunąć**.
   
    ![Menu kontekstowe formuły](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. Wybierz **tak** okno dialogowe potwierdzenia usunięcia toohello.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Wpisy na blogu pokrewne
* [Niestandardowe obrazy lub formuł?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Następne kroki
Po utworzeniu formułę do użycia podczas tworzenia maszyny Wirtualnej, następnym krokiem hello jest zbyt[Dodawanie maszyny Wirtualnej laboratorium tooyour](devtest-lab-add-vm-with-artifacts.md).

