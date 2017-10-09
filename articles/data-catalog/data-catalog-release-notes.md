---
title: informacje o wersji aaaAzure Data Catalog | Dokumentacja firmy Microsoft
description: "Informacje o wersji dla usługi Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="71c7e-103">Informacje o wersji usługi Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="71c7e-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="71c7e-104">Informacje o wersji 20 listopada 2015 hello Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="71c7e-104">Notes for hello November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="71c7e-105">Otwieranie źródeł danych w programie Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="71c7e-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="71c7e-106">Korzystając z opcji "Otwórz w Power BI Desktop" hello z hello **Azure Data Catalog** portalu, użytkownicy mogą wystąpić jeden z dwóch problemów w aplikacji Power BI Desktop hello:</span><span class="sxs-lookup"><span data-stu-id="71c7e-106">When using hello "Open in Power BI Desktop" option from hello **Azure Data Catalog** portal, users may encounter one of two problems in hello Power BI Desktop application:</span></span>

* <span data-ttu-id="71c7e-107">Zostanie wyświetlone okno dialogowe, z tytułem hello "TooOpen dokumentu"</span><span class="sxs-lookup"><span data-stu-id="71c7e-107">A dialog box with hello title "Unable tooOpen Document" is displayed</span></span>
* <span data-ttu-id="71c7e-108">Otwiera Hello aplikacji Power BI Desktop, ale plik hello pojawi się pusta toobe</span><span class="sxs-lookup"><span data-stu-id="71c7e-108">hello Power BI Desktop application opens, but hello file appears toobe empty</span></span>

