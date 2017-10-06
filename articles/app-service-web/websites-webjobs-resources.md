---
title: "zasoby dokumentacji zadań Webjob aaaAzure"
description: "Zasoby szkoleniowe zalecany sposób toouse zadań Webjob Azure i hello Azure WebJobs SDK."
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Zasoby dokumentacji zadań Webjob Azure
## <a name="overview"></a>Omówienie
Ten temat zawiera łącza toodocumentation zasoby dotyczące toouse zadań Webjob Azure i hello Azure WebJobs SDK. Zadań Webjob Azure zapewniają prosty sposób toorun skrypty lub programy jako tło procesów w kontekście hello [aplikacji interfejsu API, aplikacji mobilnej lub aplikacji sieci web usługi aplikacji](../app-service/app-service-value-prop-what-is.md). Możesz przekazać i uruchom plik wykonywalny, takich jak jako cmd, bat, exe (.NET), ps1, sh, php, py i js i jar. Te programy uruchamiane jako zadań Webjob, zgodnie z harmonogramem (cron) lub w sposób ciągły.

Witaj celem hello [zestaw SDK zadań Webjob](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) jest kod hello toosimplify zapisu typowych zadań, które mogą wykonywać zadanie WebJob, takich jak przetwarzania obrazu, przetwarzanie kolejki, agregacja danych RSS, plików obsługi i wysyłania wiadomości e-mail. zestaw SDK zadań Webjob Hello ma wbudowane funkcje do pracy z usługą Azure Storage i usługi Service Bus, planowanie zadań i obsługa błędów i wielu innych typowych scenariuszy. Ponadto ma przeznaczona toobe rozszerzony i jest [repozytorium typu open source dla rozszerzeń](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview). [Środowisko Azure Functions](../azure-functions/functions-overview.md) (obecnie w wersji zapoznawczej) jest oparta na wersji hello zestaw SDK zadań Webjob, który działa z C# skrypt, Node.js i innych języków. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

Tworzenie, wdrażanie i zarządzanie zadań Webjob jest bezproblemowe z narzędziami zintegrowane w programie Visual Studio. Można utworzyć zadania Webjob na podstawie szablonów, publikowanie i zarządzanie (uruchomić, zatrzymać, monitorowania i debug) je. 

pulpitu nawigacyjnego zadań Webjob Hello w hello Azure portal udostępnia funkcji zaawansowanego zarządzania, które zapewniają pełną kontrolę nad hello wykonywanie zadań Webjob, w tym hello możliwości tooinvoke poszczególnych funkcji w ramach zadań Webjob. pulpit nawigacyjny Hello są również wyświetlane funkcja środowisk uruchomieniowych i dane wyjściowe rejestrowania. 

