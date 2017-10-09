---
title: "Dodatek dla programu Eclipse sieci szkieletowej usług aaaAzure | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z hello wtyczki sieci szkieletowej usług dla programu Eclipse."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>Wtyczka usługi Service Fabric na potrzeby tworzenia aplikacji Java w środowisku Eclipse
Środowisko Eclipse jest jednym z hello najczęściej używane zintegrowane środowisk deweloperskich (IDE) dla deweloperów języka Java. W tym artykule opisano sposób tooset się toowork środowisko rozwoju Eclipse, tak z sieci szkieletowej usług Azure. Dowiedz się, jak utworzyć aplikację sieci szkieletowej usług hello tooinstall wtyczki sieci szkieletowej usług i wdrażanie z sieci szkieletowej usług aplikacji tooa lokalnego lub zdalnego klastra sieci szkieletowej usług w środowisku Eclipse Neon.

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a>Zainstaluj lub zaktualizuj hello wtyczki w środowisku Eclipse Neon sieci szkieletowej usług
W środowisku Eclipse można zainstalować wtyczkę usługi Service Fabric. Wtyczka Hello może ułatwić proces hello tworzenie i wdrażanie usług Java.

1.  Upewnij się, czy masz najnowszą wersję programu Eclipse Neon hello i hello najnowszą wersję Buildship zainstalowany (1.0.17 lub nowszy):
    -   toocheck hello wersje zainstalowanych składników w Eclipse Neon Przejdź zbyt**pomocy** > **szczegółowe informacje dotyczące instalacji**.
    -   Zobacz tooupdate Buildship, [Eclipse Buildship: Eclipse wtyczek dla narzędzia Gradle][buildship-update].
    -   toocheck dla i instalacja aktualizacji dla programu Eclipse Neon, go za**pomocy** > **Sprawdź aktualizacje**.

2.  tooinstall hello usługi sieć szkieletowa wtyczki w Eclipse Neon Przejdź zbyt**pomocy** > **zainstalować nowe oprogramowanie**.
  1.    W hello **pracować z** wprowadź **http://dl.microsoft.com/eclipse**.
  2.    Kliknij pozycję **Dodaj**.

         ![Wtyczka usługi Service Fabric dla środowiska Eclipse Neon][sf-eclipse-plugin-install]
  3.    Wybierz hello wtyczki sieci szkieletowej usług, a następnie kliknij przycisk **dalej**.
  4.    Wykonaj kroki instalacji hello, a następnie zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft hello.

Jeśli masz już hello usługi sieć szkieletowa wtyczki zainstalowane, upewnij się, że masz hello najnowszej wersji. toocheck dostępnych aktualizacji, przejdź zbyt**pomocy** > **szczegółowe informacje dotyczące instalacji**. Witaj listy zainstalowanych wtyczek, wybierz sieć szkieletowa usług, a następnie kliknij **aktualizacji**. Dostępne aktualizacje zostaną zainstalowane.

