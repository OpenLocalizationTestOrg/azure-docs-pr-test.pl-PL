---
title: "Rozwiązywanie problemów maszyny Wirtualnej platformy Azure przy użyciu zagnieżdżonych wirtualizacji na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak rozwiązać problem z maszyny Wirtualnej platformy Azure przy użyciu zagnieżdżonych wirtualizacji na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 11/06/2017
ms.author: genli
ms.openlocfilehash: b50d139f62ef773fb5b9bb2638e40f8154e80979
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/03/2018
---
# <a name="troubleshoot-a-problem-azure-vm-by-using-nested-virtualization-in-azure"></a>Rozwiązywanie problemów maszyny Wirtualnej platformy Azure przy użyciu zagnieżdżonych wirtualizacji na platformie Azure

W tym artykule pokazano, jak utworzyć środowisko wirtualizacji zagnieżdżone na platformie Microsoft Azure, można zainstalować dysk problemu maszyny Wirtualnej na hoście funkcji Hyper-V (odzyskiwania maszyn wirtualnych) na potrzeby rozwiązywania problemów.

## <a name="prerequisite"></a>Wymagania wstępne

Aby zainstalować problem maszyny Wirtualnej, maszyna wirtualna odzyskiwania musi spełniać następujące wymagania wstępne:

-   Maszyna wirtualna odzyskiwania musi być w tej samej lokalizacji co problem maszyny Wirtualnej.

-   Maszyna wirtualna odzyskiwania musi być w tej samej grupie zasobów co problem maszyny Wirtualnej.

-   Maszyna wirtualna odzyskiwania musi używać tego samego typu konta magazynu (standardowa lub Premium), co problem maszyny Wirtualnej.

## <a name="step-1-create-a-recovery-vm-and-install-hyper-v-role"></a>Krok 1: Utworzenie maszyny Wirtualnej odzyskiwania i zainstalować rolę funkcji Hyper-V

