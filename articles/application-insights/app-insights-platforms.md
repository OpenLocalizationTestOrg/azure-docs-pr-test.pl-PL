---
title: "Application Insights: języki, platformy i integracje | Microsoft Docs"
description: "Języki, platformy i integracje dostępne dla usługi Application Insights"
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
manager: carmonm
ms.assetid: 974db106-54ff-4318-9f8b-f7b3a869e536
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: bwren
ms.openlocfilehash: 14b363c934a018ce72be97d1a0b74a6c2210656e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="developer-analytics-languages-platforms-and-integrations"></a>Rozszerzenie Developer Analytics: języki, platformy i integracje
Poniższe elementy to znane implementacje usługi [Application Insights](app-insights-overview.md), w tym niektóre innych firm.

## <a name="languages---officially-supported-by-application-insights-team"></a>Języki — oficjalnie obsługiwane przez zespół usługi Application Insights
* [C#|VB (.NET)](app-insights-asp-net.md)
* [Java](app-insights-java-get-started.md)
* [Strony sieci Web w języku JavaScript](app-insights-javascript.md)

## <a name="languages---community-supported"></a>Języki — obsługiwane przez społeczności
* [Node.JS](https://github.com/Microsoft/ApplicationInsights-node.js)
* [PHP](https://github.com/Microsoft/ApplicationInsights-PHP)
* [Python](https://pypi.python.org/pypi/applicationinsights/0.1.0)
* [Ruby](https://rubygems.org/gems/application_insights)
* [Coś innego](#projects)

## <a name="platforms-and-frameworks"></a>Platformy i struktury
* [Angular](https://www.npmjs.com/package/angular-applicationinsights)
* [ASP.NET](app-insights-asp-net.md)
* [ASP.NET — dla aplikacji, które już działają](app-insights-monitor-performance-live-website-now.md)
* [ASP.NET Core](app-insights-asp-net-core.md)
* [Android](https://github.com/Microsoft/ApplicationInsights-Android) (HockeyApp)
* [Azure Web Apps](app-insights-azure-web-apps.md)
* Usługi [Azure Cloud Services](app-insights-cloudservices.md) &#151; w tym role sieci Web i procesu roboczego
* [Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample)
* [Docker](app-insights-docker.md)
* [Glimpse](https://azure.microsoft.com/blog/glimpse-application-insights/)
* [iOS](https://github.com/Microsoft/ApplicationInsights-iOS) (HockeyApp)
* [J2EE](app-insights-java-get-started.md)
* [J2EE — dla aplikacji, które już działają](app-insights-java-live.md)
* [Aplikacja systemu Mac OS X](https://support.hockeyapp.net/kb/client-integration-ios-mac-os-x-tvos/hockeyapp-for-mac-os-x) (HockeyApp)
* [Node.JS](https://www.npmjs.com/package/applicationinsights)
* [OSX](https://github.com/Microsoft/ApplicationInsights-OSX)
* [Spring](http://joe.blog.freemansoft.com/2015/12/enabling-microsoft-application-insight.html)
* [Uniwersalna aplikacja systemu Windows](https://support.hockeyapp.net/kb/client-integration-windows-and-windows-phone/how-to-create-an-app-for-uwp) (HockeyApp)
* [WCF](https://github.com/Microsoft/ApplicationInsights-SDK-Labs/blob/master/WCF/readme.md)
* [Aplikacja systemu Windows Phone 8 i 8.1](https://support.hockeyapp.net/kb/client-integration-windows-and-windows-phone/hockeyapp-for-windows-phone-silverlight-apps-80-and-81) (HockeyApp)
* [Aplikacja Windows Presentation Foundation](https://support.hockeyapp.net/kb/client-integration-windows-and-windows-phone/hockeyapp-for-windows-wpf-apps) (HockeyApp)
* [Aplikacje klasyczne, usługi i role procesów roboczych systemu Windows](app-insights-windows-desktop.md)
* [Coś innego](#projects)

## <a name="logging-frameworks"></a>Struktury rejestrowania
* [Log4Net, NLog lub System.Diagnostics.Trace](app-insights-diagnostic-search.md)
* [Java, Log4J lub Logback](app-insights-java-trace-logs.md)
* [Semantic Logging (SLAB)](https://github.com/fidmor89/SLAB_AppInsights) — integruje się z usługą [Semantic Logging Application Block](https://msdn.microsoft.com/library/dn440729.aspx)
* [Testowanie obciążenia w chmurze](http://blogs.msdn.com/b/visualstudioalm/archive/2015/07/30/getting-application-insights-counters-with-cloud-based-load-testing.aspx)
* [Dodatek LogStash](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-output-applicationinsights)
* [OMS Log Analytics](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)
* [Logary](https://www.nuget.org/packages/Logary.Targets.AppInsights/)

## <a name="content-management-systems"></a>Systemy zarządzania zawartością
* [Concrete](https://github.com/fidmor89/appInsights-Concrete)
* [Drupal](https://github.com/fidmor89/AppInsights-Drupal)
* [Joomla](https://github.com/fidmor89/AppInsights-Joomla)
* [Orchard](https://azure.microsoft.com/blog/integrating-application-insights-into-a-modular-cms-and-a-multi-tenant-public-saas/preview/)
* [SharePoint](app-insights-sharepoint.md)
* [WordPress](https://wordpress.org/plugins/application-insights/)

## <a name="export-and-data-analysis"></a>Eksportowanie i analiza danych
* [Alooma](https://www.alooma.com/blog/application-insights-amazon-redshift)
* [Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx)
* [Stream Analytics](app-insights-export-power-bi.md)

## <a name="projects"></a> Tworzenie własnych zestawów SDK
Jeśli nie ma jeszcze zestawu SDK dla języka lub platformy, prawdopodobnie chcesz toobuild jeden? Spójrz na powitania kod hello istniejące zestawy SDK na liście hello [projekt zestawu SDK usługi Application Insights w serwisie GitHub](https://github.com/Microsoft/AppInsights-Home).
