---
title: "Usługi w chmurze przy użyciu narzędzia Azure hello aaaPublishing | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toopublish Azure cloud projektów usług w programie Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/14/2017
ms.author: kraigb
ms.openlocfilehash: 31ede8308146de2bb128b768f23f64eb85bc7548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publishing-a-cloud-service-using-hello-azure-tools"></a>Publikowanie za pomocą narzędzia Azure hello usługi w chmurze
Przy użyciu hello Azure Tools dla programu Microsoft Visual Studio, możesz opublikować aplikację Azure bezpośrednio z programu Visual Studio. Visual Studio obsługuje, zintegrowane publikowania tooeither hello przemieszczania lub hello środowiska produkcyjnego usługi w chmurze.

Przed opublikowaniem aplikacji Azure, musi mieć subskrypcję platformy Azure. Należy również skonfigurować chmury usługi i przechowywania konta toobe używanych przez aplikację. Można je skonfigurować na powitania [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!IMPORTANT]
> Podczas publikowania, można wybrać hello środowiska wdrażania dla usługi w chmurze. Musisz również wybrać konto magazynu, który jest pakiet aplikacji hello toostore używanych do wdrożenia. Po wdrożeniu pakietu aplikacji hello jest usuwany z hello konta magazynu.
> 
> 

Podczas tworzenia i testowania aplikacji Azure, narzędzie Web Deploy toopublish zmian można użyć przyrostowo dla poszczególnych ról sieci web. Po opublikowaniu środowiska wdrażania tooa aplikacji Web Deploy umożliwia wdrażanie zmiany bezpośrednio toohello maszyny wirtualnej, na którym jest uruchomiony hello roli sieci web. Nie ma toopackage i opublikować całą aplikację Azure zawsze ma tooupdate tootest roli sieci web zmian hello. Z tej metody może mieć zmiany roli sieci web dostępnych w chmurze hello testowania bez oczekiwania toohave środowiska wdrażania tooa opublikowanych aplikacji.

Użyj hello następujące procedury toopublish aplikacji platformy Azure i tooupdate rolę sieci web za pomocą narzędzia Web Deploy:

* Publikowanie lub pakietu aplikacji Azure w programie Visual Studio
* Zaktualizuj rolę sieci web jako część hello programowania i testowania cyklu

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>Publikowanie lub pakietu aplikacji Azure w programie Visual Studio
Podczas publikowania aplikacji platformy Azure, możesz wybrać jedną hello następujące zadania:

