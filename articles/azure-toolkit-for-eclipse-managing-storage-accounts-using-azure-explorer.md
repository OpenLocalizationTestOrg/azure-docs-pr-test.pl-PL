---
title: "Zarządzanie kontami magazynu przy użyciu Eksploratora Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać kontami magazynu Azure za pomocą Eksploratora Azure dla programu Eclipse."
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
ms.openlocfilehash: 5b3014b5aca368be8ea46863c83665abde10fed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a>Zarządzanie kontami magazynu przy użyciu Eksploratora Azure dla programu Eclipse

Eksploratora Azure, która jest częścią zestawu narzędzi platformy Azure dla programu Eclipse, oferuje Java deweloperom łatwe w użyciu rozwiązanie do zarządzania kontami magazynu Azure konta od wewnątrz Eclipse zintegrowane środowisko programistyczne (IDE).

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a>Utwórz konto magazynu w środowisku Eclipse

Aby utworzyć konto magazynu przy użyciu Eksploratora Azure, wykonaj następujące czynności:

1. Zaloguj się do konta platformy Azure przy użyciu [instrukcje logowania dla zestawu narzędzi platformy Azure dla programu Eclipse].

2. W **Eksploratora Azure** wyświetlić, rozwiń węzeł **Azure** węzła, kliknij prawym przyciskiem myszy **kont magazynu**, a następnie kliknij przycisk **Utwórz konto magazynu**.

   ![Utwórz konto magazynu, polecenie][CS01]

3. W **Utwórz konto magazynu** oknie dialogowym określ następujące opcje:

   ![Tworzenie nowego konta magazynu, okno dialogowe][CS02]

   * **Nazwa**: Określa nazwę dla nowego konta magazynu.

   * **Subskrypcja**: Określa subskrypcji Azure, która ma być używany dla nowego konta magazynu.

   * **Grupa zasobów**: Określa grupę zasobów dla maszyny wirtualnej. Wybierz jedną z następujących opcji:
      * **Utwórz nowy**: Określa, czy chcesz utworzyć nową grupę zasobów.
      * **Użyj istniejącego**: Określa, czy będzie wybierz z listy grup zasobów, które są skojarzone z kontem usługi Azure.

   * **Region**: Określa lokalizację, w której zostanie utworzona konta magazynu (na przykład "Zachodnie nam").

   * **Konto rodzaju**: Określa typ konta magazynu (na przykład "Magazynu obiektów Blob"). Aby uzyskać więcej informacji, zobacz [kont magazynu Azure o].

   * **Wydajność**: Określa konto magazynu, które oferty do użycia z wybranego wydawcy (na przykład "Premium"). Aby uzyskać więcej informacji, zobacz [elementy docelowe skalowalności i wydajności magazynu Azure].

   * **Replikacja**: Określa replikacji dla konta magazynu (na przykład "Strefowo nadmiarowy"). Aby uzyskać więcej informacji, zobacz [replikacji usługi Azure storage].

4. Po określeniu wszystkich powyższych opcji kliknij przycisk **Utwórz**.

## <a name="create-a-storage-container-in-eclipse"></a>Tworzenie kontenera magazynu w środowisku Eclipse

Aby utworzyć kontener magazynu przy użyciu Eksploratora Azure, wykonaj następujące czynności:

1. W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy konto magazynu, w którym chcesz utworzyć kontener, a następnie kliknij przycisk **Tworzenie kontenera obiektów blob**.

   ![Utwórz polecenie kontenera obiektów blob][CC01]

2. W **Tworzenie kontenera obiektów blob** okno dialogowe, określ nazwę użytkownika kontenera, a następnie kliknij **OK**. Aby uzyskać więcej informacji o nazwach kontenery magazynu, zobacz [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych].

   ![Tworzenie kontenera obiektów blob, okno dialogowe][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a>Usuń kontener magazynu w środowisku Eclipse

Aby usunąć kontenera magazynu przy użyciu Eksploratora Azure, wykonaj następujące czynności:

1. W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy kontener magazynu, a następnie kliknij przycisk **usunąć**.

   ![Usuń polecenie kontenera magazynu][DC01]

2. W oknie potwierdzenia kliknij **OK**.

   ![Usuń okno potwierdzenia kontenera magazynu][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a>Usuwanie konta magazynu w środowisku Eclipse

Aby usunąć konto magazynu przy użyciu Eksploratora Azure, wykonaj następujące czynności:

1. W **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy konto magazynu, a następnie kliknij przycisk **usunąć**.

   ![Usuń polecenie konta magazynu][DS01]

2. W oknie potwierdzenia kliknij **OK**.

   ![Usuń okno potwierdzenia konta magazynu][DS02]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o kontach magazynu Azure rozmiarów i cenach, zobacz następujące zasoby:

* [Wprowadzenie do usługi Microsoft Azure Storage]
* [kont magazynu Azure o]
* Rozmiary konto usługi Azure storage
  * [Rozmiary dla konta magazynu systemu Windows na platformie Azure]
  * [Rozmiary dla konta magazynu w systemie Linux na platformie Azure]
* Konto usługi Azure storage — cennik
  * [Cennik konta magazynu systemu Windows]
  * [Cennik konta magazynu systemu Linux]

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

[Wprowadzenie do usługi Microsoft Azure Storage]: /azure/storage/storage-introduction
[kont magazynu Azure o]: /azure/storage/storage-create-storage-account
[replikacji usługi Azure storage]: /azure/storage/storage-redundancy
[Cele dotyczące wydajności i skalowalności magazynu Azure]: /azure/storage/storage-scalability-targets
[nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych]: http://go.microsoft.com/fwlink/?LinkId=255555

[Rozmiary dla konta magazynu systemu Windows na platformie Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Rozmiary dla konta magazynu w systemie Linux na platformie Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Cennik konta magazynu systemu Windows]: /pricing/details/virtual-machines/windows/
[Cennik konta magazynu systemu Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