<span data-ttu-id="71c7e-109">W każdej sytuacji hello problemu przez pobranie i zainstalowanie najnowszej wersji programu Power BI Desktop z hello [witryny PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="71c7e-109">For each situation, hello problem can be resolved by downloading and installing hello latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="71c7e-110">Informacje o wersji 13 listopada 2015 hello Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="71c7e-110">Notes for hello November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-tooteradata"></a><span data-ttu-id="71c7e-111">Rejestrowanie i łączenie tooTeradata</span><span class="sxs-lookup"><span data-stu-id="71c7e-111">Registering and connecting tooTeradata</span></span>
<span data-ttu-id="71c7e-112">Łącząc tooTeradata źródeł danych użytkownicy mają zainstalowany sterownik Teradata ODBC hello, które odpowiada hello liczbie bitów (32-bitowy lub 64-bitowy) hello oprogramowanie wykorzystywane.</span><span class="sxs-lookup"><span data-stu-id="71c7e-112">When connecting tooTeradata data sources users must have installed hello correct Teradata ODBC driver that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

<span data-ttu-id="71c7e-113">Począwszy od tej ADC Data wydania, hello najnowszych [sterownika ODBC programu Teradata dla systemu windows (wersja 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) jest zgodny z pakietu Office 2013, ale nie z pakietu Office 2016.</span><span class="sxs-lookup"><span data-stu-id="71c7e-113">As of this ADC release date, hello most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="71c7e-114">Informacje o wersji 13 lipca 2015 hello Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="71c7e-114">Notes for hello July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-toooracle-database"></a><span data-ttu-id="71c7e-115">Rejestrowanie i łączenie tooOracle bazy danych</span><span class="sxs-lookup"><span data-stu-id="71c7e-115">Registering and connecting tooOracle Database</span></span>
<span data-ttu-id="71c7e-116">Podczas łączenia użytkowników źródeł danych bazy danych tooOracle musi być zainstalowany hello poprawne Oracle sterowniki zgodne hello liczba bitów (32-bitowy lub 64-bitowy) hello oprogramowanie wykorzystywane.</span><span class="sxs-lookup"><span data-stu-id="71c7e-116">When connecting tooOracle Database data sources users must have installed hello correct Oracle drivers that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

* <span data-ttu-id="71c7e-117">Podczas rejestrowania źródła danych Oracle na komputerze z 32-bitowego systemu Windows, będą używane hello 32-bitowe sterowniki Oracle</span><span class="sxs-lookup"><span data-stu-id="71c7e-117">When registering Oracle data sources on a computer running 32-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="71c7e-118">Podczas rejestrowania źródła danych Oracle na komputerze z systemem 64-bitowego systemu Windows, będą używane hello 64-bitowych Oracle sterowników</span><span class="sxs-lookup"><span data-stu-id="71c7e-118">When registering Oracle data sources on a computer running 64-bit Windows, hello 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="71c7e-119">Podczas łączenia z tooOracle źródła danych przy użyciu programu Excel na komputerze z systemem hello 32-bitowej wersji pakietu Microsoft Office, w tym na 64-bitowej wersji systemu Windows hello 32-bitowe sterowniki Oracle będą używane</span><span class="sxs-lookup"><span data-stu-id="71c7e-119">When connecting tooOracle data sources using Excel on a computer running hello 32-bit version of Microsoft Office, including on 64-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="71c7e-120">Podczas łączenia z tooOracle źródła danych przy użyciu programu Excel na komputerze z systemem hello 64-bitowej wersji pakietu Microsoft Office, będą używane hello 64-bitowych Oracle sterowników</span><span class="sxs-lookup"><span data-stu-id="71c7e-120">When connecting tooOracle data sources using Excel on a computer running hello 64-bit version of Microsoft Office, hello 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-toosql-server-reporting-services"></a><span data-ttu-id="71c7e-121">Rejestrowanie i łączenie tooSQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="71c7e-121">Registering and connecting tooSQL Server Reporting Services</span></span>
<span data-ttu-id="71c7e-122">Obsługa źródeł danych usługi SQL Server Reporting Services (SSRS) jest obecnie ograniczone tooNative tryb tylko serwerów.</span><span class="sxs-lookup"><span data-stu-id="71c7e-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited tooNative Mode servers only.</span></span> <span data-ttu-id="71c7e-123">Obsługa usługi SSRS w trybie programu SharePoint zostanie dodany w nowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="71c7e-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="71c7e-124">Otwieranie zasobów danych w programie Excel</span><span class="sxs-lookup"><span data-stu-id="71c7e-124">Opening data assets in Excel</span></span>
<span data-ttu-id="71c7e-125">Podczas otwierania zasobów danych w programie Microsoft Excel z hello **Azure Data Catalog** portalu użytkowników może zostać wyświetlony monit o **powiadomienie o zabezpieczeniach programu Microsoft Excel** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="71c7e-125">When opening data assets in Microsoft Excel from hello **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="71c7e-126">Standard, jest to oczekiwane zachowanie, a użytkownicy mogą wybrać **włączyć** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="71c7e-126">This is standard, expected behavior, and users can select **Enable** toocontinue.</span></span>

<span data-ttu-id="71c7e-127">Aby uzyskać więcej informacji, zobacz [Włącz lub Wyłącz alerty zabezpieczeń dotyczące łącza i pliki z podejrzanych witrynach internetowych](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="71c7e-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="71c7e-128">Serwer proxy i zasad konfiguracji i danych rejestracji źródła</span><span class="sxs-lookup"><span data-stu-id="71c7e-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="71c7e-129">Użytkownicy mogą wystąpić w sytuacji, w którym można rejestrować na toohello portalu wykazu danych Azure, ale podczas prób toolog na toohello narzędzia rejestracji źródła danych w momencie napotkania komunikat o błędzie, który uniemożliwia zalogowanie.</span><span class="sxs-lookup"><span data-stu-id="71c7e-129">Users may encounter a situation where they can log on toohello Azure Data Catalog portal, but when they attempt toolog on toohello data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="71c7e-130">Istnieją dwie możliwe przyczyny tego problemu zachowania:</span><span class="sxs-lookup"><span data-stu-id="71c7e-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="71c7e-131">**1 Przyczyna: Konfiguracja Active Directory Federation Services** narzędzia rejestracji źródła danych hello korzysta z uwierzytelniania formularzy toovalidate użytkownika logowania do usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71c7e-131">**Cause 1: Active Directory Federation Services configuration** hello data source registration tool uses Forms Authentication toovalidate user logons against Active Directory.</span></span> <span data-ttu-id="71c7e-132">Do pomyślnego logowania należy włączyć uwierzytelnianie formularzy w hello globalne zasady uwierzytelniania przez administratora usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71c7e-132">For successful logon, Forms Authentication must be enabled in hello Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="71c7e-133">W niektórych sytuacjach zachowanie ten błąd może wystąpić tylko wtedy, gdy użytkownik hello znajduje się w sieci firmy hello lub tylko wtedy, gdy użytkownik hello nawiązuje połączenie z hello poza siecią firmową.</span><span class="sxs-lookup"><span data-stu-id="71c7e-133">In some situations, this error behavior may occur only when hello user is on hello company network, or only when hello user is connecting from outside hello company network.</span></span> <span data-ttu-id="71c7e-134">Witaj globalne zasady uwierzytelniania umożliwia włączone oddzielnie w intranecie i ekstranecie połączeń toobe metody uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="71c7e-134">hello Global Authentication Policy allows authentication methods toobe enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="71c7e-135">Błędy logowania może wystąpić, jeśli nie włączono uwierzytelniania formularzy hello sieci, z których hello użytkownik nawiązuje połączenie.</span><span class="sxs-lookup"><span data-stu-id="71c7e-135">Logon errors may occur if Forms Authentication is not enabled for hello network from which hello user is connecting.</span></span>

<span data-ttu-id="71c7e-136">Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad uwierzytelniania](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="71c7e-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="71c7e-137">**Przyczyny 2: Konfiguracja serwera proxy sieci** Jeśli hello sieć firmowa używa serwera proxy, narzędzie rejestracji hello może nie być możliwe tooconnect tooAzure usługi Active Directory za pośrednictwem serwera proxy hello.</span><span class="sxs-lookup"><span data-stu-id="71c7e-137">**Cause 2: Network proxy configuration** If hello corporate network uses a proxy server, hello registration tool may not be able tooconnect tooAzure Active Directory through hello proxy.</span></span> <span data-ttu-id="71c7e-138">Użytkownicy zapewnia narzędzia rejestracji hello, edytując plik konfiguracji narzędzia hello, dodawanie tego pliku toohello sekcji:</span><span class="sxs-lookup"><span data-stu-id="71c7e-138">Users can ensure that hello registration tool by editing hello tool’s configuration file, adding this section toohello file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="71c7e-139">toolocate hello RegistrationTool.exe.config plików, uruchom narzędzie rejestracji hello, a następnie otwórz narzędzie Menedżera zadań systemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="71c7e-139">toolocate hello RegistrationTool.exe.config file, launch hello registration tool, and then open hello Windows Task Manager utility.</span></span> <span data-ttu-id="71c7e-140">Na karcie Szczegóły hello w Menedżerze zadań kliknij prawym przyciskiem myszy na RegistrationTool.exe i wybierz z menu podręcznego hello Otwórz lokalizację pliku.</span><span class="sxs-lookup"><span data-stu-id="71c7e-140">On hello Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from hello pop-up menu.</span></span>