* Tworzenie pakietu usług: ten pakiet i program hello usługi konfiguracji pliku toopublish można użyć środowiska wdrażania aplikacji tooa z hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
* Opublikować projekt platformy Azure w programie Visual Studio: toopublish aplikacji bezpośrednio tooAzure, użyj hello Kreator publikowania. Aby uzyskać informacje, zobacz [Kreator publikowania aplikacji Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="toocreate-a-service-package-from-visual-studio"></a>toocreate pakietu usług w programie Visual Studio
1. Po osiągnięciu gotowości toopublish aplikacji, Otwórz Eksplorator rozwiązań hello Otwórz menu skrótów hello Azure projekt, który zawiera role, i wybierz polecenie Publikuj.
2. toocreate pakiet usługi, wykonaj następujące kroki:  
   
   1. Menu skrótów hello hello Azure projektu, wybierz **pakietu**.
   2. W hello **pakietu aplikacji Azure** okno dialogowe Wybieranie hello konfiguracji usługi, dla której ma zostać toocreate pakietu, a następnie wybierz hello konfigurację kompilacji.
   3. (opcjonalnie) tooturn pulpitu zdalnego dla usługi w chmurze powitania po opublikowaniu, wybierz hello **Włącz pulpit zdalny dla wszystkich ról** pole wyboru, a następnie wybierz **ustawienia** tooconfigure pulpitu zdalnego. Jeśli chcesz toodebug usługi w chmurze po opublikowaniu, włączyć debugowanie zdalne, wybierając **Włącz zdalny debuger dla wszystkich ról**.
      
      Aby uzyskać więcej informacji, zobacz [za pomocą pulpitu zdalnego z rolami Azure](vs-azure-tools-remote-desktop-roles.md).
   4. Witaj toocreate pakiecie, wybierz hello **pakietu** łącza.
      
      Eksplorator plików zawiera lokalizację pliku hello hello nowo utworzony pakiet. Możesz skopiować tej lokalizacji, tak aby można go używać z hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   5. toopublish to środowisko wdrażania tooa pakietu, należy użyć tej lokalizacji, ponieważ hello lokalizacja pakietu podczas tworzenia usługi w chmurze i wdrażania tego pakietu środowiska tooan z hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
3. Wybierz proces wdrażania hello toocancel (opcjonalnie), w menu skrótów hello hello pozycji w dzienniku aktywności hello **Anuluj i Usuń**. Powoduje to zatrzymanie procesu wdrażania hello i usuwa środowisko wdrażania hello z platformy Azure.
   
   > [!NOTE]
   > tooremove to środowisko wdrażania po nim została wdrożona, należy użyć hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   > 
   > 
4. (Opcjonalnie) Po uruchomiona wystąpienia roli, Visual Studio zawiera automatycznie środowiska wdrażania hello hello **usługi w chmurze** węzła w Eksploratorze serwera. W tym miejscu można wyświetlić stan hello hello wystąpień poszczególnych ról. Zobacz [Azure zarządzanie zasobami za pomocą Eksploratora chmury](vs-azure-tools-resources-managing-with-cloud-explorer.md).hello następującej ilustracji przedstawiono hello wystąpień roli, gdy są one nadal w stanie inicjowanie hello:
   
    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-hello-development-and-testing-cycle"></a>Zaktualizuj rolę sieci Web w ramach hello programowanie i testowanie cyklu
Jeśli infrastruktury wewnętrznej bazy danych aplikacji jest stabilna, ale hello role sieci web trzeba więcej często uaktualniać, można użyć narzędzia Web Deploy tooupdate roli sieci web w projekcie. Jest to przydatne, gdy nie ma toorebuild i wdrożenie roli proces roboczy hello wewnętrznej bazy danych lub jeśli masz wiele ról sieci web i chcesz tooupdate tylko jedną z ról sieci web hello.

### <a name="requirements"></a>Wymagania
Oto hello wymagania toouse narzędzia Web Deploy tooupdate roli sieci web:

* **Do projektowania i testowania celów tylko:** hello zmian bezpośrednio maszyny wirtualnej toohello którym jest uruchomiona rola sieci web hello. Jeśli ta maszyna wirtualna ma toobe poddanych recyklingowi, hello zmiany zostaną utracone, ponieważ hello oryginalny pakiet opublikowaną jest maszyną wirtualną hello toorecreate używane dla roli hello. Będzie konieczne ponownie opublikowanie aplikacji tooget hello najnowsze zmiany hello roli sieci web.
* **Można aktualizować tylko role sieci web:** nie można zaktualizować roli proces roboczy. Ponadto nie można zaktualizować hello RoleEntryPoint w role.cs sieci web.
* **Może obsługiwać tylko jedno wystąpienie roli sieci web:** nie może mieć wielu wystąpień dowolnej roli sieci web w środowisku wdrażania. Jednak wielu role sieci web każdego z tylko jednym wystąpieniem są obsługiwane.
* **Należy włączyć połączenia pulpitu zdalnego:** jest to wymagane, dzięki czemu narzędzia Web Deploy można użyć hello użytkownika i hasło tooconnect toohello maszyny wirtualnej toodeploy hello zmiany toohello serwera z systemem Internet Information Services (IIS). Ponadto może być konieczne tooconnect toohello maszyny wirtualnej tooadd tooIIS zaufanego certyfikatu, na tej maszynie wirtualnej. (To zapewnia, że hello połączenia zdalnego dla usług IIS, który jest używany przez narzędzie Web Deploy jest bezpieczny).

Witaj poniższej procedurze przyjęto, że używasz hello **publikowanie aplikacji platformy Azure** kreatora.

### <a name="tooenable-web-deploy-when-you-publish-your-application"></a>tooEnable aplikacji sieci Web wdrażanie podczas możesz opublikować swój
1. Witaj tooenable **Włącz narzędzia Web Deploy** dla wszystkich sieci web pole wyboru ról, należy najpierw skonfigurować połączenia pulpitu zdalnego. Wybierz **Włącz pulpit zdalny** dla wszystkich ról, a następnie podaj hello poświadczenia, które będą używane tooconnect zdalnie w hello **konfigurację usług pulpitu zdalnego** pojawi się okno. Zobacz [za pomocą pulpitu zdalnego z rolami Azure](vs-azure-tools-remote-desktop-roles.md) Aby uzyskać więcej informacji.
2. Narzędzie Web Deploy tooenable hello wszystkie role sieci web w aplikacji, wybierz **Włącz narzędzia Web Deploy dla wszystkich ról sieci web**.
   
    Żółty trójkąt ostrzeżenie zostanie wyświetlone. Narzędzie Web Deploy używa certyfikatów niezaufanych, podpisem domyślnie, co nie jest zalecane do przekazywania poufnych danych. Jeśli potrzebujesz toosecure ten proces dla danych poufnych, można dodać toobe certyfikatu SSL, używanych dla połączenia narzędzia Web Deploy. Ten certyfikat musi toobe zaufanego certyfikatu. Informacje na temat toodo, zobacz sekcję hello **tooMake bezpiecznego wdrażania sieci Web** dalszej części tego tematu.
3. Wybierz **dalej** tooshow hello **Podsumowanie** ekranu, a następnie wybierz pozycję **publikowania** usługi w chmurze hello toodeploy.
   
    usługi w chmurze Hello jest opublikowana. Hello maszyny wirtualnej, która jest tworzona ma włączone dla usług IIS, aby umożliwić narzędzia Web Deploy tooupdate używanych połączeń zdalnych role sieci web bez ponownego ich publikowania.
   
   > [!NOTE]
   > Jeśli masz więcej niż jedno wystąpienie skonfigurowany dla roli sieci web, komunikat ostrzegawczy z informacją, że każda rola sieci web zostanie wyświetlony wystąpienia tooone ograniczone tylko w pakiecie hello, który utworzył toopublish aplikacji. Wybierz **OK** toocontinue. Jak już wspomniano w sekcji wymagań hello, można mieć więcej niż jedną witrynę sieci web roli, ale tylko jedno wystąpienie każdej roli.
   > 
   > 

### <a name="tooupdate-your-web-role-by-using-web-deploy"></a>tooUpdate Your roli sieci Web za pomocą narzędzia Web Deploy
1. toouse narzędzia Web Deploy należy projektu toohello zmiany kodu dla żadnej z ról sieci web w programie Visual Studio, czy mają toopublish, a następnie kliknij prawym przyciskiem myszy węzeł tego projektu w rozwiązaniu i wskaż zbyt**publikowania**. Witaj **publikowanie w sieci Web** zostanie wyświetlone okno dialogowe.
2. (Opcjonalnie) Jeśli dodano zaufany toouse certyfikatu SSL dla połączeń zdalnych dla usług IIS, można wyczyścić hello **niezaufany Zezwalaj** pole wyboru. Informacje o sposobie tooadd toomake certyfikatu, narzędzie Web Deploy bezpieczny, sekcji hello **tooMake sieci Web wdrażanie bezpiecznych** dalszej części tego tematu.
3. toouse sieci Web wdrażanie, publikowanie hello mechanizmu musi hello nazwy użytkownika i hasła, skonfigurowanej dla połączenia pulpitu zdalnego podczas pierwszej publikacji hello pakietu.
   
   1. W **nazwy użytkownika**, wprowadź nazwę użytkownika hello.
   2. W **hasło**, wprowadź hasło hello.
   3. (Opcjonalnie) Toosave to hasło do tego profilu, wybierz opcję **Zapisz hasło**.
4. toopublish hello zmiany tooyour roli sieć web wybierz **publikowania**.
   
    Wyświetla wiersz stanu Hello **publikowania uruchomiona**. Po zakończeniu publikowania hello **publikowanie zakończyło się pomyślnie** pojawi się. zmiany Hello zostały teraz roli sieci web toohello wdrożone na maszynie wirtualnej. Teraz można uruchomić aplikacji platformy Azure w tootest środowiska platformy Azure hello zmiany.

### <a name="toomake-web-deploy-secure"></a>tooMake bezpiecznego wdrażania w sieci Web
1. Narzędzie Web Deploy używa certyfikatów niezaufanych, podpisem domyślnie, co nie jest zalecane do przekazywania poufnych danych. Jeśli potrzebujesz toosecure ten proces dla danych poufnych, można dodać toobe certyfikatu SSL, używanych dla połączenia narzędzia Web Deploy. Ten certyfikat musi toobe zaufanego certyfikatu, który można uzyskać od urzędu certyfikacji (CA).
   
    toomake narzędzia Web Deploy bezpieczne dla każdej maszyny wirtualnej dla każdej z ról użytkownika sieci web, musisz przekazać hello zaufanych certyfikatów, które mają toouse dla narzędzia web deploy toohello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885). Zapewnia to, że ten certyfikat hello zostanie dodany toohello maszyny wirtualnej, która jest tworzona dla roli sieci web hello podczas publikowania aplikacji.
