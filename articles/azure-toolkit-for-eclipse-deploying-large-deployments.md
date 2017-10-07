---
title: "aaaDeploying dużych wdrożeń"
description: "Dowiedz się, jak toodeploy dużych wdrożeń za pomocą hello zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a>Wdrażanie dużych wdrożeń
Wdrożenie jest zbyt duży toobe znajdujące się w folderze approot domyślne hello, można użyć zasobów magazynu lokalnego jako folder główny wdrożenia hello, dla Twojej JDK i serwera aplikacji.

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>toouse zasobu magazynu lokalnego jako folder główny wdrożenia hello w przypadku dużych wdrożeń
1. Tworzenie nowego zasobu magazynu lokalnego. Nazwa Hello hello zasobu nie ma znaczenia. Zasoby magazynu są definiowane na poziomie roli hello. Witaj najszybszy sposób tooaccess hello Magazyn lokalny okna dialogowego konfiguracji, w którym można utworzyć nowego zasobu lokalnego magazynu polega na użyciu hello następujące kroki: kliknij prawym przyciskiem myszy rolę hello w hello **Eksplorator projektów** widoku (rozwiń węzeł sieci Azure węzła projektu, jeśli nie widzisz roli hello), kliknij przycisk **Azure**, a następnie kliknij przycisk **Magazyn lokalny**. W ramach hello **Magazyn lokalny** okna dialogowego, kliknij przycisk **Dodaj** toocreate nowego zasobu magazynu lokalnego.

2. Witaj zestaw żądaną tooat rozmiar co najmniej 2048 MB (niczego mniej może powodować hello takie same problemy rozmiar pliku, ponieważ może wystąpić w hello approot).

3. Upewnij się, że **wyczyścić zawartość hello podczas odtwarzania wystąpienia roli hello** zaznaczono; może to pomóc w zabezpieczeniu Logika uruchamiania wdrożenia hello z systemem Windows powoduje konflikt z istniejące pliki w zasobie hello po hello roli wystąpienie zostanie odtworzony.

4. Upewnij się, że hello **przechowywania zmiennych środowiska hello ścieżki katalogu zasobu po wdrożeniu** wartość ciągu toohello **DEPLOYROOT**. Twoje okno dialogowe zasobu lokalnego magazynu będzie wyglądać podobnie następujące toohello.

   ![][ic667943]

Alternatywnie Jeśli używasz **DEPLOYROOT** jako hello *nazwa* zasobu lokalnego, a nie należy zmieniać nazwę zmiennej środowiskowej generowane automatycznie hello (której będzie można ustawić za **DEPLOYROOT_PATH** w takim przypadku), który będzie działać również aplikacji.

Dodatkowe informacje na temat tworzenia zasobu lokalnego magazynu można znaleźć w folderze [właściwości magazynu lokalnego][Local storage properties].

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse] 

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
