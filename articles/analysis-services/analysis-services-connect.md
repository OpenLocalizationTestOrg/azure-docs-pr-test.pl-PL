---
title: "tooAzure aaaConnect usług Analysis Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconnect tooand pobrać dane z serwera usług Analysis Services na platformie Azure."
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
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="381e3-103">Połączyć z serwerem usług Azure Analysis Services tooan</span><span class="sxs-lookup"><span data-stu-id="381e3-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="381e3-104">W tym artykule opisano serwer łączący tooa za pomocą modelowania danych i zarządzania aplikacji, takich jak SQL Server Management Studio (SSMS) lub SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="381e3-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="381e3-105">Lub z klientem raportowanie aplikacji, takich jak program Microsoft Excel, Power BI Desktop lub niestandardowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="381e3-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="381e3-106">Usługi Analysis Services tooAzure połączeń używać protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="381e3-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="381e3-107">Biblioteki klienckie</span><span class="sxs-lookup"><span data-stu-id="381e3-107">Client libraries</span></span>
[<span data-ttu-id="381e3-108">Pobierz najnowsze bibliotek klienckich hello</span><span class="sxs-lookup"><span data-stu-id="381e3-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="381e3-109">Wszystkie połączenia serwera tooa, niezależnie od tego typu, wymagają zaktualizowanej AMO, ADOMD.NET i OLEDB biblioteki tooconnect tooand interfejsu klienta z serwerem usług Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="381e3-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="381e3-110">Dla narzędzia SSMS, narzędzi SSDT Excel 2016 i usługi Power BI bibliotek klienckich najnowsze hello są zainstalowane lub zaktualizowane wersje miesięcznych.</span><span class="sxs-lookup"><span data-stu-id="381e3-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="381e3-111">Jednak w niektórych przypadkach jest aplikacja nie może mieć hello najnowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="381e3-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="381e3-112">Na przykład podczas aktualizacji opóźnienie zasad lub aktualizacji usługi Office 365 są na powitania kanału opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="381e3-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="381e3-113">Nazwa serwera</span><span class="sxs-lookup"><span data-stu-id="381e3-113">Server name</span></span>

<span data-ttu-id="381e3-114">Podczas tworzenia serwera usług Analysis Services na platformie Azure, należy określić unikatowy region nazwy i hello której serwer hello jest toobe utworzony.</span><span class="sxs-lookup"><span data-stu-id="381e3-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="381e3-115">Podczas określania nazwy serwera hello na połączenie, jest schemat nazewnictwa powitania serwera:</span><span class="sxs-lookup"><span data-stu-id="381e3-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="381e3-116">Gdy protokół jest ciągiem **asazure**, region jest hello identyfikatora Uri, której utworzono powitania serwera (na przykład westus.asazure.windows.net) i servername jest nazwą powitania serwera unikatowy w obrębie regionu hello.</span><span class="sxs-lookup"><span data-stu-id="381e3-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="381e3-117">Pobierz nazwę serwera hello</span><span class="sxs-lookup"><span data-stu-id="381e3-117">Get hello server name</span></span>
<span data-ttu-id="381e3-118">W **portalu Azure** > serwera > **omówienie** > **nazwy serwera**, nazwa całego serwera hello kopii.</span><span class="sxs-lookup"><span data-stu-id="381e3-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="381e3-119">Inni użytkownicy w organizacji za łączenia toothis serwera, można udostępniać tę nazwę serwera z nimi.</span><span class="sxs-lookup"><span data-stu-id="381e3-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="381e3-120">Podczas określania nazwy serwera, należy użyć hello pełną ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="381e3-120">When specifying a server name, hello entire path must be used.</span></span>

![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="381e3-122">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="381e3-122">Connection string</span></span>

<span data-ttu-id="381e3-123">Podczas nawiązywania połączenia tooAzure Analysis Services przy użyciu hello tabelaryczny Model obiektów, użyj hello następujące formaty ciągu połączenia:</span><span class="sxs-lookup"><span data-stu-id="381e3-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="381e3-124">Zintegrowane uwierzytelnianie usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="381e3-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="381e3-125">Uwierzytelnianie zintegrowane przejmuje hello pamięci podręcznej poświadczeń usługi Azure Active Directory. Jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="381e3-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="381e3-126">Jeśli nie jest wyświetlane okno logowania do platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="381e3-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="381e3-127">Azure uwierzytelniania usługi Active Directory za pomocą nazwy użytkownika i hasła</span><span class="sxs-lookup"><span data-stu-id="381e3-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="381e3-128">Uwierzytelnianie systemu Windows (zintegrowane zabezpieczenia)</span><span class="sxs-lookup"><span data-stu-id="381e3-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="381e3-129">Użyj konta systemu Windows hello systemem hello bieżącego procesu.</span><span class="sxs-lookup"><span data-stu-id="381e3-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="381e3-130">Połącz, używając pliku odc</span><span class="sxs-lookup"><span data-stu-id="381e3-130">Connect using an .odc file</span></span>
<span data-ttu-id="381e3-131">W starszych wersjach programu Excel użytkownicy mogą łączyć tooan usług Azure Analysis Services serwera przy użyciu pliku połączenia danych pakietu Office (odc).</span><span class="sxs-lookup"><span data-stu-id="381e3-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="381e3-132">toolearn więcej, zobacz [Tworzenie pliku połączenia danych pakietu Office (odc)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="381e3-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="381e3-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="381e3-133">Next steps</span></span>
<span data-ttu-id="381e3-134">[Połącz przy użyciu programu Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="381e3-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="381e3-135">[Uzyskuj dostęp do usługi Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="381e3-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="381e3-136">Zarządzanie serwerem</span><span class="sxs-lookup"><span data-stu-id="381e3-136">Manage your server</span></span>](analysis-services-manage.md)   

