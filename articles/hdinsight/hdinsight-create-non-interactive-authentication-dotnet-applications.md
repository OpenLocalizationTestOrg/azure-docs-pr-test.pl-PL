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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Tworzenie aplikacji usługi HDInsight .NET uwierzytelnianie nieinterakcyjne
Można uruchomić aplikacji .NET Azure HDInsight w ramach tożsamości aplikacji (nieinterakcyjnym) lub tożsamością hello hello zalogowanego użytkownika aplikacji hello (interaktywne). Przykładowy interaktywna aplikacja hello, [połączyć tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). W tym artykule opisano sposób toocreate uwierzytelnianie nieinteraktywne .NET aplikacji tooconnect tooAzure i zarządzanie nimi w usłudze HDInsight.

Z poziomu innego nieinteraktywnego aplikacji .NET potrzebne są:

* Identyfikator subskrypcji platformy Azure dzierżawy (nazywane również identyfikator katalogu). Zobacz [uzyskanie Identyfikatora dzierżawy](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* Identyfikator klienta aplikacji usługi Azure Active Directory Hello. Zobacz [tworzy aplikację usługi Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), i [uzyskiwanie Identyfikatora aplikacji](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)
* Azure Active Directory Hello aplikacji klucz tajny. Zobacz [klucz uwierzytelniania aplikacji Get](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)

## <a name="prerequisites"></a>Wymagania wstępne
* Klaster usługi HDInsight. Zobacz [Wprowadzenie — samouczek](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-toorole"></a>Przypisz toorole aplikacji usługi Azure AD
Należy przypisać tooa aplikacji hello [roli](../active-directory/role-based-access-built-in-roles.md) toogrant ona uprawnienia do wykonywania akcji. Zakres hello można ustawić na poziomie hello hello subskrypcji, grupy zasobów lub zasobów. uprawnienia Hello są dziedziczone toolower poziomy zakresu (na przykład dodawanie przez rolę czytelnika toohello aplikacji dla grupy zasobów. oznacza to, że może odczytywać hello grupy zasobów i wszystkie zasoby, które zawiera). W tym samouczku zostanie Ustaw zakres hello na poziomie grupy zasobów hello. Aby uzyskać więcej informacji, zobacz [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](../active-directory/role-based-access-control-configure.md)

**Witaj tooadd właściciela roli toohello usługi Azure AD aplikacji**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **grupy zasobów** w okienku po lewej stronie powitania.
3. Kliknij grupę zasobów hello, która zawiera hello klastra usługi HDInsight, gdzie należy uruchomić zapytanie Hive w dalszej części tego samouczka. Jeśli ma zbyt wiele grup zasobów, można użyć filtru hello.
4. Kliknij przycisk **(IAM) kontroli dostępu** hello zasobów grupy menu.
5. Kliknij przycisk **Dodaj** z hello **użytkowników** bloku.
6. Wykonaj hello instrukcji tooadd hello **właściciela** toohello roli aplikacji usługi Azure AD, został utworzony w poprzedniej procedurze hello. Po zakończeniu jego pomyślnie, zostanie wyświetlona aplikacja hello hello blok użytkownicy z rolą właściciela hello na liście.

## <a name="develop-hdinsight-client-application"></a>Tworzenie aplikacji klienckich usługi HDInsight

1. Utwórz aplikację konsolową języka C#.
2. Dodaj następujące pakiety Nuget hello:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Użyj hello poniższy kod przykładowy:

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

## <a name="next-steps"></a>Następne kroki
* [Tworzenie aplikacji usługi Azure Active Directory i nazwy głównej usługi przy użyciu portalu](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Uwierzytelnianie nazwy głównej usługi z usługą Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Kontrola dostępu oparta na rolach na platformie Azure](../active-directory/role-based-access-control-configure.md)
