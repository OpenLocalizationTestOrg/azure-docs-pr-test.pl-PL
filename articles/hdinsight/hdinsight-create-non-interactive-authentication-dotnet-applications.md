---
title: "Uwierzytelnianie nieinterakcyjne aaaCreate osób uzyskujących .NET HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacje usługi HDInsight .NET uwierzytelnianie nieinteraktywne toocreate."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="e89ad-103">Tworzenie aplikacji usługi HDInsight .NET uwierzytelnianie nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="e89ad-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="e89ad-104">Można uruchomić aplikacji .NET Azure HDInsight w ramach tożsamości aplikacji (nieinterakcyjnym) lub tożsamością hello hello zalogowanego użytkownika aplikacji hello (interaktywne).</span><span class="sxs-lookup"><span data-stu-id="e89ad-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="e89ad-105">Przykładowy interaktywna aplikacja hello, [połączyć tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="e89ad-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="e89ad-106">W tym artykule opisano sposób toocreate uwierzytelnianie nieinteraktywne .NET aplikacji tooconnect tooAzure i zarządzanie nimi w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e89ad-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="e89ad-107">Z poziomu innego nieinteraktywnego aplikacji .NET potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="e89ad-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="e89ad-108">Identyfikator subskrypcji platformy Azure dzierżawy (nazywane również identyfikator katalogu).</span><span class="sxs-lookup"><span data-stu-id="e89ad-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="e89ad-109">Zobacz [uzyskanie Identyfikatora dzierżawy](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="e89ad-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="e89ad-110">Identyfikator klienta aplikacji usługi Azure Active Directory Hello.</span><span class="sxs-lookup"><span data-stu-id="e89ad-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="e89ad-111">Zobacz [tworzy aplikację usługi Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), i [uzyskiwanie Identyfikatora aplikacji](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="e89ad-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="e89ad-112">Azure Active Directory Hello aplikacji klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="e89ad-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="e89ad-113">Zobacz [klucz uwierzytelniania aplikacji Get](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="e89ad-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e89ad-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e89ad-114">Prerequisites</span></span>
* <span data-ttu-id="e89ad-115">Klaster usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e89ad-115">HDInsight cluster.</span></span> <span data-ttu-id="e89ad-116">Zobacz [Wprowadzenie — samouczek](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="e89ad-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="e89ad-117">Przypisz toorole aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e89ad-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="e89ad-118">Należy przypisać tooa aplikacji hello [roli](../active-directory/role-based-access-built-in-roles.md) toogrant ona uprawnienia do wykonywania akcji.</span><span class="sxs-lookup"><span data-stu-id="e89ad-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="e89ad-119">Zakres hello można ustawić na poziomie hello hello subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="e89ad-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="e89ad-120">uprawnienia Hello są dziedziczone toolower poziomy zakresu (na przykład dodawanie przez rolę czytelnika toohello aplikacji dla grupy zasobów. oznacza to, że może odczytywać hello grupy zasobów i wszystkie zasoby, które zawiera).</span><span class="sxs-lookup"><span data-stu-id="e89ad-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="e89ad-121">W tym samouczku zostanie Ustaw zakres hello na poziomie grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="e89ad-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="e89ad-122">Aby uzyskać więcej informacji, zobacz [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="e89ad-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="e89ad-123">**Witaj tooadd właściciela roli toohello usługi Azure AD aplikacji**</span><span class="sxs-lookup"><span data-stu-id="e89ad-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="e89ad-124">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e89ad-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e89ad-125">Kliknij przycisk **grupy zasobów** w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="e89ad-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="e89ad-126">Kliknij grupę zasobów hello, która zawiera hello klastra usługi HDInsight, gdzie należy uruchomić zapytanie Hive w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="e89ad-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="e89ad-127">Jeśli ma zbyt wiele grup zasobów, można użyć filtru hello.</span><span class="sxs-lookup"><span data-stu-id="e89ad-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="e89ad-128">Kliknij przycisk **(IAM) kontroli dostępu** hello zasobów grupy menu.</span><span class="sxs-lookup"><span data-stu-id="e89ad-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="e89ad-129">Kliknij przycisk **Dodaj** z hello **użytkowników** bloku.</span><span class="sxs-lookup"><span data-stu-id="e89ad-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="e89ad-130">Wykonaj hello instrukcji tooadd hello **właściciela** toohello roli aplikacji usługi Azure AD, został utworzony w poprzedniej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="e89ad-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="e89ad-131">Po zakończeniu jego pomyślnie, zostanie wyświetlona aplikacja hello hello blok użytkownicy z rolą właściciela hello na liście.</span><span class="sxs-lookup"><span data-stu-id="e89ad-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="e89ad-132">Tworzenie aplikacji klienckich usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="e89ad-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="e89ad-133">Utwórz aplikację konsolową języka C#.</span><span class="sxs-lookup"><span data-stu-id="e89ad-133">Create a C# console application.</span></span>
2. <span data-ttu-id="e89ad-134">Dodaj następujące pakiety Nuget hello:</span><span class="sxs-lookup"><span data-stu-id="e89ad-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="e89ad-135">Użyj hello poniższy kod przykładowy:</span><span class="sxs-lookup"><span data-stu-id="e89ad-135">Use hello following code sample:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter hello Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a><span data-ttu-id="e89ad-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e89ad-136">Next steps</span></span>
* [<span data-ttu-id="e89ad-137">Tworzenie aplikacji usługi Azure Active Directory i nazwy głównej usługi przy użyciu portalu</span><span class="sxs-lookup"><span data-stu-id="e89ad-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="e89ad-138">Uwierzytelnianie nazwy głównej usługi z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e89ad-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="e89ad-139">Kontrola dostępu oparta na rolach na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e89ad-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
