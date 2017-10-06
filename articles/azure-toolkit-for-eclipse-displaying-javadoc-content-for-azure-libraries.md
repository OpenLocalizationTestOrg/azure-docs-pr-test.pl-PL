---
title: "aaaDisplaying Javadoc zawartości w programie Eclipse dla hello pakietu biblioteki Azure dla języka Java"
description: "Jak toodisplay hello Javadoc zawartości dla biblioteki Azure hello w środowisku Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a>Wyświetlanie zawartości Javadoc w środowisku Eclipse hello pakietu biblioteki Azure dla języka Java
Witaj Javadoc zawartość hello biblioteki Azure dla języka Java można wyświetlić w środowisku Eclipse kojarząc hello Javadoc zawartości toohello biblioteki Azure dla języka Java. Witaj poniższej procedurze pokazano, jak toouse tę funkcję w środowisku Eclipse.

W tej procedurze przyjęto założenie, że dodano już hello biblioteki Azure dla ścieżki kompilacji tooyour Java.

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a>toodisplay Javadoc zawartość w programie Eclipse hello biblioteki Azure dla języka Java
* W środowisku Eclipse w Eksploratorze projektu w hello **odwołuje się do bibliotek** hello Otwórz menu kontekstowe dla hello biblioteki Azure dla programu Java JAR, sekcji projektu. Na przykład **microsoft-windowsazure-api-0.1.0.jar** (numer wersji hello mogą być różne, w zależności od wersji zainstalowane).

* Kliknij pozycję **Właściwości**.

* W ramach hello **właściwości** okna dialogowego, w okienku po lewej stronie powitania kliknij **lokalizacji Javadoc**. Witaj **lokalizacji Javadoc** zostanie wyświetlone okno dialogowe.

* Można określić **Javadoc URL**, lub **Javadoc w archiwum**.

   * Jeśli wybierzesz toospecify **Javadoc URL**, takich jak używać adresów URL hello **http://dl.windowsazure.com/javadoc** lub **http://dl.windowsazure.com/storage/javadoc**.

   * Jeśli wybierzesz toouse **Javadoc w archiwum**, można określić plik lub pliku obszaru roboczego.

   Wybierz ustawienia i przeglądania/sprawdzanie poprawności stosownie do potrzeb. Witaj poniższy przykład kojarzy hello biblioteki Azure dla języka Java z hello odpowiedniego Javadoc JAR której pobierana lokalnie tooa folder o nazwie **c:\MyAzureJARs**.

   ![][ic553487]

* *Krok opcjonalny*: kliknij **zweryfikować**. Potencjalne problemy z hello Javadoc JAR mogą być wyświetlone tutaj.

* Kliknij przycisk **OK**.

Po skojarzonych z biblioteką hello, hello zawartości Javadoc powinien być wyświetlany w środowiskiem Eclipse IDE. Na przykład jeśli `blob` zdefiniowano typu `CloudBlockBlob` w kodzie, hello poniżej przedstawiono przykład Javadoc zawartość, która pojawia się po wpisaniu `blob.acquireLease` w kodzie:

![][ic553488]

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

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
