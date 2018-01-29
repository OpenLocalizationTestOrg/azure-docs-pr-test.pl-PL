---
title: "Grupowanie maszyn przy użyciu zależności maszyny w usłudze Azure migracji | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tworzenia ocenę przy użyciu zależności komputera z usługą Azure migracji."
author: rayne-wiselman
ms.service: azure-migrate
ms.topic: article
ms.date: 12/25/2017
ms.author: raynew
ms.openlocfilehash: 720380fd14d9eaf4856ad75269a80f2b63a4725f
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/02/2018
---
# <a name="group-machines-using-machine-dependency-mapping"></a>Grupy maszyn przy użyciu mapowania zależności maszyny

W tym artykule opisano sposób tworzenia grupy komputerów dla [migracji Azure](migrate-overview.md) oceny przez wizualizowanie zależności maszyn. Jeśli chcesz ocenić grupy maszyn wirtualnych z wyższego poziomu zaufania krzyżowe sprawdzanie z zależnościami maszyny przed uruchomieniem ocenę zwykle Użyj tej metody. Wizualizacja zależności ułatwia efektywne planowanie migracji do usługi Azure. Pomaga zapewnić, że nic pozostawione i awarie niespodziewanego występuje, gdy w przypadku migracji do usługi Azure. Umożliwia odnalezienie wszystkich współzależne systemów, które należy migrować ze sobą i ustalić, czy na komputerze z uruchomionym systemem nadal działa jako użytkowników lub kwalifikuje się do likwidacji zamiast migracji. 


## <a name="prepare-machines-for-dependency-mapping"></a>Przygotowanie maszyny do mapowania zależności
Aby wyświetlić zależności maszyny, musisz pobrać i zainstalować agentów na każdej maszynie lokalnej, która ma zostać oceniona. Ponadto, jeśli masz maszyny bez łączności z Internetem, musisz pobrać i zainstalować [bramy OMS](../log-analytics/log-analytics-oms-gateway.md) na nich.

### <a name="download-and-install-the-vm-agents"></a>Pobierz i zainstaluj agentów maszyny Wirtualnej
1. W **omówienie**, kliknij przycisk **Zarządzaj** > **maszyny**i wybierz wymagany komputer.
2. W **zależności** kolumny, kliknij przycisk **zainstalowani agenci**. 
3. Na **zależności** strony, Pobierz i zainstaluj program Microsoft Monitoring Agent (MMA) i agenta zależności na każdej maszynie Wirtualnej, które chcesz ocenić.
4. Skopiuj identyfikator i klucz. Należy je po zainstalowaniu MMA na maszynie lokalnej.

### <a name="install-the-mma"></a>Zainstaluj MMA

Aby zainstalować agenta na komputerze z systemem Windows:

1. Kliknij dwukrotnie pobrany agenta.
2. Na **stronie powitalnej** kliknij przycisk **Dalej**. Na **postanowień licencyjnych** kliknij przycisk **zgadzam się** do akceptowania licencji.
3. W **Folder docelowy**, Zachowaj lub zmienić domyślny folder instalacji > **dalej**. 
4. W **opcje instalacji agenta**, wybierz pozycję **Analiza dzienników Azure (OMS)** > **dalej**. 
5. Kliknij przycisk **Dodaj** Aby dodać nowy obszar roboczy OMS. Wklej identyfikator i klucz, który został skopiowany z portalu. Kliknij przycisk **Dalej**.


Aby zainstalować agenta na komputerze z systemem Linux:

1. Transfer odpowiedniego pakietu (x86 lub x64) na komputerze systemu Linux przy użyciu scp/sftp.
2. Instalowanie pakietu przy użyciu argumentu--instalacji.

    ```sudo sh ./omsagent-<version>.universal.x64.sh --install -w <workspace id> -s <workspace key>```


### <a name="install-the-dependency-agent"></a>Zainstaluj agenta zależności
1. Aby zainstalować agenta zależności na komputerze z systemem Windows, kliknij dwukrotnie plik konfiguracji i wykonaj instrukcje kreatora.
2. Aby zainstalować agenta zależności na komputerze z systemem Linux, zainstalować jako główny przy użyciu następującego polecenia:

    ```sh InstallDependencyAgent-Linux64.bin```

[Dowiedz się więcej](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) o systemach operacyjnych obsługiwanych przez agenta zależności. 

## <a name="create-a-group"></a>Utwórz grupę

1. Po zainstalowaniu agentów, przejdź do portalu i kliknij przycisk **Zarządzaj** > **maszyny**.
2. Wyszukiwanie maszyny, na którym zainstalowano agentów.
3. **Zależności** kolumny maszyny powinny być teraz wyświetlane jako **zależności widoku**. Kliknij kolumnę, aby wyświetlić zależności maszyny.
4. Zależności mapy dla maszyny zawiera następujące informacje:
    - Przychodzące (klienci) i połączenia wychodzące (serwery) TCP do/z maszyny
        - Zależne maszyny, które nie jest zainstalowany agent MMA i zależności są pogrupowane według numerów portów
        - Maszyny dependenct, które mają MMA i z zainstalowanym agentem zależności są wyświetlane jako osobne pola 
    - Procesów uruchomionych na maszynie, możesz rozszerzyć każde pole maszyny do wyświetlania procesów
    - Właściwości, takie jak pełni kwalifikowana nazwa domeny, System operacyjny, itp. adres MAC każdego komputera, możesz kliknąć każde pole maszyny, aby wyświetlić te szczegóły

 ![Wyświetlanie maszyny zależności](./media/how-to-create-group-machine-dependencies/machine-dependencies.png)

4. Można przyjrzeć zależności dla czasu trwania w innym czasie, klikając na czas trwania w etykiecie zakres czasu. Domyślnie zakres jest godzinę. Możesz zmodyfikować zakres czasu lub określ rozpoczęcia oraz datę zakończenia oraz czas trwania.
5. Po wyłaniają zależnych maszyny, które będą grupowane, za pomocą klawiszy Ctrl + kliknięcie, wybrać wiele komputerów, na mapie, a następnie kliknij przycisk **grupowanie maszyn**.
6. Określ nazwę grupy. Upewnij się, że zależny maszyny są wykrywane przez Azure migracji. 

    > [!NOTE]
    > Jeśli maszyny zależny nie został odnaleziony przez migrację Azure, nie można dodać go do grupy. Aby dodać tych komputerów do grupy, należy ponownie uruchomić proces odnajdowania z zakresem prawa w programie vCenter Server i upewnij się, że komputer jest wykrywane przez Azure migracji.  

7. Jeśli chcesz utworzyć oceny dla tej grupy, wybierz pole wyboru, aby utworzyć nowy oceny grupy.
8. Kliknij przycisk **OK** można zapisać grupy.

Po utworzeniu grupy, zaleca się instalowania agentów na wszystkich komputerach, grupy i zakres grupy wizualizowanie zależności całej grupy.

## <a name="next-steps"></a>Kolejne kroki

- [Dowiedz się, jak](how-to-create-group-dependencies.md) Aby zawęzić kryteria do grupy przez wizualizowanie zależności grupy
- [Dowiedz się więcej](concepts-assessment-calculation.md) o obliczania oceny.