## <a name="getstarted"></a>Wprowadzenie do korzystania z zadań Webjob i hello zestaw SDK zadań Webjob
* [Wprowadzenie tooAzure zadań Webjob](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [Klienci są zadań Webjob Azure i należy zacząć od razu przy ich użyciu!](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (Wpis w blogu przez Troy Hunt.)
* [Funkcje zadań Webjob Azure](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [Co to jest zestaw SDK zadań Webjob hello](websites-dotnet-webjobs-sdk.md)
* [Wskazówki dotyczące zadań tła przez Microsoft Patterns and Practices](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [Anonsowanie hello 1.1.0 RTM programu Microsoft Azure WebJobs SDK](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Rozpoczynanie pracy z hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md)
* [Jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Jak toouse Azure tabeli magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [W jaki sposób toouse usługa Azure Service Bus z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-service-bus.md)
* [Azure WebJobs szybkie odwołanie do zestawu SDK (do pobrania plików PDF)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [Zadania Webjob ustawienia dokumentacji w witrynie GitHub](https://github.com/projectkudu/kudu/wiki/Web-jobs).
* Filmy wideo
  * [Zadań Webjob i hello zestaw SDK zadań Webjob](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Seria filmów zadań Webjob Azure witrynie Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Wprowadzenie do zadań Webjob narzędzi dla programu Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Narzędzia zadań Webjob i debugowanie zdalne](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Azure WebJobs aktualizacji za pomocą Pranav Rastogi - rozszerzalności w wersji 1.1](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

Zobacz także następujące sekcje zawierają informacje powitania [wdrażanie zadań Webjob](#deploy) i [testowanie i debugowanie zadań Webjob](#debug).

## <a name="deploy"></a>Wdrażanie zadań Webjob
* [Jak tooDeploy zadań Webjob Azure przy użyciu programu Visual Studio](websites-dotnet-deploy-webjobs.md)
* [Jak hello toodeploy zadań Webjob przy użyciu portalu Azure](web-sites-create-web-jobs.md)
* [Włączanie wiersza polecenia lub ciągłego dostarczania zadań Webjob Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Wdrażanie tooAzure aplikacji konsoli .NET przy użyciu zadań Webjob Git](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [Wdrażanie tooAzure zadania WebJob F #](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Wdrażanie niestandardowych usług jako zadań Webjob Azure](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* Filmy wideo
  * [Wprowadzenie do zadań Webjob narzędzi dla programu Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Narzędzia zadań Webjob i debugowanie zdalne](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>Planowanie zadań Webjob
* [Witaj dodać Azure zadania WebJob okna dialogowego](websites-dotnet-deploy-webjobs.md#configure)
* [Tworzenie zaplanowanych zadań WebJob w hello portalu Azure](web-sites-create-web-jobs.md#CreateScheduled)
* [Podłączanie tooa zadania harmonogramu zadań WebJob](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [Planowanie zadań Webjob Azure za pomocą wyrażeń usługi cron](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [Planowanie poszczególnych funkcji zadania WebJob przy użyciu hello TimerTrigger zestawu SDK zadań Webjob](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>Testowanie i debugowanie zadań Webjob
* [Nowe dla deweloperów i debugowanie funkcji Webjob Azure w programie Visual Studio](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Witaj widoku pulpitu nawigacyjnego zadań Webjob](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [Jak toowrite dzienników przy użyciu hello zestaw SDK zadań Webjob i wyświetlić je w hello pulpitu nawigacyjnego](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [Zdalne debugowanie zadań Webjob](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [Autorze tego obiektu blob?](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [Hosting kodu interaktywnego w hello chmury](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [Dodawanie tooAzure śledzenia zadań Webjob](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [Monitorowanie, diagnozowanie i rozwiązywanie problemów z usługi Magazyn Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* Filmy wideo
  * [Narzędzia zadań Webjob i debugowanie zdalne](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>Skalowanie zadania Webjob
* [Skalowanie aplikacji sieci Web z witryn sieci Web Azure](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Usługa aplikacji Azure: Projektowania aplikacji sieci Web gotowe dla firm bardzo dużej skali](https://channel9.msdn.com/Events/Build/2014/3-626). Obejmuje skalowanie aplikacji sieci web za pomocą zadań Webjob, w tym hello zestaw SDK zadań Webjob.
* Filmy wideo
  * [Skalowanie w poziomie zadań Webjob](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>Dodatkowe zasoby zadań Webjob
* [Azure WebJobs GA wpis w blogu przez Magnus Mårtensson](http://magnusmartensson.com/azure-webjobs-ga)
* [Uruchomione zadania sieci Web programu Powershell w usłudze aplikacji Azure](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Pobieranie powiadomienia, gdy Azure wyzwolony zadań Webjob zakończeniu](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [Proste zasady przechowywania kopii zapasowej aplikacji sieci Web z zadań Webjob](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [Aplikacje sieci Web platformy Azure i usługi w chmurze powolna na pierwsze żądanie](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Pokazuje, jak toosimulate zadań Webjob toouse hello funkcji AlwaysOn, który jest dostępny tylko dla warstwy cenowej standardowa hello.
* [Łagodne zamykanie zadań Webjob](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). Łagodne zamykanie dla SDK zadań Webjob, zobacz [łagodne zamykanie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).)
* [Automatyzowanie kopii zapasowych z zadań Webjob Azure & AzCopy](http://markjbrown.com/azure-webjobs-azcopy/)
* Filmy wideo
  * [Azure WebJobs wideo przez Magnus Mårtensson](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Seria filmów zadań Webjob Azure witrynie Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>Dodatkowe zasoby zestaw SDK zadań Webjob
* [Informacje o wersji zestawu SDK zadań Webjob](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [Zestaw SDK zadań Webjob kodu źródłowego](https://github.com/Azure/azure-webjobs-sdk)
* [Kod źródłowy rozszerzenia SDK zadań Webjob](https://github.com/Azure/azure-webjobs-sdk-extensions), z [modelu rozszerzalności toohello szczegółowy przewodnik](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).  
* [Kod źródłowy skryptu zestaw SDK zadań Webjob](https://github.com/Azure/azure-webjobs-sdk-script/) (używane dla [usługi Azure Functions](../azure-functions/functions-overview.md))
* [Zadanie WebJob tooupload FREB pliki tooAzure magazynu za pomocą hello zestaw SDK zadań Webjob](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [Hosting Azure webjobs poza Azure, z hello logowania korzyści z platformy Azure hostowanej zadania webjob](http://bypassion.dk/?p=510)
* [Tworzenie narzędzia importu danych z zadań Webjob Azure](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Azure Functions — omówienie](../azure-functions/functions-overview.md)
* Filmy wideo
  * [Seria filmów zadań Webjob Azure witrynie Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>Przykładowe aplikacje zadania WebJob
* [Przykładowe aplikacje udostępniane przez zespół zadań Webjob hello w witrynie GitHub](https://github.com/azure/azure-webjobs-sdk-samples)
* [Prostej aplikacji sieci Web platformy Azure z zadań Webjob wewnętrznej bazy danych przy użyciu hello zestaw SDK zadań Webjob](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). Pokazuje użycie zaplanowanych, jak i sterowane zdarzeniami zadań Webjob. Zobacz hello blogu [hello odbudowanie SiteMonitR przy użyciu zestawu SDK zadań Webjob Azure](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs).

## <a name="blogs"></a>Blogi
* [Azure blog](/blog)
* [Blog Amitowi Apple](http://blog.amitapple.com/). Skupiono się na zadań Webjob (nie hello zestawu SDK).
* [Blog Magnus Mårtensson](http://magnusmartensson.com/)

## <a name="gethelp"></a>Uzyskiwanie pomocy dotyczącej zadań Webjob
* [StackOverflow dla zadań Webjob](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [StackOverflow dla hello zestaw SDK zadań Webjob](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [StackOverflow dla funkcji platformy Azure](http://stackoverflow.com/questions/tagged/azure-functions)
* [Forum platformy Azure i programu ASP.NET](http://forums.asp.net/1247.aspx)
* [Forum usługi Azure App Service Web Apps](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Usługi Azure site głos użytkownika aplikacji sieci Web](https://feedback.azure.com/forums/169385-websites/)
* [W usłudze Twitter](http://twitter.com/). Użyj hello hasztagiem #AzureWebJobs.
* [Zgłoś problem lub usterka zadań Webjob](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)

