---
title: "Łączenie się z usługami Azure Analysis | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nawiązać połączenie i Pobierz dane z serwerem usług Analysis Services na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: deb3ef28d20decef01826450bd6091f87dd069de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-an-azure-analysis-services-server"></a><span data-ttu-id="46677-103">Połącz się z serwerem usług Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="46677-103">Connect to an Azure Analysis Services server</span></span>

<span data-ttu-id="46677-104">W tym artykule opisano łączenia się z serwerem za pomocą modelowania danych i zarządzania aplikacji, takich jak SQL Server Management Studio (SSMS) lub SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="46677-104">This article describes connecting to a server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="46677-105">Lub z klientem raportowanie aplikacji, takich jak program Microsoft Excel, Power BI Desktop lub niestandardowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="46677-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="46677-106">Połączenia do usług Azure Analysis Services używają protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="46677-106">Connections to Azure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="46677-107">Biblioteki klienckie</span><span class="sxs-lookup"><span data-stu-id="46677-107">Client libraries</span></span>
[<span data-ttu-id="46677-108">Pobierz najnowsze biblioteki klienta</span><span class="sxs-lookup"><span data-stu-id="46677-108">Get the latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="46677-109">Wszystkie połączenia z serwerem, niezależnie od tego typu, wymagają zaktualizowanej biblioteki AMO, ADOMD.NET i OLEDB klienta do nawiązania połączenia i łączyć się z serwerem usług Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="46677-109">All connections to a server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries to connect to and interface with an Analysis Services server.</span></span> <span data-ttu-id="46677-110">Dla narzędzia SSMS, narzędzi SSDT Excel 2016 i usługi Power BI najnowsze biblioteki klienta są zainstalowane lub zaktualizowane wersje miesięcznych.</span><span class="sxs-lookup"><span data-stu-id="46677-110">For SSMS, SSDT, Excel 2016, and Power BI, the latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="46677-111">Jednak w niektórych przypadkach jest aplikacji nie może mieć r.</span><span class="sxs-lookup"><span data-stu-id="46677-111">However, in some cases, it's possible an application may not have the latest.</span></span> <span data-ttu-id="46677-112">Na przykład gdy opóźnienie zasady aktualizacji lub aktualizacji usługi Office 365 są w kanale opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="46677-112">For example, when policies delay updates, or Office 365 updates are on the Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="46677-113">Nazwa serwera</span><span class="sxs-lookup"><span data-stu-id="46677-113">Server name</span></span>

<span data-ttu-id="46677-114">Podczas tworzenia serwera usług Analysis Services na platformie Azure, należy określić unikatową nazwę i regionu, w którym można utworzyć serwera.</span><span class="sxs-lookup"><span data-stu-id="46677-114">When you create an Analysis Services server in Azure, you specify a unique name and the region where the server is to be created.</span></span> <span data-ttu-id="46677-115">Podczas określania nazwy serwera na połączenie, jest schemat nazewnictwa serwera:</span><span class="sxs-lookup"><span data-stu-id="46677-115">When specifying the server name in a connection, the server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="46677-116">Gdy protokół jest ciągiem **asazure**, region jest identyfikatorem Uri, gdy serwer został utworzony (na przykład westus.asazure.windows.net) i servername jest nazwą serwera unikatowy w obrębie regionu.</span><span class="sxs-lookup"><span data-stu-id="46677-116">Where protocol is string **asazure**, region is the Uri where the server was created (for example, westus.asazure.windows.net) and servername is the name of your unique server within the region.</span></span>

### <a name="get-the-server-name"></a><span data-ttu-id="46677-117">Pobierz nazwę serwera</span><span class="sxs-lookup"><span data-stu-id="46677-117">Get the server name</span></span>
<span data-ttu-id="46677-118">W **portalu Azure** > serwera > **omówienie** > **nazwy serwera**, skopiuj nazwę całego serwera.</span><span class="sxs-lookup"><span data-stu-id="46677-118">In **Azure portal** > server > **Overview** > **Server name**, copy the entire server name.</span></span> <span data-ttu-id="46677-119">Jeśli innym użytkownikom w organizacji są zbyt połączenie do tego serwera, można udostępniać tę nazwę serwera z nimi.</span><span class="sxs-lookup"><span data-stu-id="46677-119">If other users in your organization are connecting to this server too, you can share this server name with them.</span></span> <span data-ttu-id="46677-120">Podczas określania nazwy serwera, należy użyć pełną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="46677-120">When specifying a server name, the entire path must be used.</span></span>

![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="46677-122">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="46677-122">Connection string</span></span>

<span data-ttu-id="46677-123">Podczas nawiązywania połączenia przy użyciu modelu tabelarycznego obiektu usług Azure Analysis Services, użyj ciągu połączenia w następujących formatach:</span><span class="sxs-lookup"><span data-stu-id="46677-123">When connecting to Azure Analysis Services using the Tabular Object Model, use the following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="46677-124">Zintegrowane uwierzytelnianie usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46677-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="46677-125">Uwierzytelnianie zintegrowane przejmuje pamięci podręcznej poświadczeń usługi Azure Active Directory, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="46677-125">Integrated authentication picks up the Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="46677-126">Jeśli nie jest wyświetlane okno logowania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="46677-126">If not, the Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="46677-127">Azure uwierzytelniania usługi Active Directory za pomocą nazwy użytkownika i hasła</span><span class="sxs-lookup"><span data-stu-id="46677-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="46677-128">Uwierzytelnianie systemu Windows (zintegrowane zabezpieczenia)</span><span class="sxs-lookup"><span data-stu-id="46677-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="46677-129">Użyj konta systemu Windows uruchomiona bieżącego procesu.</span><span class="sxs-lookup"><span data-stu-id="46677-129">Use the Windows account running the current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="46677-130">Połącz, używając pliku odc</span><span class="sxs-lookup"><span data-stu-id="46677-130">Connect using an .odc file</span></span>
<span data-ttu-id="46677-131">W starszych wersjach programu Excel użytkownicy mogą łączyć się z serwerem usług Azure Analysis Services przy użyciu pliku połączenia danych pakietu Office (odc).</span><span class="sxs-lookup"><span data-stu-id="46677-131">With older versions of Excel, users can connect to an Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="46677-132">Aby dowiedzieć się więcej, zobacz [Tworzenie pliku połączenia danych pakietu Office (odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="46677-132">To learn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="46677-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="46677-133">Next steps</span></span>
<span data-ttu-id="46677-134">[Połącz przy użyciu programu Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="46677-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="46677-135">[Uzyskuj dostęp do usługi Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="46677-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="46677-136">Zarządzanie serwerem</span><span class="sxs-lookup"><span data-stu-id="46677-136">Manage your server</span></span>](analysis-services-manage.md)   

