---
title: "aaaUse podglądu raportów w witrynie sieci Web | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, jak toobuild z hello Visual Studio ReportViewer formant, który wyświetla raport witryną sieci Web platformy Microsoft Azure przechowywane na maszyny wirtualnej platformy Microsoft Azure."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>Korzystanie z narzędzia ReportViewer w witrynie internetowej hostowanej na platformie Azure
> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

Można tworzyć z hello formant programu Visual Studio podglądu raportów, który wyświetla raport przechowywane na maszyny wirtualnej platformy Microsoft Azure witryną sieci Web platformy Microsoft Azure. Hello formantu ReportViewer znajduje się w aplikacji sieci Web, tworzenie przy użyciu hello szablonu aplikacji sieci Web ASP.NET.

> [!IMPORTANT]
> Szablony aplikacji sieci Web platformy ASP.NET MVC Hello nie obsługują hello formantu ReportViewer.

tooincorporate podglądu raportów do witryny sieci Web platformy Microsoft Azure, należy hello toocomplete następujące zadania.

* **Dodaj** toohello zestawy pakiet wdrożeniowy
* **Skonfiguruj** uwierzytelniania i autoryzacji
* **Publikowanie** hello tooAzure aplikacji sieci Web ASP.NET

## <a name="prerequisites"></a>Wymagania wstępne
Przejrzyj sekcję "ogólne zalecenia i najlepsze rozwiązania w zakresie" hello w [analizy biznesowej programu SQL Server w usłudze Azure Virtual Machines](../classic/ps-sql-bi.md).

