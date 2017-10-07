---
title: "aaaManage kont magazynu przy użyciu hello Azure Explorer for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage magazyn Azure kont za pomocą hello Azure Explorer for IntelliJ."
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
ms.openlocfilehash: b094bdcd2fa2782cb12b67c96ac406fbe4c1aa3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a>Zarządzanie kontami magazynu przy użyciu hello Azure Explorer for IntelliJ

Hello Azure Eksploratora, będący częścią hello Azure Toolkit for IntelliJ zapewnia Java deweloperom łatwe w użyciu rozwiązanie do zarządzania kontami magazynu na koncie Azure z wewnątrz hello IntelliJ zintegrowane środowisko programistyczne (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Utwórz konto magazynu w IntelliJ

Konto magazynu przy użyciu Eksploratora Azure hello toocreate hello następujące:

1. Zaloguj się tooyour konto platformy Azure przy użyciu hello [instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]. 

2. W hello **Eksploratora Azure** wyświetlić, rozwiń węzeł hello **Azure** węzła, kliknij prawym przyciskiem myszy **kont magazynu**, a następnie kliknij przycisk **Utwórz konto magazynu**.

   ![Utwórz konto magazynu, polecenie][CS01]

3. W hello **Utwórz konto magazynu** oknie dialogowym Określ hello następujące opcje:

   ![Tworzenie nowego konta magazynu, okno dialogowe][CS02]

   * **Nazwa**: Określa nazwę hello hello nowe konto magazynu.

   * **Konto rodzaju**: Określa typ hello toocreate konta magazynu (na przykład "magazynu obiektów Blob"). Aby uzyskać więcej informacji, zobacz [kont magazynu Azure o]. 

   * **Wydajność**: Określa konto magazynu, które oferty toouse hello wybranego wydawcy (na przykład "Premium"). Aby uzyskać więcej informacji, zobacz [elementy docelowe skalowalności i wydajności magazynu Azure]. 

   * **Replikacja**: Określa hello replikacji dla konta magazynu hello (na przykład "Strefowo nadmiarowy"). Aby uzyskać więcej informacji, zobacz [replikacji usługi Azure storage]. 

   * **Subskrypcja**: Określa hello mają toouse dla nowego konta magazynu hello subskrypcji platformy Azure.

   * **Lokalizacja**: Określa lokalizację hello, w której zostanie utworzona konta magazynu (na przykład "Zachodnie nam").

   * **Grupa zasobów**: Określa hello grupy zasobów dla maszyny wirtualnej. Wybierz jedną z hello następujące opcje:
      * **Utwórz nowe**: Określa, że toocreate nową grupę zasobów.
      * **Użyj istniejącego**: Określa, czy będzie wybierz z listy grup zasobów, które są skojarzone z kontem usługi Azure.

4. Po określeniu wszystkie hello poprzedzających opcje, kliknij przycisk **OK**.

## <a name="create-a-storage-container-in-intellij"></a>Tworzenie kontenera magazynu w IntelliJ

toocreate kontener magazynu przy użyciu Eksploratora Azure hello hello następujące:

1. W widoku Eksploratora Azure hello, kliknij prawym przyciskiem myszy konto magazynu hello, gdzie mają toocreate kontener, a następnie kliknij przycisk **Tworzenie kontenera obiektów blob**.

   ![Utwórz polecenie kontenera obiektów blob][CC01]

2. W hello **Tworzenie kontenera obiektów blob** okno dialogowe, określ nazwę hello z kontenera, a następnie kliknij **OK**. Aby uzyskać więcej informacji o nazwach kontenery magazynu, zobacz [nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych].

   ![Tworzenie kontenera magazynu, okno dialogowe][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Usuń kontener magazynu w IntelliJ

toodelete kontener magazynu przy użyciu Eksploratora Azure hello hello następujące:

1. W widoku Eksploratora Azure hello, kliknij prawym przyciskiem myszy kontener magazynu hello, a następnie kliknij przycisk **usunąć**.

   ![Usuń polecenie kontenera magazynu][DC01]

2. W oknie potwierdzenia powitania kliknij **tak**.

   ![Usuń okno potwierdzenia kontenera magazynu][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Usuwanie konta magazynu w IntelliJ

Konto magazynu przy użyciu Eksploratora Azure hello toodelete hello następujące:

1. W hello **Eksploratora Azure** wyświetlić, kliknij prawym przyciskiem myszy konto magazynu hello, a następnie wybierz **usunąć**.

   ![Usuwanie z menu konta magazynu][DS01]

2. W oknie potwierdzenia powitania kliknij **tak**.

   ![Usuń okno potwierdzenia konta magazynu][DS02]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o kontach magazynu Azure rozmiary i cenach, zobacz następujące zasoby hello:

* [Wprowadzenie tooMicrosoft usługi Azure Storage]
* [kont magazynu Azure o]
* Rozmiary konto usługi Azure storage
  * [Rozmiary dla konta magazynu systemu Windows na platformie Azure]
  * [Rozmiary dla konta magazynu w systemie Linux na platformie Azure]
* Konto usługi Azure storage — cennik
  * [Cennik konta magazynu systemu Windows]
  * [Cennik konta magazynu systemu Linux]

Aby uzyskać więcej informacji na temat narzędzi Azure dla języka Java IDEs Zobacz hello następujące zasoby:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [What's new in hello Azure Toolkit for IntelliJ]
  * [Instalowanie hello Azure Toolkit for IntelliJ]
  * [Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center] i [Java Tools for Visual Studio Team Services].

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's new in hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

[Wprowadzenie tooMicrosoft usługi Azure Storage]: /azure/storage/storage-introduction
[kont magazynu Azure o]: /azure/storage/storage-create-storage-account
[replikacji usługi Azure storage]: /azure/storage/storage-redundancy
[Cele dotyczące wydajności i skalowalności magazynu Azure]: /azure/storage/storage-scalability-targets
[nazewnictwa i odwołuje się do kontenerów, obiektów blob i metadanych]: http://go.microsoft.com/fwlink/?LinkId=255555

[Rozmiary dla konta magazynu systemu Windows na platformie Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Rozmiary dla konta magazynu w systemie Linux na platformie Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Cennik konta magazynu systemu Windows]: /pricing/details/virtual-machines/windows/
[Cennik konta magazynu systemu Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
