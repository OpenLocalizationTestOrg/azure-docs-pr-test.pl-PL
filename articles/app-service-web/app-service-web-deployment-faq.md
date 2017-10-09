---
title: "aaaDeployment — często zadawane pytania dotyczące aplikacji sieci web platformy Azure | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toofrequently zadawane pytania dotyczące wdrażania dla funkcji Web Apps hello Azure App Service."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a>Często zadawane pytania dotyczące wdrażania aplikacji sieci Web na platformie Azure

Ten artykuł zawiera odpowiedzi toofrequently zadawane pytania (FAQ) dotyczące problemów dotyczących wdrożenia dla hello [funkcja Web Apps usługi Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a>Jestem I dopiero rozpoczynasz pracę z aplikacjami sieci web usługi aplikacji. Jak opublikować mój kod?

Poniżej przedstawiono niektóre opcje publikowania kodu aplikacji sieci web:

*   Wdrażanie przy użyciu programu Visual Studio. Jeśli masz hello rozwiązania Visual Studio, kliknij prawym przyciskiem myszy projekt aplikacji hello sieci web, a następnie wybierz **publikowania**.
*   Wdrażanie przy użyciu klienta FTP. W portalu Azure hello, hello pobierania profilu dla aplikacji sieci web hello publikowania mają toodeploy swój kod. Następnie przekaż hello too\site\wwwroot plików przy użyciu hello sam publikowania poświadczenia profilu FTP.

Aby uzyskać więcej informacji, zobacz [wdrażanie tooApp Twojej aplikacji usługi](web-sites-deploy.md).

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a>Podczas próby toodeploy z programu Visual Studio, zobacz się komunikat o błędzie. Jak rozwiązać ten problem?

Jeśli widzisz następującą wiadomości powitania, być może korzystasz starszej wersji zestawu SDK hello: "Wystąpił błąd podczas wdrażania zasobu"YourResourceName"w grupie zasobów"YourResourceGroup": MissingRegistrationForLocation: hello subskrypcja nie jest zarejestrowana dla Witaj typ zasobu "składniki" w lokalizacji hello środkowe stany USA. Zarejestruj ponownie dla tego dostawcy, w kolejności toohave dostępu toothis lokalizacji." 

tooresolve ten błąd, uaktualnienia toohello [najnowszej wersji zestawu SDK](https://azure.microsoft.com/downloads/). Jeśli ten komunikat zostanie wyświetlony i mieć hello najnowszej wersji zestawu SDK, należy przesłać żądanie obsługi.

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a>Jak wdrożyć aplikację ASP.NET z programu Visual Studio tooApp usługi?
<a id="deployasp"></a>

Samouczek Hello [tworzenie pierwszej aplikacji sieci web platformy ASP.NET na platformie Azure w ciągu pięciu minut](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) pokazuje, jak toodeploy platformy ASP.NET w sieci web aplikacji sieci web tooa aplikacji w usłudze App Service przy użyciu programu Visual Studio 2015.

## <a name="what-are-hello-different-types-of-deployment-credentials"></a>Co to są różnych typów hello poświadczenia wdrożenia?

Usługi aplikacji obsługuje dwa typy poświadczeń dla lokalnych wdrożeniem Git i FTP/S. Aby uzyskać więcej informacji o tym, jak tooconfigure poświadczenia wdrażania, zobacz [Konfigurowanie poświadczeń wdrożenia dla aplikacji usługi](app-service-deployment-credentials.md).

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a>Co to jest struktura pliku lub katalogu hello Moja aplikacja sieci web usługi aplikacji?

Aby informacji na temat struktury plików hello aplikację usługi aplikacji, zobacz [pliku struktura w systemie Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a>Jak rozwiązać, "Błąd FTP 550 - tam nie jest za mało miejsca na dysku hello" podczas próby tooFTP pliki?

Jeśli ten komunikat zostanie wyświetlony, istnieje prawdopodobieństwo, że uruchamiasz w przydział dysku w hello planu usługi dla aplikacji sieci web. Może być konieczne tooscale się tooa wyższego poziomu usługi na podstawie Twoich potrzeb miejsca na dysku. Aby uzyskać więcej informacji na temat cen planów i limity zasobów, zobacz [cennik usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a>Jak skonfigurować ciągłe wdrażanie dla mojej aplikacji sieci web usługi aplikacji?

Można skonfigurować ciągłego wdrażania od wielu zasobów, w tym Visual Studio Team Services, usługi OneDrive, GitHub, Bitbucket, Dropbox i innych repozytoriów narzędzia Git. Te opcje są dostępne w portalu hello. [TooApp ciągłego wdrażania usługi](app-service-continuous-deployment.md) jest przydatne samouczek, który objaśnia, jak tooset się ciągłego wdrażania.

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a>Jak rozwiązać problemy z ciągłego wdrażania od GitHub i Bitbucket?

Aby uzyskać pomoc do badania problemów dotyczących ciągłego wdrażania od usługi GitHub lub Bitbucket, [badanie ciągłe wdrażanie](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a>Nie mogę toomy witryny FTP i Publikuj kod. Jak rozwiązać ten problem?

problemy tooresolve FTP:

1. Upewnij się, że wprowadzasz hello poprawną nazwę hosta i poświadczeń. Aby uzyskać szczegółowe informacje o różnych typach poświadczeń i toouse, zobacz temat [poświadczenia wdrażania](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).
2. Upewnij się, że porty hello FTP nie są blokowane przez zaporę. porty Hello powinny mieć następujące ustawienia:
    * Port połączenia sterowania FTP: 21
    * Port połączenia danych FTP: 989, 10001 10300

## <a name="how-do-i-publish-my-code-tooapp-service"></a>Jak opublikować moje tooApp kodu usługi?

Witaj Szybki Start Azure jest zaprojektowana toohelp wdrażanie aplikacji przy użyciu hello wdrożenia stosu i użyciu wybranej metody. toouse hello Szybki Start, w hello portalu Azure Przejdź zbyt**ustawienia** > **wdrażania aplikacji**.

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a>Dlaczego moja aplikacja czasami ponownie po tooApp wdrożenia usługi?

toolearn temat hello okoliczności, w których wdrożenia aplikacji może spowodować ponowne uruchomienie, zobacz [wdrożenia, a problemy środowiska uruchomieniowego](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts"). Zgodnie z opisem w artykule hello usługi aplikacji — wdraża folder wwwroot toohello plików. Nigdy nie bezpośrednio ponownego uruchomienia aplikacji.

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a>Jak zintegrować kodu programu Visual Studio Team Services z usługi aplikacji?

Masz dwie opcje związane z Visual Studio Team Services za pomocą ciągłego wdrażania:

*   Użyj projektu Git. Połączenie za pomocą usługi aplikacji przy użyciu opcji wdrażania hello na tym repozytorium.
*   Użyj projektu kontroli wersji typu Team Foundation (TFVC). Wdrażanie przy użyciu hello agenta kompilacji dla aplikacji usługi.

Kod ciągłego wdrażania dla obu tych opcji zależy od istniejących projektanta przepływów pracy i procedur zaewidencjonowania. Aby uzyskać więcej informacji zobacz następujące artykuły: 

*   [Wdrożenie ciągłe wdrażanie tooan Twojej aplikacji witryny sieci Web Azure](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [Konfigurowanie konta usługi Visual Studio Team Services, można wdrożyć aplikację sieci web tooa](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a>Jak używać toodeploy FTP i FTPS Moje tooApp app Service?

Informacje o korzystaniu z FTP i FTPS toodeploy tooApp aplikacji sieci web usługi, zobacz [wdrażanie tooApp Twojego app Service przy użyciu FTP/S](app-service-deploy-ftp.md).
