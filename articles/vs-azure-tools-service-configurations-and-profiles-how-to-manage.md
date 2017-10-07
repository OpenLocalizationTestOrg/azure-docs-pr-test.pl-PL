---
title: "aaaHow toomanage usługi konfiguracji i profile | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toowork za pomocą plików konfiguracji usługi konfiguracji i profile | które ustawienia w środowiskach wdrożenia hello są przechowywane i ustawienia publikowania dla usługi w chmurze."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: 1dba9df2fa57fe94dacc90ae74b05ccdc28270c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-service-configurations-and-profiles"></a>Jak toomanage usługi konfiguracji i profili
## <a name="overview"></a>Omówienie
Po opublikowaniu usługi w chmurze programu Visual Studio przechowuje informacje o konfiguracji w dwa rodzaje pliki konfiguracji: usługa konfiguracji i profilów. Konfiguracja usługi (.cscfg pliki) przechowywania ustawień hello środowiska wdrażania usługi w chmurze Azure. Azure korzysta z tych plików konfiguracji podczas zarządzania usługi w chmurze. Na hello drugiej strony, profile (pliki .azurePubxml) magazynu ustawienia publikowania dla usługi w chmurze. Te ustawienia są rejestr wybierz używania hello Kreator publikowania i są używane lokalnie przez program Visual Studio. W tym temacie opisano sposób toowork z obu typów plików konfiguracyjnych.

## <a name="service-configurations"></a>Konfiguracja usługi
Można utworzyć wiele toouse konfiguracji usługi dla poszczególnych środowisk wdrażania. Może na przykład utworzyć konfigurację usługi dla środowiska lokalne powitania używanie toorun i testowania aplikacji Azure i inną konfigurację usługi dla środowiska produkcyjnego.

Można dodać, usunąć, Zmień nazwę i zmodyfikuj te konfiguracje usługi, w zależności od wymagań. Te konfiguracje usługi można zarządzać w programie Visual Studio, pokazane na następującej ilustracji hello.

