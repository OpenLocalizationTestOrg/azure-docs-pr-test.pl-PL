---
title: "aaaAdd laboratorium tooa repozytorium Git w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Dodawanie źródła niestandardowe artefakty repozytorium GitHub lub Visual Studio Team Services Git w usłudze Azure DevTest Labs"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>Dodaj Git artefakty niestandardowych toostore repozytorium i szablony usługi Azure Resource Manager

Jeśli chcesz zbyt[Tworzenie niestandardowych artefaktów](devtest-lab-artifact-author.md) dla hello maszyn wirtualnych w laboratorium, lub [toocreate szablonów usługi Azure Resource Manager środowiska testowego niestandardowych użyj](devtest-lab-create-environment-from-arm.md), musisz również dodać prywatnej tooinclude repozytorium Git Artefakty Hello lub szablonów usługi Azure Resource Manager, które tworzy zespołu. Witaj repozytorium może być hostowana na [GitHub](https://github.com) lub na [programu Visual Studio Team Services (VSTS)](https://visualstudio.com).

Firma Microsoft umieściła [repozytorium Github artefaktów](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) wdrażanego jako — jest lub Dostosuj w laboratoriach użytkownika. Podczas dostosowywania lub tworzenia artefaktu, nie można zapisać je w repozytorium publicznych hello — należy utworzyć własne prywatne repozytorium. 

Podczas tworzenia maszyny Wirtualnej, można zapisać szablon usługi Azure Resource Manager hello, dostosować go, jeśli, a następnie użyć jej nowszych tooeasily utworzyć więcej maszyn wirtualnych. Musisz utworzyć własne toostore prywatnym repozytorium szablonów niestandardowych usługi Azure Resource Manager.  

* toolearn toocreate repozytorium GitHub, zobacz temat [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).
* toolearn toocreate projekt usługi Team Services z repozytorium Git, zobacz temat [połączyć tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).

Witaj Poniższy zrzut ekranu przedstawia przykład repozytorium zawierający artefakty może wyglądać w witrynie GitHub:  
![Przykładowe repozytorium artefaktów GitHub](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>Pobierz informacje o repozytorium hello i poświadczenia
tooadd laboratorium tooyour repozytorium, należy najpierw pobrać niektóre informacje z repozytorium. Witaj następujące sekcje zawierają informacje pomocne przy pobranie tych informacji dla repozytoriów hostowanych w usłudze GitHub i Visual Studio Team Services.

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>Uzyskaj token dostępu osobistych i URL klonowania repozytorium GitHub hello
adres URL klonowania repozytorium GitHub hello tooget i osobistego tokenu dostępu, wykonaj następujące kroki:

1. Przejdź na stronę główną toohello repozytorium GitHub hello zawierający artefaktu hello lub definicje szablonów usługi Azure Resource Manager.
2. Wybierz **klonowania lub pobierania**.
3. Witaj wybierz przycisk toocopy Witaj **HTTPS url klonowania** Schowka toohello i Zapisz adres URL hello do późniejszego użycia.
4. Wybierz obraz profilu hello hello prawym górnym rogu GitHub, a następnie wybierz **ustawienia**.
5. W hello **ustawienia osobiste** menu na powitania po lewej, wybierz opcję **osobiste tokeny dostępu**.
6. Wybierz **Wygeneruj nowy token**.
7. Na powitania **nowy osobisty token dostępu** wprowadź **Token opis**, zaakceptuj domyślne ustawienia hello hello **wybierz zakres**, a następnie wybierz pozycję **Generowanie Token**.
8. Zapisać hello wygenerowany token, ponieważ będzie potrzebny później.
9. Można teraz zamknąć GitHub.   
10. Kontynuować toohello [połączenia repozytorium toohello laboratorium](#connect-your-lab-to-the-repository) sekcji.

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Pobierz token hello adres URL klonowania repozytorium dla Visual Studio Team Services i osobistych dostęp
adres URL klonowania repozytorium tooget hello Visual Studio Team Services i osobistego tokenu dostępu, wykonaj następujące kroki:

1. Strona główna Otwórz hello kolekcji team (na przykład `https://contoso-web-team.visualstudio.com`), a następnie wybierz projekt.
2. Na stronie głównej projektu hello, wybierz **kod**.
3. tooview hello klonowania adresu URL, na powitania projektu **kod** wybierz pozycję **klonowania**.
4. Zapisz adres URL hello potrzebne w dalszej części tego samouczka.
5. Wybierz toocreate osobisty Token dostępu, **Mój profil** z menu rozwijanego konta użytkownika hello.
6. Na stronie informacje o profilu hello, wybierz **zabezpieczeń**.
7. Na powitania **zabezpieczeń** wybierz opcję **Dodaj**.
8. W hello **utworzyć osobisty token dostępu** strony:

   * Wprowadź **opis** hello tokenu.
   * Wybierz **180 dni** z hello **wygasa w** listy.
   * Wybierz **wszystkich dostępnych kont** z hello **kont** listy.
   * Wybierz hello **wszystkie zakresy** opcji.
   * Wybierz **Utwórz Token**.
9. Po zakończeniu hello nowy token jest wyświetlana w hello **osobiste tokeny dostępu** listy. Wybierz **kopiowania tokenu**, a następnie zapisz hello wartość tokenu do późniejszego użycia.
10. Kontynuować toohello [połączenia repozytorium toohello laboratorium](#connect-your-lab-to-the-repository) sekcji.

## <a name="connect-your-lab-toohello-repository"></a>Połącz z repozytorium toohello laboratorium
1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.
3. Z listy hello labs wybierz żądany laboratorium hello.   
4. W lewym panelu hello, wybierz **konfiguracji i zasadach**.
5. W laboratorium hello **konfiguracji i zasadach** wybierz opcję **repozytoria**.
6. Na powitania **repozytoria** wybierz opcję **+ Dodaj**.

    ![Dodawanie przycisku repozytorium](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. Na powitania drugi **repozytoria** Określ hello następujących informacji:

   * **Nazwa** — wprowadź nazwę hello repozytorium.
   * **Adres Url klonowania Git** — wprowadź hello HTTPS adres URL klonowania Git, które wcześniej zostały skopiowane z usługi GitHub lub Visual Studio Team Services.
   * **Gałąź** — wprowadź hello tooget gałęzi do definicji.
   * **Osobisty Token dostępu** — wprowadź hello osobisty token dostępu uzyskanymi wcześniej z usługi GitHub lub Visual Studio Team Services.
   * **Ścieżka folderu** — Wprowadź co najmniej jeden folder ścieżki względnej toohello klonowania adres URL zawierający Twoje artefaktu lub definicji szablonu usługi Azure Resource Manager. Podczas określania podkatalogu, upewnij się, że tooinclude hello ukośnika w ścieżce folderu hello.

     ![Repozytoria obszaru](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. Wybierz pozycję **Zapisz**.

## <a name="next-steps"></a>Następne kroki
Po utworzeniu swoje prywatne repozytorium Git, w zależności od potrzeb można wykonać jedną lub obie następujące hello:
* Magazyn sieci [niestandardowe artefakty](devtest-lab-artifact-author.md), który toocreate nowszej można użyć nowych maszyn wirtualnych.
* [Tworzenie środowisk wielu maszyn wirtualnych i PaaS zasobów przy użyciu szablonów usługi Azure Resource Manager](devtest-lab-create-environment-from-arm.md) , a następnie hello szablony są przechowywane w sieci prywatnej repozytorium.

Podczas tworzenia maszyny Wirtualnej, można sprawdzić, czy artefakty hello lub szablony są dodawane tooyour repozytorium Git. Są one dostępne natychmiast na liście hello artefakty lub szablonów, o nazwie hello Twoje prywatne repozytorium wyświetlane w kolumnie hello, który określa źródło hello. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>Wpisy na blogu pokrewne
* [Jak tootroubleshoot niepowodzeniem artefaktów w usłudze Azure DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Dołącz do maszyny Wirtualnej tooexisting domeny AD przy użyciu szablonu usługi resource manager w usłudze Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
