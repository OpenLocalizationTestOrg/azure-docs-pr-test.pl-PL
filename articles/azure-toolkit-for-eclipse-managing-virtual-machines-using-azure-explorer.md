---
title: "Zarządzania maszynami wirtualnymi przy użyciu Eksploratora Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać maszynach wirtualnych platformy Azure za pomocą Eksploratora Azure dla programu Eclipse."
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
ms.openlocfilehash: 9784e8af9c530078afee06f08a23403a44b0762f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a>Zarządzania maszynami wirtualnymi przy użyciu Eksploratora Azure dla programu Eclipse

Eksploratora Azure, która jest częścią zestawu narzędzi platformy Azure dla programu Eclipse, oferuje Java deweloperom łatwe w użyciu rozwiązanie do zarządzania maszynami wirtualnymi na koncie Azure z wewnątrz Eclipse zintegrowane środowisko programistyczne (IDE).

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Utwórz maszynę wirtualną w środowisku Eclipse

Aby utworzyć maszynę wirtualną za pomocą Eksploratora Azure, wykonaj następujące czynności:

1. Zaloguj się do konta platformy Azure przy użyciu [instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse].

2. W **Eksploratora Azure** wyświetlić, rozwiń węzeł **Azure** węzła, kliknij prawym przyciskiem myszy **maszyn wirtualnych**, a następnie kliknij przycisk **Utwórz maszynę Wirtualną**.

   ![Polecenie Utwórz maszynę Wirtualną][CR01]  
   **Tworzenia nowej maszyny wirtualnej** zostanie otwarty Kreator.

3. W **Wybierz subskrypcję** okna, wybierz subskrypcję, a następnie kliknij przycisk **dalej**.

   ![Wybierz okno subskrypcji][CR02]

4. W **Wybieranie obrazu maszyny wirtualnej** okna, wprowadź następujące informacje:

   * **Lokalizacja**: Określa, gdzie można utworzyć maszyny wirtualnej (na przykład *zachodnie stany USA*).

   * **Wydawca**: Określa wydawcy, który utworzył obraz będziesz używać do tworzenia maszyny wirtualnej (na przykład *Microsoft*).

   * **Oferują**: określa oferty do użycia z wybranego wydawcy maszyny wirtualnej (na przykład *JDK*).

   * **Jednostka SKU**: Określa jedn (SKU) do użycia z wybranej oferty (na przykład *JDK_8*).

   * **Wersja #**: Określa, która wersja wybranej jednostki SKU do użycia.

    ![Wybierz okno Obraz maszyny wirtualnej][CR03]

5. Kliknij przycisk **Dalej**.

6. W **ustawienia podstawowej maszyny wirtualnej** okna, wprowadź następujące informacje:

   * **Nazwa maszyny wirtualnej**: Określa nazwę dla nowej maszyny wirtualnej, który musi rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.

   * **Rozmiar**: Określa liczbę rdzeni i ilości pamięci do przydzielenia dla maszyny wirtualnej.

   * **Nazwa użytkownika**: Określa konto administratora, aby utworzyć zarządzania maszyny wirtualnej.

   * **Hasło** i **Potwierdź**: Określa hasło dla konta administratora.

    ![Okno Ustawienia podstawowej maszyny wirtualnej][CR04]

7. Kliknij przycisk **Dalej**.

8. W **utworzyć nowe konto magazynu** okna, wprowadź następujące informacje:

   * **Grupa zasobów**: Określa grupę zasobów dla maszyny wirtualnej. Wybierz jedną z następujących opcji:
      * **Utwórz nowe**: Określa, czy chcesz utworzyć nową grupę zasobów.
      * **Użyj istniejącego**: Określa, czy chcesz wybrać grupę zasobów, która jest już skojarzona z Twoim kontem platformy Azure.

      ![Okno dialogowe Tworzenie nowego konta magazynu][CR05]

   * **Konto magazynu**: Określa konto magazynu do przechowywania maszyny wirtualnej. Możesz użyć istniejącego konta magazynu lub utworzyć nowe konto.

   * **Sieć wirtualna** i **podsieci**: Określa sieci wirtualnej i podsieci, które będą się łączyć maszyny wirtualnej. Można użyć istniejącej sieci i podsieci, lub można utworzyć nowej sieci i podsieci. W przypadku wybrania **Utwórz nowy**, zostanie wyświetlone następujące okno dialogowe:

      ![Okno dialogowe Tworzenie nowej sieci wirtualnej][CR06]