> [!NOTE]
> Kontrolki podglądu raportów są dostarczane z programem Visual Studio, Standard Edition lub nowszy. Jeśli używasz hello Web Developer Express Edition, musisz zainstalować hello [RUNTIME 2012 PODGLĄDU raportów firmy MICROSOFT](https://www.microsoft.com/download/details.aspx?id=35747) funkcji środowiska uruchomieniowego ReportViewer hello toouse.
> 
> W trybie przetwarzania lokalnego podglądu raportów nie jest obsługiwana w systemie Microsoft Azure.

## <a name="adding-assemblies-toohello-deployment-package"></a>Dodawanie zestawów toohello pakiet wdrożeniowy
Kiedy host ASP.NET aplikacji lokalnej, zestawy ReportViewer hello bezpośrednio w hello globalnej pamięci podręcznej zestawów (GAC) serwera IIS hello zazwyczaj są instalowane podczas instalacji programu Visual Studio i można uzyskać dostępu bezpośrednio aplikacji hello. Jednak hosta można aplikacji ASP.NET w chmurze hello, Microsoft Azure nie zezwala na coś toobe zainstalowane w hello GAC, dlatego należy upewnić się, hello ReportViewer zestawy są dostępne lokalnie dla aplikacji. Można to zrobić przez dodanie toothem odwołań w projekcie i skonfigurować je toobe skopiowany lokalnie.

W trybie przetwarzania zdalnego hello formantu ReportViewer wykorzystuje następujące zestawy hello:

* **Microsoft.ReportViewer.WebForms.dll**: zawiera hello ReportViewer kod, który należy toouse podglądu raportów na stronie. Odwołanie do tego zestawu dodaniu projektu tooyour po upuszczeniu formant podglądu raportów na stronę ASP.NET w projekcie.
* **Microsoft.ReportViewer.Common.dll**: zawiera klasy używane przez hello formantu ReportViewer w czasie wykonywania. Tooyour projekt nie został automatycznie dodany.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>tooadd tooMicrosoft.ReportViewer.Common odwołania
* Kliknij prawym przyciskiem myszy projektu **odwołania** a następnie wybierz węzeł **Dodaj odwołanie**, wybierz zestaw hello hello .NET kartę i kliknij przycisk **OK**.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>zestawy hello toomake dostępne lokalnie przez aplikację ASP.NET
1. W hello **odwołania** folderu, kliknij przycisk zestawu Microsoft.ReportViewer.Common hello tak, aby jego właściwości są wyświetlane w okienku właściwości hello.
2. W okienku właściwości hello ustawienie **Kopiuj lokalnie** tooTrue.
3. Powtórz kroki 1 i 2 dla Microsoft.ReportViewer.WebForms.

### <a name="tooget-reportviewer-language-pack"></a>tooget pakiet językowy podglądu raportów
1. Zainstaluj hello odpowiednie Runtime 2012 podglądu raportów firmy Microsoft pakiet redystrybucyjny z [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).
2. Języka hello wybierz z listy rozwijanej hello i strony hello pobiera przekierowanego toohello odpowiedniej strony Centrum pobierania.
3. Kliknij przycisk **Pobierz** pobieranie hello toostart ReportViewerLP.exe.
4. Po pobraniu ReportViewerLP.exe kliknij **Uruchom** tooinstall natychmiast, lub kliknij przycisk **zapisać** toosave on tooyour komputera. Jeśli klikniesz przycisk **zapisać**, pamiętaj hello nazwa folderu hello Jeżeli zapiszesz plik hello.
5. Zlokalizuj folder hello, w której został zapisany plik hello. Kliknij prawym przyciskiem myszy ReportViewerLP.exe, kliknij przycisk **Uruchom jako administrator**, a następnie kliknij przycisk **tak**.
6. Po uruchomieniu ReportViewerLP.exe, pojawi się hello c:\windows\assembly ma pliki zasobów hello **Microsoft.ReportViewer.Webforms.Resources** i **Microsoft.ReportViewer.Common.Resources** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>tooconfigure zlokalizowanych kontrolki podglądu raportów
1. Pobierz i zainstaluj pakiet redystrybucyjny hello Runtime 2012 podglądu raportów firmy Microsoft przez następujące hello ponad określona instrukcje.
2. Utwórz <language> folderu w hello projektu i skopiuj hello skojarzone pliki zestawu zasobów istnieje. Witaj toobe plików zestawu zasobów kopiowane są: **Microsoft.ReportViewer.Webforms.Resources.dll** i **Microsoft.ReportViewer.Common.Resources.dll**. Wybierz pliki zestawu zasobów hello, a następnie w okienku właściwości hello ustawienie **skopiuj tooOutput katalogu** zbyt "**skopiuj zawsze**".
3. Ustaw hello kultury & UICulture dla projektu sieci web hello. Aby uzyskać więcej informacji na temat sposobu hello tooset kultury i kultury interfejsu użytkownika dla strony sieci Web programu ASP.NET, zobacz [jak: zestaw hello kultury i kultury interfejsu użytkownika dla globalizacji strony sieci Web ASP.NET](http://go.microsoft.com/fwlink/?LinkId=237461).

## <a name="configuring-authentication-and-authorization"></a>Konfigurowanie uwierzytelniania i autoryzacji
Hello podglądu raportów wymaga toouse tooauthenticate odpowiednie poświadczenia dla serwera raportów na powitania, a poświadczenia hello musi zostać autoryzowana przez hello raportu server tooaccess hello raportów. Aby uzyskać informacje na temat uwierzytelniania, zobacz hello oficjalny dokument [raportu usług Reporting Services, Microsoft Azure maszyny wirtualnej na podstawie raportu serwery i formant podglądu](https://msdn.microsoft.com/library/azure/dn753698.aspx).

## <a name="publish-hello-aspnet-web-application-tooazure"></a>Publikowanie hello tooAzure aplikacji sieci Web ASP.NET
Aby uzyskać instrukcje na temat publikowania tooAzure aplikacji sieci Web ASP.NET, zobacz [porady: migracji i opublikuj tooAzure aplikacji sieci Web, z programu Visual Studio](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) i [wprowadzenie do aplikacji sieci Web i ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md).

> [!IMPORTANT]
> Jeśli w menu skrótów hello w Eksploratorze rozwiązań nie ma hello polecenia Dodaj projektu wdrożenia platformy Azure lub Dodaj projekt usługi w chmurze Azure, mogą być potrzebne platformy docelowej hello toochange hello projektu too.NET Framework 4.
> 
> Witaj dwie polecenia zapewniają zasadniczo hello tę samą funkcjonalność. Co najmniej hello inne polecenie będzie wyświetlane w menu skrótów hello zależności od instalowanej wersji hello Microsoft Azure SDK został zainstalowany.
> 
> 

## <a name="resources"></a>Zasoby
[Raporty firmy Microsoft](http://go.microsoft.com/fwlink/?LinkId=205399)

[SQL Server Business Intelligence na maszynach wirtualnych Azure](../classic/ps-sql-bi.md)

[Użyj programu PowerShell tooCreate Azure maszyny Wirtualnej z macierzysty tryb serwera raportów](../classic/ps-sql-report.md)

