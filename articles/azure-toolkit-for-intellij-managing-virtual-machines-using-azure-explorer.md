---
title: "aaaManage maszyn wirtualnych przy użyciu hello Azure Explorer for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage maszynach wirtualnych platformy Azure przy użyciu hello Azure Explorer for IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a>Zarządzania maszynami wirtualnymi przy użyciu hello Azure Explorer for IntelliJ

Hello Azure Eksploratora, będący częścią hello Azure Toolkit for IntelliJ zapewnia Java deweloperom łatwe w użyciu rozwiązanie do zarządzania maszynami wirtualnymi na koncie Azure z wewnątrz hello IntelliJ zintegrowane środowisko programistyczne (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Utwórz maszynę wirtualną w IntelliJ

toocreate maszynę wirtualną za pomocą Eksploratora Azure hello hello następujące: 

1. Zaloguj tooyour konto platformy Azure przy użyciu kroków hello w hello [logowania instrukcje dotyczące hello Azure Toolkit for IntelliJ] artykułu.

2. W hello **Eksploratora Azure** wyświetlić, rozwiń węzeł hello **Azure** węzła, kliknij prawym przyciskiem myszy **maszyn wirtualnych**, a następnie kliknij przycisk **Utwórz maszynę Wirtualną**. 

   ![Witaj polecenia Utwórz maszynę Wirtualną][CR01]  
    Witaj **tworzenia nowej maszyny wirtualnej** zostanie otwarty Kreator.

3. W hello **Wybierz subskrypcję** okna, wybierz subskrypcję, a następnie kliknij przycisk **dalej**. 

   ![Witaj wybierz okno subskrypcji][CR02]

4. W hello **Wybieranie obrazu maszyny wirtualnej** okna, wprowadź hello następujących informacji:

   * **Lokalizacja**: Określa, gdzie można utworzyć maszyny wirtualnej (na przykład *zachodnie stany USA*). 

   * **Zalecane obrazu**: Określa, czy wybierzesz obraz z skróconą listę często używane obrazy.

   * **Obraz niestandardowy**: Określa, że będzie Wybieranie niestandardowego obrazu, zapewniając hello następujących informacji:

      * **Wydawca**: Określa hello wydawcy, który utworzył obraz hello, która będzie używana dla maszyny wirtualnej (na przykład *Microsoft*).

      * **Oferują**: Określa maszyny wirtualnej hello oferty toouse hello wybranego wydawcy (na przykład *JDK*).

      * **Jednostka SKU**: Określa hello składowania jednostka SKU toouse z wybranej oferty hello (na przykład *JDK_8*).

      * **Wersja #**: Określa, która wersja hello wybrane toouse jednostki SKU.

   ![Witaj Wybierz przedział obraz maszyny wirtualnej][CR03]

5. Kliknij przycisk **Dalej**. 

6. W hello **ustawienia podstawowej maszyny wirtualnej** okna, wprowadź hello następujących informacji:

   * **Nazwa maszyny wirtualnej**: Określa nazwę powitania dla nowej maszyny wirtualnej, który musi rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.

   * **Rozmiar**: Określa liczbę hello rdzeni i tooallocate pamięci dla maszyny wirtualnej.

   * **Nazwa użytkownika**: Określa toocreate konto administratora hello zarządzania maszyny wirtualnej.

   * **Hasło** i **Potwierdź**: Określa hello hasło dla konta administratora.

   ![Witaj okno Ustawienia podstawowej maszyny wirtualnej][CR04]

7. Kliknij przycisk **Dalej**. 

8. W hello **skojarzonych zasobów** okna, wprowadź hello następujących informacji:

   * **Grupa zasobów**: Określa hello grupy zasobów dla maszyny wirtualnej. Wybierz jedną z hello następujące opcje:
      * **Utwórz nowe**: Określa, że toocreate nową grupę zasobów.
      * **Użyj istniejącego**: Określa, że tooselect z listy grup zasobów, które są skojarzone z Twoim kontem platformy Azure.

       ![Okno skojarzone zasoby Hello][CR07]

   * **Konto magazynu**: Określa toouse konta magazynu hello do przechowywania maszyny wirtualnej. Można wybrać istniejące konto magazynu lub utworzyć nowe konto. Jeśli wybierzesz **Utwórz nowy**, zostanie wyświetlone następujące okno dialogowe hello:

      ![okno dialogowe Tworzenie konta magazynu Hello][CR05]

   * **Sieć wirtualna** i **podsieci**: Określa hello sieci wirtualnej i podsieci, które będą się łączyć maszyny wirtualnej. Można użyć istniejącej sieci i podsieci, lub można utworzyć nowej sieci i podsieci. W przypadku wybrania **Utwórz nowy**, zostanie wyświetlone następujące okno dialogowe hello:

      ![okno dialogowe Tworzenie sieci wirtualnej Hello][CR06]

   * **Publiczny adres IP**: Określa adres IP dołączonej do Internetu dla maszyny wirtualnej. Można wybrać toocreate nowego adresu IP, lub Jeśli maszyna wirtualna nie ma publicznego adresu IP, możesz wybrać **(Brak)**. 

   * **Grupy zabezpieczeń sieci**: Określa opcjonalne zapory sieci dla maszyny wirtualnej. Możesz wybrać istniejącą zapory lub, jeśli maszyna wirtualna nie będzie używać zapory sieciowej, można wybrać **(Brak)**. 

   * **Zestaw dostępności**: określa zbiór dostępności opcjonalne, że maszyna wirtualna może należeć do. Można wybrać istniejący zestaw dostępności, Utwórz nowy zestaw dostępności lub, jeśli na komputerze wirtualnym, nie będą należeć tooan zestawu dostępności, wybierz **(Brak)**.

9. Kliknij przycisk **Zakończ**.  
    Nowej maszyny wirtualnej jest wyświetlany w oknie narzędzia Eksploratora Azure hello. 

   ![Nową maszynę wirtualną w widoku Eksploratora Azure hello][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Uruchom ponownie maszynę wirtualną w IntelliJ

toorestart maszynę wirtualną za pomocą Eksploratora Azure hello w IntelliJ, hello następujące:

1. W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **ponownego uruchomienia**.

   ![Witaj polecenia ponownego uruchomienia maszyny wirtualnej][RE01]

2. W oknie potwierdzenia powitania kliknij **tak**. 

   ![Witaj ponownie uruchom okno potwierdzenia maszyny wirtualnej][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Zamknij maszynę wirtualną w IntelliJ

tooshut dół uruchomionej maszyny wirtualnej za pomocą Eksploratora Azure hello w IntelliJ, hello następujące:

1. W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **zamknięcia**.

   ![polecenie zamknięcia Hello maszyn wirtualnych][SH01]

2. W oknie potwierdzenia powitania kliknij **tak**. 

   ![Witaj, zamknij okno potwierdzenia maszyny wirtualnej][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Usuń maszynę wirtualną w IntelliJ

toodelete maszynę wirtualną za pomocą Eksploratora Azure hello w IntelliJ, hello następujące:

1. W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, a następnie wybierz **usunąć**.

   ![polecenie Usuń Hello maszyn wirtualnych][DE01]

2. W oknie potwierdzenia powitania kliknij **tak**. 

   ![Witaj usunąć okno potwierdzenia maszyny wirtualnej][DE02]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat rozmiarów maszyn wirtualnych platformy Azure i cenach Zobacz hello następujące zasoby:

* Rozmiary maszyn wirtualnych platformy Azure
  * [Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]
  * [Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]
* Cennik maszyn wirtualnych platformy Azure
  * [Cennik maszyn wirtualnych systemu Windows]
  * [Cennik maszyn wirtualnych systemu Linux]

Aby uzyskać więcej informacji o hello narzędzi Azure Java IDEs zobacz następujące zasoby hello:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [What's new in hello Azure Toolkit for IntelliJ]
  * [Instalowanie hello Azure Toolkit for IntelliJ]
  * [logowania instrukcje dotyczące hello Azure Toolkit for IntelliJ]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[logowania instrukcje dotyczące hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's new in hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

[Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Cennik maszyn wirtualnych systemu Windows]: /pricing/details/virtual-machines/windows/
[Cennik maszyn wirtualnych systemu Linux]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