9. W **skojarzonych zasobów** okna, wprowadź następujące informacje:

   * **Publiczny adres IP**: Określa adres IP dołączonej do Internetu dla maszyny wirtualnej. Użytkownik może utworzyć nowego adresu IP, lub Jeśli maszyna wirtualna nie ma publicznego adresu IP, możesz wybrać **(Brak)**.

   * **Grupy zabezpieczeń sieci**: Określa opcjonalne zapory sieci dla maszyny wirtualnej. Możesz wybrać istniejącą zapory lub, jeśli maszyna wirtualna nie będzie używać zapory sieciowej, można wybrać **(Brak)**.

   * **Zestaw dostępności**: określa zbiór dostępności opcjonalne, że maszyna wirtualna może należeć do. Można wybrać istniejący zestaw dostępności lub Utwórz nowy zestaw dostępności lub, jeśli na komputerze wirtualnym zostanie nie należą do zestawu dostępności, możesz wybrać **(Brak)**.

   ![Okno skojarzonych zasobów][CR07]

9. Kliknij przycisk **Zakończ**.  
  Nowej maszyny wirtualnej jest wyświetlany w oknie narzędzia Eksplorator Azure.

   ![Nowej maszyny wirtualnej][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Uruchom ponownie maszynę wirtualną w środowisku Eclipse

Aby ponownie uruchomić maszynę wirtualną za pomocą Eksploratora Azure w programie Eclipse, wykonaj następujące czynności:

1. W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy maszynę wirtualną, a następnie wybierz **ponownego uruchomienia**.

   ![Polecenie ponownego uruchomienia maszyny wirtualnej][RE01]

2. W oknie potwierdzenia kliknij **tak**.

   ![Okno potwierdzenia ponownego uruchomienia][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Zamknij maszynę wirtualną w środowisku Eclipse

Aby zamknąć uruchomionej maszyny wirtualnej za pomocą Eksploratora Azure w programie Eclipse, wykonaj następujące czynności:

1. W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy maszynę wirtualną, a następnie wybierz **zamknięcia**.

   ![Polecenie zamknięcia maszyn wirtualnych][SH01]

2. W oknie potwierdzenia kliknij **tak**.

   ![Okno potwierdzenia zamknięcia maszyn wirtualnych][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Usuń maszynę wirtualną w środowisku Eclipse

Aby usunąć maszynę wirtualną za pomocą Eksploratora Azure w programie Eclipse, wykonaj następujące czynności:

1. W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy maszynę wirtualną, a następnie wybierz **usunąć**.

   ![Polecenie Usuń maszynę wirtualną][DE01]

2. W oknie potwierdzenia kliknij **tak**.

   ![Okno potwierdzenia usunięcia maszyny wirtualnej][DE02]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat rozmiarów maszyn wirtualnych platformy Azure i cenach zobacz następujące zasoby:

* Rozmiary maszyn wirtualnych platformy Azure
  * [Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]
  * [Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]
* Cennik maszyn wirtualnych platformy Azure
  * [Cennik maszyn wirtualnych systemu Windows]
  * [Cennik maszyn wirtualnych systemu Linux]

Aby uzyskać więcej informacji o narzędzi Azure Java IDEs zobacz następujące zasoby:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [Nowości w zestawie narzędzi programu Azure dla programu Eclipse]
  * [Installing the Azure Toolkit for Eclipse] (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
  * [instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [Nowości w zestawie narzędzi programu Azure for IntelliJ]
  * [Installing the Azure Toolkit for IntelliJ] (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
  * [Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska Eclipse)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (Instalowanie zestawu narzędzi platformy Azure dla środowiska IntelliJ)
[instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Logowanie instrukcje dotyczące zestawu narzędzi Azure for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nowości w zestawie narzędzi programu Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nowości w zestawie narzędzi programu Azure for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

[Rozmiary maszyn wirtualnych systemu Windows na platformie Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Rozmiary maszyn wirtualnych systemu Linux na platformie Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Cennik maszyn wirtualnych systemu Windows]: /pricing/details/virtual-machines/windows/
[Cennik maszyn wirtualnych systemu Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