> [!NOTE]
> Jeśli instalację lub aktualizację hello wtyczki sieci szkieletowej usług przebiega powoli, może to być spowodowane tooan Eclipse ustawienie. Eclipse zbiera metadanych we wszystkich lokacjach tooupdate zmiany, które są zarejestrowane z wystąpieniem programu Eclipse. toospeed proces hello wyszukiwanie i instalowanie aktualizacji wtyczki w sieci szkieletowej usług Przejdź zbyt**dostępnych lokacji oprogramowania**. Usuń zaznaczenie pól wyboru hello dla wszystkich lokacji, z wyjątkiem hello, który wskazuje lokalizację wtyczki toohello sieci szkieletowej usług (http://dl.microsoft.com/eclipse/azure/servicefabric).

## <a name="create-a-service-fabric-application-in-eclipse"></a>Tworzenie aplikacji usługi Service Fabric w środowisku Eclipse

1.  Eclipse Neon zbyt Przejdź**pliku** > **nowy** > **innych**. Wybierz pozycję **Service Fabric Project** (Projekt usługi Service Fabric), a następnie kliknij przycisk **Next** (Dalej).

    ![Nowy projekt usługi Service Fabric — strona 1][create-application/p1]

2.  Wprowadź nazwę projektu, a następnie kliknij przycisk **Next** (Dalej).

    ![Nowy projekt usługi Service Fabric — strona 2][create-application/p2]

3.  Witaj listy szablonów, wybierz **szablonu usługi**. Wybierz typ szablonu usługi — Actor (Aktor), Stateless (Bezstanowa), Container (Kontener) lub Guest Binary (Binarna gościa) — a następnie kliknij przycisk **Next** (Dalej).

    ![Nowy projekt usługi Service Fabric — strona 3][create-application/p3]

4.  Wprowadź nazwę usługi hello i szczegóły dotyczące usługi, a następnie kliknij przycisk **Zakończ**.

    ![Nowy projekt usługi Service Fabric — strona 4][create-application/p4]

5. Po utworzeniu pierwszego projektu sieci szkieletowej usług, hello **perspektywy skojarzonych Otwórz** okno dialogowe, kliknij przycisk **tak**.

    ![Nowy projekt usługi Service Fabric — strona 5][create-application/p5]

6.  Nowy projekt wygląda następująco:

    ![Nowy projekt usługi Service Fabric — strona 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>Kompilowanie i wdrażanie aplikacji usługi Service Fabric w środowisku Eclipse

1.  Kliknij prawym przyciskiem myszy nową aplikację usługi Service Fabric, a następnie wybierz polecenie **Service Fabric**.

    ![Menu prawego przycisku myszy usługi Service Fabric][publish/RightClick]

2. Wybierz odpowiednią opcję hello podmenu hello:
    -   Aplikacja hello toobuild bez czyszczenia, kliknij przycisk **kompilacji aplikacji**.
    -   Kliknij przycisk toodo czystą kompilację aplikacji hello **odbudować aplikacji**.
    -   Kliknij aplikacji hello tooclean wbudowanych artefaktów **czystą aplikacji**.

3.  To menu umożliwia także wdrożenie, cofnięcie wdrożenia i opublikowanie aplikacji:
    -   Klaster lokalny tooyour toodeploy, kliknij przycisk **wdrażanie aplikacji**.
    -   W hello **publikowania aplikacji** oknie dialogowym Wybierz profil publikowania:
        -  **Local.json**
        -  **Cloud.json**

     Te pliki JavaScript Object Notation (JSON) przechowywania informacji (takich jak punkty końcowe połączenia i informacji o zabezpieczeniach), która jest wymagana tooconnect tooyour lokalnego lub w klastrze chmury (Azure).

  ![Menu publikowania usługi Service Fabric][publish/Publish]

Toodeploy alternatywny sposób aplikacji sieci szkieletowej usług za pomocą programu Eclipse uruchomieniu konfiguracje.

  1.    Przejdź za**Uruchom** > **konfiguracje wykonywania**.
  2.    W obszarze **projektu Gradle**, wybierz pozycję hello **ServiceFabricDeployer** Uruchom konfigurację.
  3.    W prawym okienku hello na powitania **argumenty** karcie dla **publishProfile**, wybierz pozycję **lokalnego** lub **chmury**.  Domyślnie Hello **lokalnego**. tooa toodeploy zdalnego lub chmury klastra, wybierz opcję **chmury**.
  4.    tooensure czy hello odpowiednie informacje są umieszczane w hello profilów publikowania, Edytuj **Local.json** lub **Cloud.json** zgodnie z potrzebami. Możesz dodać lub zaktualizować szczegóły punktu końcowego i poświadczenia zabezpieczeń.
  5.    Upewnij się, że **katalog roboczy** punktów toohello aplikacji ma toodeploy. toochange hello aplikacji, kliknij przycisk hello **obszaru roboczego** przycisk, a następnie wybierz aplikację hello.
  6.    Kliknij przycisk **Apply** (Zastosuj), a następnie kliknij przycisk **Run** (Uruchom).

Aplikacja zostanie skompilowana i wdrożona w ciągu kilku minut. Można monitorować stan wdrożenia hello w narzędziu Service Fabric Explorer.  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a>Dodaj tooyour usługi sieć szkieletowa usług aplikacji sieci szkieletowej usług

tooadd sieci szkieletowej usług tooan istniejącej sieci szkieletowej usług aplikacji usługi, hello następujące kroki:

1.  Kliknij prawym przyciskiem myszy hello projektu mają tooadd usługi, a następnie kliknij przycisk **sieci szkieletowej usług**.

    ![Dodawanie usługi Service Fabric — strona 1][add-service/p1]

2.  Kliknij przycisk **dodać Usługa sieci szkieletowej usług**, i hello pełny zestaw tooadd kroki projekt toohello usługi.
3.  Hello wybierz szablon usługi ma tooadd tooyour projektu, a następnie kliknij przycisk **dalej**.

    ![Dodawanie usługi Service Fabric — strona 2][add-service/p2]

4.  Wprowadź nazwę usługi hello (i inne szczegóły, w razie potrzeby), a następnie kliknij przycisk hello **Dodaj usługę** przycisku.  

    ![Dodawanie usługi Service Fabric — strona 3][add-service/p3]

5.  Po dodaniu usługi hello ogólną strukturę projektu wygląda podobnie toohello następującego projektu:

    ![Dodawanie usługi Service Fabric — strona 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a>Edytowanie wersji manifestu aplikacji Java usługi Service Fabric

tooedit wersji manifestu, kliknij prawym przyciskiem myszy projekt hello, przejdź zbyt**sieci szkieletowej usług** i wybierz **edytować wersji manifestu...**  z hello menu rozwijanym. W Kreatorze hello można aktualizować hello wersji manifestu dla manifest usługi manifestu, aplikacji i wersji hello **kod**, **Config** i **danych** pakietów.

Jeśli zaznaczysz opcję hello **automatycznie Aktualizuj wersje aplikacji i usługi** , a następnie zaktualizuj wersję, następnie wersji manifestu hello zostanie automatycznie zaktualizowana. toogive przykładem, należy najpierw wybrać hello pole wyboru, a następnie aktualizacji wersji hello **kod** wersji z 0.0.0 too0.0.1 i kliknij pozycję **Zakończ**, następnie usługi wersji manifestu i manifest aplikacji wersja będzie too0.0.1 automatycznie aktualizowane.

## <a name="upgrade-your-service-fabric-java-application"></a>Uaktualnianie aplikacji Java usługi Service Fabric

Scenariusz uaktualnienia, powiedz utworzone hello **App1** projektu przy użyciu hello wtyczki w środowisku Eclipse sieci szkieletowej usług. Wdrożono go za pomocą wtyczki toocreate hello aplikacji o nazwie **fabric: / App1Application**. Typ aplikacji Hello jest **App1AppicationType**, i wersja aplikacji hello jest 1.0. Teraz ma tooupgrade aplikacji bez zakłócania ich dostępności.

Najpierw należy wprowadzać żadnych zmian w aplikacji tooyour i skompiluj go ponownie zmodyfikować hello usługi. Aktualizacja hello modyfikacji pliku manifestu usługi (ServiceManifest.xml) z hello zaktualizowane wersje hello usługi (i kodu, konfiguracji lub danych w formie odpowiednich). Ponadto zmodyfikuj manifest aplikacji hello (ApplicationManifest.xml) z numerem wersji hello zaktualizowane dla aplikacji hello i hello modyfikacji usługi.  

tooupgrade aplikacji przy użyciu Eclipse Neon, możesz utworzyć profil zduplikowane wykonywania konfiguracji. Następnie należy użyć go tooupgrade aplikacji zgodnie z potrzebami.

1.  Przejdź za**Uruchom** > **konfiguracje wykonywania**. W okienku po lewej stronie powitania kliknij hello małą strzałkę toohello lewej strony **projektu Gradle**.
2.  Kliknij prawym przyciskiem myszy pozycję **ServiceFabricDeployer** i wybierz polecenie **Duplicate** (Duplikuj). Wprowadź nową nazwę dla tej konfiguracji, na przykład **ServiceFabricUpgrader**.
3.  W prawym panelu hello na powitania **argumenty** Zmień **- Pconfig = "wdrażania"** za**- Pconfig = "Uaktualnij"**, a następnie kliknij przycisk **Zastosuj**.

Ten proces tworzy i zapisuje profil uruchamiania konfiguracji można w dowolnym tooupgrade czasu aplikacji. Zapewnia również hello najnowsze wersje typu aplikacji zaktualizowane z pliku manifestu aplikacji hello.

Uaktualnianie aplikacji Hello zajmuje kilka minut. Można monitorować hello uaktualniania aplikacji w narzędziu Service Fabric Explorer.

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Migrowanie starego toobe aplikacji Java sieci szkieletowej usług używany z Maven
Biblioteki usługi sieć szkieletowa Java niedawno został przeniesiony z repozytorium tooMaven zestawu SDK Java sieci szkieletowej usług. Gdy hello nowe aplikacje, które można wygenerować za pomocą programu Eclipse, spowoduje wygenerowanie najnowsze zaktualizowane projekty (które będą mogli toowork z Maven), można aktualizacji istniejącej sieci szkieletowej usług bezstanowych lub aplikacji Java aktora, które były używane hello zestawu SDK Java sieci szkieletowej usług wcześniej, toouse hello usługi sieć szkieletowa Java zależności z Maven. Wykonaj kroki hello wymienione [tutaj](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure starszych aplikacji współdziała z Maven.

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