![Zarządzanie konfiguracjami usługi](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

Można również otworzyć hello **Zarządzanie konfiguracjami** okno dialogowe z roli hello strony właściwości. właściwości hello tooopen rolę w projekcie platformy Azure, otwórz menu skrótów powitania dla tej roli, a następnie wybierz **właściwości**. Na powitania **ustawienia** karcie, rozwiń hello **konfiguracji usługi** listy, a następnie wybierz **Zarządzaj** tooopen hello **Zarządzanie konfiguracjami**okno dialogowe.

### <a name="tooadd-a-service-configuration"></a>tooadd konfigurację usługi
1. W Eksploratorze rozwiązań Otwórz menu skrótów hello hello Azure projektu, a następnie wybierz **Zarządzanie konfiguracjami**.
   
    Witaj **konfiguracji usługi zarządzania** zostanie wyświetlone okno dialogowe.
2. tooadd konfiguracji usługi, należy utworzyć kopię istniejącej konfiguracji. toodo, wybierz konfigurację hello mają toocopy z listy nazw hello, a następnie wybierz **utworzyć kopię**.
3. Wybierz z listy nazw hello hello nową konfigurację usługi konfiguracji usługi (opcjonalnie) toogive hello o innej nazwie, a następnie wybierz **zmienić**. W hello **nazwa** pole tekstowe, nazwa hello typu mają toouse dla tej konfiguracji usługi, a następnie wybierz **OK**.
   
    Nowy plik konfiguracji usługi o nazwie element ServiceConfiguration. [Nazwa nowego] .cscfg jest dodawany toohello Azure projekt w Eksploratorze rozwiązań.

### <a name="toodelete-a-service-configuration"></a>toodelete konfigurację usługi
1. W Eksploratorze rozwiązań Otwórz menu skrótów hello hello Azure projektu, a następnie wybierz **Zarządzanie konfiguracjami**.
   
    Witaj **konfiguracji usługi zarządzania** zostanie wyświetlone okno dialogowe.
2. toodelete konfiguracji usługi, wybierz hello konfiguracji, które mają toodelete z hello **nazwa** listy, a następnie wybierz **Usuń**. Okno dialogowe zostanie wyświetlone tooverify mają toodelete tej konfiguracji.
3. Wybierz pozycję **Usuń**.
   
     plik konfiguracji usługi Hello jest usuwany z hello Azure projekt w Eksploratorze rozwiązań.

### <a name="toorename-a-service-configuration"></a>toorename konfigurację usługi
1. W Eksploratorze rozwiązań Otwórz menu skrótów hello hello Azure projektu, a następnie wybierz **Zarządzanie konfiguracjami**.
   
    Witaj **konfiguracji usługi zarządzania** zostanie wyświetlone okno dialogowe.
2. toorename konfiguracji usługi, wybierz nową konfigurację usługi hello hello **nazwa** listy, a następnie wybierz **zmienić**. W hello **nazwa** pole tekstowe, nazwa hello typu mają toouse dla tej konfiguracji usługi, a następnie wybierz **OK**.
   
    Nazwa pliku konfiguracji usługi hello Hello zostanie zmieniona w hello Azure projekt w Eksploratorze rozwiązań.

### <a name="toochange-a-service-configuration"></a>toochange konfigurację usługi
* Jeśli chcesz toochange konfiguracji usługi, otwórz hello menu skrótów dla konkretnej roli hello mają toochange w hello Azure projektu, a następnie wybierz **właściwości**. Zobacz [porady: Konfigurowanie hello ról dla usługi w chmurze platformy Azure z programem Visual Studio](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) Aby uzyskać więcej informacji.

## <a name="make-different-setting-combinations-by-using-profiles"></a>Tworzenie ustawienie różnych kombinacji przy użyciu profili
Przy użyciu profilu, można automatycznie wypełnić hello **Kreator publikowania** z różną kombinacją możliwości ustawienia do różnych celów. Na przykład można mieć jeden profil debugowania i drugi dla wersji kompilacji. W takim przypadku Twojego **debugowania** byłyby profilu **IntelliTrace** włączona i hello **debugowania** zaznaczone, Konfiguracja i **wersji** Profil musi **IntelliTrace** wyłączone, a hello **wersji** Konfiguracja wybrana. Można również użyć toodeploy różnych profilów usługi przy użyciu innego konta magazynu.

Po uruchomieniu kreatora hello powitania po raz pierwszy, tworzony jest profil domyślny. Visual Studio przechowuje hello profil w pliku z rozszerzeniem nazwy .azurePubXml, która jest dodawana tooyour projektu platformy Azure w obszarze hello **profile** folderu. Jeśli po uruchomieniu kreatora hello później, ręcznie określić różne opcje, plik hello automatycznie aktualizacji. Przed uruchomieniem hello procedury powinna już opublikowany usługi w chmurze co najmniej raz.

### <a name="tooadd-a-profile"></a>tooadd profilu
1. Otwórz menu skrótów hello Azure projektu, a następnie wybierz **publikowania**.
2. Dalej toohello **docelowego profilu** listy, wybierz opcję hello **Zapisz profil** przycisk jako powitania po ilustracją. Spowoduje to utworzenie profilu dla Ciebie.
   
    ![Utwórz nowy profil](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. Po utworzeniu profilu hello, wybierz **< Zarządzaj >** w hello **docelowego profilu** listy.
   
    Witaj **zarządzania profilami** zostanie wyświetlone okno dialogowe jako powitania po ilustracją.
   
    ![Okno dialogowe Profile Zarządzanie](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. W hello **nazwa** listy, wybierz profil, a następnie wybierz **Utwórz kopię**.
5. Wybierz hello **Zamknij** przycisku.
   
    Hello nowy profil zostanie wyświetlony na liście hello docelowego profilu.
6. W hello **docelowego profilu** listy hello wybierz profil, który został utworzony. ustawienia kreatora Publikowanie Hello są wypełniane hello wybór z wybranego profilu hello.
7. Wybierz hello **Wstecz** i **dalej** przyciski toodisplay każdej stronie powitania Kreatora publikowania, a następnie dostosować ustawienia powitania dla tego profilu. Zobacz [Kreator publikowania aplikacji Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) informacji.
8. Po zakończeniu Dostosowywanie ustawień hello, wybierz **dalej** toogo toohello wstecz ustawienia strony. Profil Hello jest zapisany po opublikowaniu usługi hello przy użyciu tych ustawień lub w przypadku wybrania **zapisać** dalej toohello listy profilów.

### <a name="toorename-or-delete-a-profile"></a>toorename lub usuwanie profilu
1. Otwórz menu skrótów hello Azure projektu, a następnie wybierz **publikowania**.
2. W hello **docelowego profilu** listy, wybierz **Zarządzaj**.
3. W hello **zarządzania profilami** okno dialogowe, wybierz hello profilu mają toodelete, a następnie wybierz **Usuń**.
4. Okno dialogowe potwierdzenia hello, który pojawia się, wybierz **OK**.
5. Wybierz **Zamknij**.

### <a name="toochange-a-profile"></a>toochange profilu
1. Otwórz menu skrótów hello Azure projektu, a następnie wybierz **publikowania**.
2. W hello **docelowego profilu** listy hello wybierz profil, które mają toochange.
3. Wybierz hello **Wstecz** i **dalej** toodisplay hello każdej stronie Kreatora publikowania, a następnie zmień ustawienia hello ma przyciski. Zobacz [Kreator publikowania aplikacji Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) informacji.
4. Po zakończeniu zmiany ustawień hello, wybierz **dalej** toohello wstecz toogo **ustawienia** strony.
5. (Opcjonalnie) zaznacz **publikowania** usługi w chmurze hello toopublish przy użyciu nowych ustawień hello. Jeśli nie chcesz toopublish zamknąć usługi w chmurze w tym momencie, a hello Kreator publikowania, Visual Studio zapyta, jeśli chcesz toosave hello zmiany toohello profilu.

## <a name="next-steps"></a>Następne kroki
toolearn o konfigurowaniu innych części projektu platformy Azure w programie Visual Studio, zobacz [Konfigurowanie projektu platformy Azure](http://go.microsoft.com/fwlink/p/?LinkID=623075)