1.  Utwórz nową maszynę Wirtualną odzyskiwania:

    -  System operacyjny: Windows Server 2016 Datacenter

    -  Rozmiar: Ciągu V3 z co najmniej dwa rdzenie tego wirtualizacji zagnieżdżone pomocy technicznej. Aby uzyskać więcej informacji, zobacz [wprowadzenie nowe rozmiary Dv3 i wirtualna Ev3](https://azure.microsoft.com/blog/introducing-the-new-dv3-and-ev3-vm-sizes/).

    -  Tej samej lokalizacji, konta magazynu i grupy zasobów jako problem maszyny Wirtualnej.

    -  Wybierz ten sam typ magazynu jako problem maszyny Wirtualnej (standardowy lub Premium).

2.  Po maszyna wirtualna odzyskiwania jest tworzony, pulpitu zdalnego do maszyny Wirtualnej odzyskiwania.

3.  W Menedżerze serwera wybierz **Zarządzaj** > **Dodaj role i funkcje**.

4.  W **typu instalacji** zaznacz **Instalacja roli lub funkcji**.

5.  W **serwera docelowego wybierz** sekcji, upewnij się, że maszyna wirtualna odzyskiwania jest zaznaczona.

6.  Wybierz **roli funkcji Hyper-V** > **Dodaj funkcje**.

7.  Wybierz **dalej** na **funkcje** sekcji.

8.  Jeśli przełącznik wirtualny jest dostępna, zaznacz go. W przeciwnym razie wybierz **dalej**.

9.  Na **migracji** zaznacz **dalej**

10. Na **magazyny domyślne** zaznacz **dalej**.

11. Pole wyboru, aby automatycznie uruchom ponownie serwer, jeśli jest to wymagane.

12. Wybierz **zainstalować**.

13. Zezwalaj na serwerze, aby zainstalować rolę funkcji Hyper-V. To zajmuje kilka minut, a serwer zostanie automatycznie ponownie uruchomiony.

## <a name="step-2-create-the-problem-vm-on-the-recovery-vms-hyper-v-server"></a>Krok 2: Tworzenie problem maszyny Wirtualnej na serwerze funkcji Hyper-V maszyny Wirtualnej odzyskiwania

1.  Zapisz nazwę dysku problem maszyny Wirtualnej, a następnie usuń problem maszyny Wirtualnej. Upewnij się, że zachowasz wszystkich dołączonych dysków. 

2.  Dołącz dysk systemu operacyjnego problemu maszyny Wirtualnej jako dysku danych maszyny wirtualnej odzyskiwania.

    1.  Po jego usunięciu maszyny Wirtualnej, przejdź do maszyny Wirtualnej odzyskiwania.

    2.  Wybierz **dysków**, a następnie **Dodaj dysk danych**.

    3.  Wybierz dysk maszyny Wirtualnej problem, a następnie wybierz **zapisać**.

3.  Po dysku została pomyślnie dołączona, zdalny pulpit do maszyny Wirtualnej odzyskiwania.

4.  Otwórz przystawkę Zarządzanie dyskami (diskmgmt.msc). Upewnij się, że dysk problem maszyny Wirtualnej, jest ustawiony na **Offline**.

5.  Otwórz Menedżera funkcji Hyper-V: W **Menedżera serwera**, wybierz pozycję **roli funkcji Hyper-V**. Kliknij prawym przyciskiem myszy serwer, a następnie wybierz **Menedżera funkcji Hyper-V**.

6.  W Menedżerze funkcji Hyper-V kliknij prawym przyciskiem myszy maszynę Wirtualną odzyskiwania, a następnie wybierz **nowy** > **maszyny wirtualnej** > **dalej**.

7.  Wpisz nazwę maszyny Wirtualnej, a następnie wybierz **dalej**.

8.  Wybierz **generacji 1**.

9.  Pamięć początkowa ustawioną 1024 MB lub większej.

10. Jeśli ma to zastosowanie wybierz przełącznik sieci funkcji Hyper-V, który został utworzony. Else przejdź do następnej strony.

11. Wybierz **Dołącz wirtualny dysk twardy później**.

    ![obraz o Attach opcja później wirtualnego dysku twardego](./media/troubleshoot-vm-by-use-nested-virtualization/attach-disk-later.png)

12. Wybierz **Zakończ** po utworzeniu maszyny Wirtualnej.

13. Kliknij prawym przyciskiem myszy maszynę Wirtualną, która zostanie utworzona, a następnie wybierz **ustawienia**.

14. Wybierz **kontroler IDE 0**, wybierz pozycję **dysk twardy**, a następnie kliknij przycisk **Dodaj**.

    ![obraz o dodaje nowy dysk twardy](./media/troubleshoot-vm-by-use-nested-virtualization/create-new-drive.png)    

15. W **fizyczny dysk twardy**, wybierz dysk problem, maszynie Wirtualnej, która jest dołączona do maszyny Wirtualnej platformy Azure. Jeśli nie ma żadnych dysków na liście, należy sprawdzić, jeśli dysk ma ustawioną w trybie offline za pomocą przystawki Zarządzanie dyskami.

    ![obraz o instaluje dysk](./media/troubleshoot-vm-by-use-nested-virtualization/mount-disk.png)  


17. Wybierz **Zastosuj**, a następnie wybierz **OK**.

18. Kliknij dwukrotnie na maszynie Wirtualnej, a następnie uruchom go.

19. Możesz teraz pracować na maszynie Wirtualnej jako lokalną maszynę Wirtualną. Można wykonać wszystkie kroki rozwiązywania problemów, które są potrzebne.

## <a name="step-3-re-create-your-azure-vm-in-azure"></a>Krok 3: Ponownie utwórz Azure maszyny Wirtualnej na platformie Azure

1.  Po uzyskaniu trybu online maszyny Wirtualnej, zamknij maszynę Wirtualną w Menedżerze funkcji Hyper-V.

2.  Przejdź do [portalu Azure](https://portal.azure.com) i wybierz maszynę Wirtualną odzyskiwania > dysków, skopiuj nazwę dysku. Nazwa będzie używana w następnym kroku. Odłącz stały dysk od maszyny Wirtualnej odzyskiwania.

3.  Przejdź do **wszystkie zasoby**, wyszukaj nazwę dysku, a następnie wybierz dysk.

     ![obraz o wyszukuje dysku](./media/troubleshoot-vm-by-use-nested-virtualization/search-disk.png)     

4. Kliknij przycisk **tworzenie maszyny Wirtualnej**.

     ![obraz o utworzenie maszyny wirtualnej z dysku](./media/troubleshoot-vm-by-use-nested-virtualization/create-vm-from-vhd.png) 

Za pomocą programu PowerShell Azure można również utworzyć maszynę Wirtualną z dysku. Aby uzyskać więcej informacji, zobacz [tworzenia nowej maszyny Wirtualnej z istniejącego dysku przy użyciu programu PowerShell](create-vm-specialized.md#create-the-new-vm). 

## <a name="next-steps"></a>Kolejne kroki

Jeśli występują problemy dotyczące nawiązywania połączenia z maszyną Wirtualną, zobacz [połączeniami RDP Rozwiązywanie problemów z maszyną wirtualną Azure](troubleshoot-rdp-connection.md). W przypadku problemów z dostępem do aplikacji działających na maszynie Wirtualnej, zobacz [Rozwiązywanie problemów z łącznością aplikacji na maszynie Wirtualnej Windows](troubleshoot-app-connection.md).
