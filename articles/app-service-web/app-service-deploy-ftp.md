---
title: "aaaDeploy Twojego tooAzure aplikacji App Service przy użyciu FTP/S | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy Twojego tooAzure aplikacji App Service przy użyciu FTP i FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>Wdrażanie sieci tooAzure aplikacji App Service przy użyciu FTP/S

W tym artykule opisano sposób toouse FTP i FTPS toodeploy aplikację sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API za[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Hello końcowego FTP/S dla aplikacji jest już aktywna. Konfiguracja nie jest konieczne tooenable wdrożenia FTP/S.

> [!IMPORTANT]
> Firma Microsoft stale wykonywanie czynności tooimprove zabezpieczeń platformy Microsoft Azure. Jako część tego ciągłego wysiłku regiony Niemcy centralnej i Niemcy północno-wschodnie planowana jest uaktualnienie aplikacji sieci Web. Podczas tego aplikacje sieci Web będzie wyłączanie hello użycie protokołu zwykły tekst FTP wdrożeń. Naszym klientom tooour zalecenie jest tooFTPS tooswitch wdrożeń. Firma Microsoft nie będzie przerw w działaniu usługi tooyour podczas tego uaktualnienia, którą jest planowana 9/5. Dziękujemy za obsługuje w tym wysiłku.

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>Krok 1: Konfigurowanie poświadczeń wdrożenia

tooaccess hello FTP serwera dla aplikacji, należy najpierw poświadczenia wdrożenia. 

tooset lub zresetowania poświadczenia wdrażania, zobacz [poświadczenia wdrożenia usługi aplikacji Azure](app-service-deployment-credentials.md). W tym samouczku przedstawiono używanie hello poświadczeń na poziomie użytkownika.

## <a name="step-2-get-ftp-connection-information"></a>Krok 2: Pobieranie informacji o połączeniu FTP

1. W hello [portalu Azure](https://portal.azure.com), otwórz aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Wybierz **omówienie** w menu po lewej stronie powitania, a następnie zanotuj wartości hello **użytkownika serwera FTP/wdrożenia**, **nazwa hosta FTP**, i **nazwy hosta FTPS**. 

    ![Informacje o połączeniu FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > Witaj **użytkownika serwera FTP/wdrożenia** użytkownika wartości wyświetlanej przez hello portalu Azure, łącznie z nazwą aplikacji hello w kolejności tooprovide prawidłowego kontekstu serwera hello FTP.
    > Można znaleźć hello tych samych informacji po wybraniu **właściwości** w menu po lewej stronie powitania. 
    >
    > Ponadto hello wdrożenia hasło nigdy nie jest wyświetlana. Jeśli zapomnisz hasła wdrożenia, wróć za[krok 1](#step1) i zresetuj hasło wdrożenia.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>Krok 3: Wdrażanie tooAzure plików

1. Z tego klienta FTP ([programu Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client)itp), użyj informacji o połączeniu hello zebranych tooconnect tooyour aplikacji.
3. Kopiowanie plików i ich toohello struktury katalogu odpowiednich [ **/lokacji/wwwroot** katalogu](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) na platformie Azure (lub hello **/lokacji/wwwroot/App_Data/zadania/** katalogu dla Zadania Webjob).
4. Aplikacja hello tooverify adres URL przeglądania tooyour aplikacji działa prawidłowo. 

> [!NOTE] 
> W odróżnieniu od [wdrożenia oparte na Git](app-service-deploy-local-git.md), wdrożenie FTP nie obsługuje powitania po automatyzacji wdrażania: 
>
> - Przywracanie zależności (na przykład automatyzacji NuGet, NPM, PIP i kompozytor)
> - Kompilacja plików binarnych .NET
> - Generowanie pliku Web.config (w tym miejscu jest [przykład Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))
> 
> Należy przywrócić, kompilacji i generuje te niezbędne pliki ręcznie na komputerze lokalnym i wdrażać je razem z aplikacji.
>
>

## <a name="next-steps"></a>Następne kroki

W przypadku bardziej zaawansowanych scenariuszy wdrażania, spróbuj [wdrażanie tooAzure za pomocą narzędzia Git](app-service-deploy-local-git.md). Wdrażanie na podstawie Git tooAzure umożliwia kontroli wersji, Przywracanie pakietu MSBuild i więcej.

## <a name="more-resources"></a>Więcej zasobów

* [Tworzenie aplikacji sieci web PHP MySQL i wdrażanie za pomocą protokołu FTP](web-sites-php-mysql-deploy-use-ftp.md).
* [Poświadczenia wdrożenia usługi aplikacji Azure](app-service-deploy-ftp.md)