2. tooadd zaufanych toouse tooIIS certyfikatu SSL na dla połączeń zdalnych, wykonaj następujące kroki:
   
   1. maszyny wirtualnej toohello tooconnect, którym jest uruchomiona rola sieci web hello, wybierz hello wystąpienia roli sieci web hello w **Eksplorator chmury** lub **Eksploratora serwera**, a następnie wybierz pozycję hello **łączyć się przy użyciu Pulpit zdalny** polecenia. Aby uzyskać szczegółowe instrukcje na temat tooconnect toohello maszyny wirtualnej, zobacz [za pomocą pulpitu zdalnego z rolami Azure](vs-azure-tools-remote-desktop-roles.md).
      
      Przeglądarka wyświetli monit toodownload. Plik RDP.
   2. tooadd certyfikatu SSL, otwórz hello usługi zarządzania w Menedżerze usług IIS. W Menedżerze usług IIS, Włącz protokół SSL przez otwarcie hello **powiązania** łącze w hello **akcji** okienka. Witaj **Dodawanie powiązania witryny** zostanie wyświetlone okno dialogowe. Wybierz **Dodaj**, a następnie wybierz pozycję HTTPS w hello **typu** listy rozwijanej. W hello **certyfikat SSL** wybierz certyfikat SSL hello, aby były podpisane przez urząd certyfikacji i że przekazana toohello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885). Aby uzyskać więcej informacji, zobacz [Konfigurowanie ustawień połączenia dla usługi zarządzania hello](http://go.microsoft.com/fwlink/?LinkId=215824).
      
      > [!NOTE]
      > Jeśli dodajesz zaufanego certyfikatu SSL, hello żółty trójkąt ostrzeżenia nie będzie widoczny w hello **Kreator publikowania**.
      > 
      > 

## <a name="include-files-in-hello-service-package"></a>Pliki dołączane w hello pakiet usługi
Aby były one dostępne na maszynie wirtualnej hello, który jest tworzony dla roli, może być konieczne tooinclude określonych plików w pakiecie usługi. Na przykład można tooadd .exe lub pliku msi, który jest używany przez pakiet usługi tooyour uruchomienia skryptu. Lub może być konieczne tooadd zestawu, który wymaga projektu roli sieć web, jak rola lub procesu roboczego. tooinclude pliki, które muszą być dodane toohello rozwiązanie dla aplikacji platformy Azure.

### <a name="tooinclude-files-in-hello-service-package"></a>tooinclude plików w pakiecie usługi hello
1. tooadd pakiet zestawu tooa usługi użyj hello następujące kroki:
   
   1. W **Eksploratora rozwiązań** hello Otwórz węzeł projektu dla projektu hello, którym brakuje hello odwołuje się do zestawu.
   2. Projekt toohello tooadd hello zestawu, hello Otwórz menu skrótów hello **odwołania** folder, a następnie wybierz **Dodaj odwołanie**. zostanie wyświetlone okno dialogowe Dodaj odwołanie Hello.
   3. Wybierz odwołanie hello, że mają tooadd, a następnie wybierz pozycję hello **OK** przycisku.
      
      Odwołanie Hello jest dodawany toohello liście hello **odwołania** folderu.
   4. Otwórz menu skrótów hello hello zestawu, który został dodany i wybierz polecenie **właściwości**. Witaj **właściwości** zostanie wyświetlone okno.
      
      tooinclude tego zestawu w usłudze hello pakietu, w hello **kopii lokalnej listy** wybierz **True**.
2. W **Eksploratora rozwiązań** hello Otwórz węzeł projektu dla projektu hello, którym brakuje hello odwołuje się do zestawu.
3. Projekt toohello tooadd hello zestawu, hello Otwórz menu skrótów hello **odwołania** folder, a następnie wybierz **Dodaj odwołanie**. Witaj **Dodaj odwołanie** zostanie wyświetlone okno dialogowe.
4. Wybierz odwołanie hello, że mają tooadd, a następnie wybierz pozycję hello **OK** przycisku.
   
    Odwołanie Hello jest dodawany toohello liście hello **odwołania** folderu.
5. Otwórz menu skrótów hello hello zestawu, który został dodany i wybierz polecenie **właściwości**. zostanie wyświetlone powitalne okno właściwości.
6. tooinclude tego zestawu w usłudze hello pakietu, w hello **Kopiuj lokalnie** wybierz **True**.
7. pliki tooinclude w pakiecie usługi hello, które zostały dodane do projektu roli sieć web tooyour, otwórz menu skrótów hello hello pliku, a następnie wybierz **właściwości**. Z hello **właściwości** okna, wybierz **zawartości** z hello **Akcja kompilacji** pola listy.
8. pliki tooinclude w pakiecie usługi hello, które zostały dodane do projektu roli proces roboczy tooyour, otwórz menu skrótów hello hello pliku, a następnie wybierz **właściwości**. Z hello **właściwości** okna, wybierz **Kopiuj, jeśli nowszy** z hello **kopiowania katalogu toooutput** pola listy.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat publikowania tooAzure z programu Visual Studio, zobacz [Kreator publikowania aplikacji Azure](vs-azure-tools-publish-azure-application-wizard.md).

