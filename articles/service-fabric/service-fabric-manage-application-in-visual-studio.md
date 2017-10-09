---
title: aaaManage aplikacji w programie Visual Studio | Dokumentacja firmy Microsoft
description: "Użyj toocreate programu Visual Studio, tworzenie pakietów, wdrażanie i debugowanie usług i aplikacji sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>Użyj zapisu toosimplify programu Visual Studio i zarządzanie aplikacjami sieci szkieletowej usług
Można zarządzać sieć szkieletowa usług Azure, aplikacji i usług za pomocą programu Visual Studio. Po wprowadzeniu [Konfigurowanie środowiska deweloperskiego](service-fabric-get-started.md), korzystają z programu Visual Studio toocreate sieci szkieletowej usług aplikacji, Dodaj rejestru usług lub pakiet i wdrażania aplikacji w klastrze lokalnym programowanie.

## <a name="deploy-your-service-fabric-application"></a>Wdrażanie aplikacji sieci szkieletowej usług
Domyślnie wdrażanie aplikacji łączy hello w jednej operacji proste wykonaj następujące kroki:

1. Tworzenie pakietu aplikacji hello
2. Przekazywanie hello pakietu toohello obrazu sklepu z aplikacjami
3. Rejestracja typu aplikacji hello
4. Usunąć wszystkie uruchomione wystąpienia aplikacji
5. Tworzenie wystąpienia aplikacji

W programie Visual Studio naciskając klawisz **F5** wdraża aplikację i Dołącz hello debugera tooall aplikacji wystąpień. Można użyć **Ctrl + F5** toodeploy aplikacji bez debugowania lub możesz opublikować tooa lokalnego lub zdalnego klastra przy użyciu hello profilu publikowania. Aby uzyskać więcej informacji, zobacz [publikowanie aplikacji tooa zdalnego klastra przy użyciu programu Visual Studio](service-fabric-publish-app-remote-cluster.md).

### <a name="application-debug-mode"></a>Tryb debugowania aplikacji
Visual Studio Udostępnij właściwość o nazwie **tryb debugowania aplikacji**, która kontroluje sposób wdrażania aplikacji toohandle programu Visual Studio w ramach debugowania.

#### <a name="tooset-hello-application-debug-mode-property"></a>Witaj tooset właściwość tryb debugowania aplikacji
1. Na powitania sieci szkieletowej usług aplikacji projektu (*.sfproj) menu skrótów wybierz **właściwości** (lub naciśnij klawisz hello **F4** klucza).
2. W hello **właściwości** okna, zestaw hello **tryb debugowania aplikacji** właściwości.

![Ustaw właściwość tryb debugowania aplikacji][debugmodeproperty]

#### <a name="application-debug-modes"></a>Tryb debugowania aplikacji

1. **Odświeżanie aplikacji** tego trybu umożliwia zmianę tooquickly i debugować kod i obsługuje edycję plików statycznych sieci web podczas debugowania. W tym trybie działa tylko, jeśli klaster lokalny rozwój jest w [tryb węzła 1](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Usuń aplikację** przyczyny hello usuwane, gdy kończy się sesja debugowania hello toobe aplikacji.
3. **Automatyczne uaktualnienie** aplikacji hello nadal toorun podczas kończenia hello sesji debugowania. Witaj następnej sesji debugowania, będą traktować wdrożenia hello uaktualnienie. proces uaktualniania Hello zachowuje dane, które wprowadzono w poprzedniej sesji debugowania.
4. **Zachowaj aplikacji** hello przechowuje aplikacji uruchomionych w klastrze hello gdy hello debugowania zakończenia sesji. Początek hello hello następnej sesji debugowania, aplikacja hello zostaną usunięte.

Aby uzyskać **automatycznego uaktualnienia** dane zostaną zachowane, stosując możliwości uaktualnienia aplikacji hello sieci szkieletowej usług. Aby uzyskać więcej informacji o uaktualnianiu aplikacji i jak może wykonać uaktualnienie w środowisku prawdziwe, zobacz [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md).

## <a name="add-a-service-tooyour-service-fabric-application"></a>Dodaj tooyour usługi sieć szkieletowa usług aplikacji
Można dodać nowych usług tooyour aplikacji tooextend jego funkcjonalność.  tooensure, czy usługa hello jest uwzględniona w pakiet aplikacji, Dodaj hello usługi za pośrednictwem hello **nowa sieci szkieletowej usług...**  elementu menu.

![Dodaj nową usługę sieci szkieletowej usług][newservice]

Wybierz aplikację tooyour tooadd typ projektu sieci szkieletowej usług i określ nazwę usługi hello.  Zobacz [Wybieranie framework usługi](service-fabric-choose-framework.md) toohelp zdecydujesz usługi, która wpisz toouse.

![Wybierz aplikację tooyour tooadd typ projektu sieci szkieletowej usług usługi][addserviceproject]

Nowa usługa Hello jest dodawany tooyour rozwiązanie i istniejący pakiet aplikacji. odwołania do usług Hello i domyślnego wystąpienia usługi będzie dodany toohello manifest aplikacji, powodując toobe usługi hello utworzeniu i uruchomieniu hello następnym wdrażania aplikacji hello.

![Nowa usługa Hello jest dodawany tooyour manifest aplikacji][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Pakiet aplikacji sieci szkieletowej usług
Aplikacja hello toodeploy i jej usług tooa klastra, należy toocreate pakietu aplikacji.  Pakiet HELLO organizuje manifest aplikacji hello, manifesty usługi i inne niezbędne pliki w określonym układzie.  Visual Studio konfiguruje i zarządza hello pakietu w folderze projekt aplikacji hello w katalogu "pkg" hello.  Kliknięcie przycisku **pakietu** z hello **aplikacji** tworzy menu kontekstowego lub aktualizacje hello pakietu aplikacji.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Usuwanie aplikacji i typów aplikacji, w Eksploratorze chmury
Można wykonać operacji zarządzania podstawowy klaster z poziomu programu Visual Studio za pomocą Eksploratora chmury, które można uruchomić z hello **widoku** menu. Na przykład można usunąć aplikacji i wstrzymał obsługi administracyjnej typy aplikacji w klastrze lokalnym lub zdalnym.

![Usuwanie aplikacji][removeapplication]

> [!TIP]
> Aby uzyskać bardziej rozbudowane funkcje zarządzania klastrem, zobacz [wizualizacja klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
* [Model aplikacji sieci szkieletowej usług](service-fabric-application-model.md)
* [Wdrażanie aplikacji sieci szkieletowej usług](service-fabric-deploy-remove-applications.md)
* [Zarządzanie parametry aplikacji dla wielu środowisk](service-fabric-manage-multiple-environment-app-configuration.md)
* [Debugowanie aplikacji sieci szkieletowej usług](service-fabric-debugging-your-application.md)
* [Wizualizacja klastra przy użyciu Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png