---
title: "Witaj aaaInstalling zestawu narzędzi platformy Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall hello zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6c195fab2b47fb5c42541a8cf52be4ec88d27b5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-hello-azure-toolkit-for-eclipse"></a>Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse
Hello zestawu narzędzi platformy Azure dla programu Eclipse zawiera szablony i funkcje, które pozwalają tooeasily tworzenia, opracowanie, testowanie i wdrażanie aplikacji platformy Azure przy użyciu Środowisko deweloperskie Eclipse hello. zestaw narzędzi platformy Azure dla programu Eclipse Hello jest projekt typu Open Source. Kod źródłowy Hello jest dostępnych w ramach hello MIT licencji z <https://github.com/microsoft/azure-tools-for-java>.

Hello następujące kroki pokazują, jak tooinstall hello zestawu narzędzi platformy Azure dla programu Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="tooinstall-hello-azure-toolkit-for-eclipse"></a>Witaj tooinstall zestawu narzędzi platformy Azure dla programu Eclipse
1. Uruchom środowisko Eclipse.
2. Kliknij przycisk hello **pomocy** menu, a następnie kliknij przycisk **zainstalować nowe oprogramowanie**, jak pokazano na następującej ilustracji hello.
   
    ![Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][01]
3. W hello **dostępnego oprogramowania** okna dialogowego, w ramach hello **pracować z** polu tekstowym `http://dl.microsoft.com/eclipse` następuje hello **Enter** klucza.
4. W hello **nazwa** okienku wyboru **zestawu narzędzi platformy Azure dla programu Eclipse**i usuń zaznaczenie pola wyboru **skontaktuj się z wszystkich aktualizacji lokacji podczas instalacji oprogramowania wymagane toofind**. Na ekranie powinna zostać wyświetlona podobne toohello następujące czynności:
   
    ![Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][02]
5. Po rozwinięciu hello **zestawu narzędzi platformy Azure dla programu Eclipse**, zobaczysz hello następujące elementy:
   
   * **Wtyczka Insights aplikacji Java**: ten składnik umożliwia toouse Azure usługi rejestrowania i analizy danych telemetrycznych dla aplikacji i wystąpienia serwera.
   * **Azure filtr usługi kontroli dostępu**: ten składnik zapewnia obsługę uwierzytelniania użytkowników aplikacji przy użyciu usług Azure ACS, włączanie scenariuszy rejestracji jednokrotnej i jego oddzielenie logiki tożsamości od aplikacji hello.
   * **Azure wtyczki wspólnej**: ten składnik zapewnia hello często używane funkcje wymagane przez inne składniki zestawu narzędzi.
   * **Eksplorator systemu Azure dla programu Eclipse**: ten składnik zapewnia hello często używane funkcje wymagane przez inne składniki zestawu narzędzi.
   * **Azure dodatek dla programu Eclipse z językiem Java**: ten składnik zapewnia obsługę programowania projektów, które pomagają tworzenia, testowania i wdrażania aplikacji Java na powitania chmury Microsoft Azure w programie Eclipse i przy użyciu wiersza polecenia.
   * **Azure wtyczki aplikacji sieci Web z językiem Java**: ten składnik zapewnia obsługę wdrażania kontenery tooMicrosoft aplikacji Java sieci web w aplikacji sieci Web platformy Azure.
   * **4.2 sterownik JDBC firmy Microsoft dla programu SQL Server**: ten składnik zapewnia JDBC interfejsu API programu SQL Server i bazy danych SQL Azure firmy Microsoft dla języka Java platformy Enterprise Edition 8.
   * **Pakiet Apache Qpid bibliotek klienta JMS**: ten składnik zapewnia składnik klienta JMS hello z hello Apache Qpid projektu tooenable Twojej aplikacji toouse AMQP wiadomości w Microsoft Azure.
   * **Pakiet dla bibliotek usługi Microsoft Azure dla języka Java**: ten składnik udostępnia interfejsy API do uzyskiwania dostępu do usług Microsoft Azure, takich jak magazyn, usługi service bus, czas wykonywania usługi itp.
6. Kliknij przycisk **Dalej**. (Jeśli opóźnień nietypowe podczas instalowania zestawu narzędzi hello, upewnij się, że **skontaktuj się z wszystkich aktualizacji lokacji podczas instalacji oprogramowania wymagane toofind** nie jest zaznaczone.)
7. W hello **zainstalować szczegóły** okna dialogowego, kliknij przycisk **dalej**.
   
    ![Przejrzyj szczegóły instalacji][03]
8. W hello **Przejrzyj licencji** okna dialogowego, zapoznaj się warunkami hello hello umów licencyjnych. Jeśli akceptujesz postanowienia hello hello umów licencyjnych, kliknij przycisk **hello postanowienia Umowy licencyjnej hello** , a następnie kliknij przycisk **Zakończ**. (pozostałe kroki hello przyjęto założenie, że akceptujesz warunki hello hello umów licencyjnych. Jeśli nie zaakceptujesz postanowień hello hello umów licencyjnych, Zakończ proces instalacji hello.)
   
    ![Przegląd licencji][04]
   
    Eclipse pobierze i zainstaluje hello wymagane pakiety.
   
    ![Postęp instalacji][05]
9. Jeśli zostanie wyświetlony monit toorestart Eclipse toocomplete instalacji, kliknij przycisk **tak**.
   
    ![Uruchom ponownie wiersza][06]

## <a name="see-also"></a>Zobacz też
Aby uzyskać więcej informacji na temat hello narzędzi Azure dla języka Java IDEs Zobacz hello następującego łącza:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * *Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse (w tym artykule)*
  * [Zaloguj się w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [Nowości w hello Azure Toolkit for IntelliJ]
  * [Instalowanie hello Azure Toolkit for IntelliJ]
  * [Zaloguj się w instrukcji hello Azure Toolkit for IntelliJ]
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center].

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Zaloguj się w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Zaloguj się w instrukcji hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nowości w hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
