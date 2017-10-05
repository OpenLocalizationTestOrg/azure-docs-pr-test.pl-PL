---
title: "Zarządzanie usług Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać serwerem usług Analysis Services na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b897e81351ebee11c292e67ac76ba8202a6f0108
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="b6991-103">Zarządzanie usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b6991-103">Manage Analysis Services</span></span>
<span data-ttu-id="b6991-104">Po utworzeniu serwerem usług Analysis Services na platformie Azure, może to być niektórych zadań administracji i zarządzania, które należy wykonać od razu lub jakimś występujących.</span><span class="sxs-lookup"><span data-stu-id="b6991-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="b6991-105">Na przykład uruchom odświeżanie danych, kontrolowania, kto może uzyskać dostępu modeli na serwerze lub monitorowania kondycji serwera przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="b6991-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="b6991-106">Niektóre zadania zarządzania można wykonać tylko w portalu Azure, inne osoby w programu SQL Server Management Studio (SSMS), a niektóre zadania można to zrobić na dwa.</span><span class="sxs-lookup"><span data-stu-id="b6991-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="b6991-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b6991-107">Azure portal</span></span>
<span data-ttu-id="b6991-108">[Azure portal](http://portal.azure.com/) pozwala można utworzyć i usuwać serwery, monitorowanie zasobów serwera, zmienianie rozmiaru, i zarządzać dostępem do serwerów.</span><span class="sxs-lookup"><span data-stu-id="b6991-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="b6991-109">Jeśli występują problemy, możesz również przekazywać żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="b6991-109">If you're having some problems, you can also submit a support request.</span></span>

![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="b6991-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b6991-111">SQL Server Management Studio</span></span>
<span data-ttu-id="b6991-112">Łączenie z serwerem na platformie Azure działa tak, jak nawiązywanie połączenia z wystąpieniem serwera w organizacji.</span><span class="sxs-lookup"><span data-stu-id="b6991-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="b6991-113">Z SSMS można wykonywanie wielu zadań, takich jak przetwarzania danych lub utworzyć skrypt przetwarzania, do zarządzania rolami i przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6991-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="b6991-115">Pobierz i zainstaluj narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="b6991-115">Download and install SSMS</span></span>
<span data-ttu-id="b6991-116">Aby uzyskać najnowsze funkcje i daje płynne środowisko podczas nawiązywania połączenia z serwerem usług Analysis Services dla platformy Azure, upewnij się, że używasz najnowszej wersji programu SSMS.</span><span class="sxs-lookup"><span data-stu-id="b6991-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="b6991-117">[Pobieranie programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="b6991-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="b6991-118">Aby połączyć się ze SSMS</span><span class="sxs-lookup"><span data-stu-id="b6991-118">To connect with SSMS</span></span>
 <span data-ttu-id="b6991-119">Korzystając z narzędzia SSMS, przed nawiązaniem połączenia z serwerem po raz pierwszy, upewnij się, że nazwa użytkownika jest uwzględniona w grupie Administratorzy usług analizy.</span><span class="sxs-lookup"><span data-stu-id="b6991-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="b6991-120">Aby dowiedzieć się więcej, zobacz [administratorom serwerów](#server-administrators) dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="b6991-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="b6991-121">Przed nawiązaniem połączenia, należy uzyskać nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="b6991-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="b6991-122">Skopiuj nazwę serwera z **portalu Azure** > serwer > **Omówienie** > **Nazwa serwera**.</span><span class="sxs-lookup"><span data-stu-id="b6991-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="b6991-124">W programie SSMS > **Eksplorator obiektów**, kliknij przycisk **Connect** > **usług Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="b6991-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="b6991-125">W **Połącz z serwerem** okno dialogowe, Wklej w polu Nazwa serwera, a następnie w **uwierzytelniania**, wybierz jedną z następujących typów uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="b6991-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span></span>
   
    <span data-ttu-id="b6991-126">**Uwierzytelnianie systemu Windows** do korzystania z poświadczeń domena azwa_użytkownika i hasło systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="b6991-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="b6991-127">**Uwierzytelnianie hasłem usługi Active Directory** używanie konta organizacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b6991-127">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="b6991-128">Na przykład podczas nawiązywania połączenia ze spoza domeny przyłączone do komputera.</span><span class="sxs-lookup"><span data-stu-id="b6991-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="b6991-129">**Uwierzytelnianie usługi Active Directory uniwersalnych** do używania [nieinterakcyjnym lub usługi Multi-Factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b6991-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Połącz w programie SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="b6991-131">Administratorzy serwera i bazy danych użytkowników</span><span class="sxs-lookup"><span data-stu-id="b6991-131">Server administrators and database users</span></span>
<span data-ttu-id="b6991-132">W usłudze Azure Analysis Services istnieją dwa typy użytkowników, administratorów serwera i bazy danych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b6991-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="b6991-133">Użytkownicy obu typów musi znajdować się w usłudze Azure Active Directory i musi być określona za pomocą adresu e-mail organizacji lub nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="b6991-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="b6991-134">Aby dowiedzieć się więcej, zobacz [Authentication and user permissions (Uwierzytelnianie i uprawnienia użytkownika)](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="b6991-134">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="b6991-135">Rozwiązywanie problemów z połączeniem</span><span class="sxs-lookup"><span data-stu-id="b6991-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="b6991-136">Podczas nawiązywania połączenia przy użyciu narzędzia SSMS, jeśli wystąpią problemy, należy wyczyścić pamięć podręczną logowania.</span><span class="sxs-lookup"><span data-stu-id="b6991-136">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="b6991-137">Nic nie są buforowane na dysku. Aby wyczyścić pamięć podręczną, zamknij i uruchom proces connect.</span><span class="sxs-lookup"><span data-stu-id="b6991-137">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b6991-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b6991-138">Next steps</span></span>
<span data-ttu-id="b6991-139">Jeśli nie zostało już wdrożone modelu tabelarycznego, do nowego serwera, teraz jest odpowiedni moment.</span><span class="sxs-lookup"><span data-stu-id="b6991-139">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="b6991-140">Aby dowiedzieć się więcej, zobacz artykuł [Deploy to Azure Analysis Services](analysis-services-deploy.md) (Wdrażanie w usługach Azure Analysis Services).</span><span class="sxs-lookup"><span data-stu-id="b6991-140">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="b6991-141">Po wdrożeniu modelu do serwera, możesz połączyć się z nim za pomocą klienta lub przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="b6991-141">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="b6991-142">Aby dowiedzieć się więcej, zobacz [Pobierz dane z serwera usług Azure Analysis Services](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b6991-142">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

