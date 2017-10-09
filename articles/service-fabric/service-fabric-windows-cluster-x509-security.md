---
title: "Sieć szkieletowa usług Azure aaaSecure klastra w systemie Windows przy użyciu certyfikatów | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toosecure komunikacji w ramach autonomicznej hello lub prywatnej klastra oraz między klientami i hello klastra."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="ec6b5-103">Zabezpieczanie klastra autonomicznego w systemie Windows za pomocą certyfikatów X.509</span><span class="sxs-lookup"><span data-stu-id="ec6b5-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="ec6b5-104">W tym artykule opisano, jak toosecure hello komunikacji między hello różnych węzłów w klastrze Windows autonomicznych, a także sposobu tooauthenticate klientów łączących się klastra toothis, za pomocą certyfikatów X.509.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="ec6b5-105">Dzięki temu, że tylko autoryzowani użytkownicy mogą uzyskiwać dostęp do klastra hello hello wdrożonych aplikacji i wykonywać zadania zarządzania.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="ec6b5-106">Certyfikat zabezpieczeń powinien być włączony w klastrze hello podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="ec6b5-107">Aby uzyskać więcej informacji dotyczących zabezpieczeń klastra, takie jak zabezpieczeń węzła do węzła, węzeł klient zabezpieczeń i kontroli dostępu opartej na rolach, zobacz [klastra scenariusze zabezpieczeń](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="ec6b5-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="ec6b5-108">Certyfikatów, które będą potrzebne?</span><span class="sxs-lookup"><span data-stu-id="ec6b5-108">Which certificates will you need?</span></span>
<span data-ttu-id="ec6b5-109">toostart, [Pobierz hello wersjach klastra](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone hello węzłów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="ec6b5-110">W hello pobrano pakiet, można znaleźć **ClusterConfig.X509.MultiMachine.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="ec6b5-111">Otwórz plik hello i sekcji hello **zabezpieczeń** w obszarze hello **właściwości** sekcji:</span><span class="sxs-lookup"><span data-stu-id="ec6b5-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

<span data-ttu-id="ec6b5-112">W tej sekcji opisano hello certyfikaty, które należy do zabezpieczania autonomiczny klastra systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="ec6b5-113">W przypadku określania certyfikatu klastra, należy ustawić wartość hello **ClusterCredentialType** too_**X509**_. W przypadku określania certyfikatu serwera dla połączeń zewnętrznych, ustaw hello **ServerCredentialType** za_**X509**_. Chociaż nie jest to konieczne, zaleca się toohave oba te certyfikaty zabezpieczenie klastra. Jeśli te wartości zostaną ustawione zbyt*X509* , a następnie należy również określić hello odpowiednie certyfikaty lub sieci szkieletowej usług spowoduje zgłoszenie wyjątku. W niektórych scenariuszach tylko możesz toospecify hello _ClientCertificateThumbprints_ lub _ReverseProxyCertificate_. W tych scenariuszach nie należy ustawić _ClusterCredentialType_ lub _ServerCredentialType_ too_X509_.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="ec6b5-114">A [odcisk palca](https://en.wikipedia.org/wiki/Public_key_fingerprint) jest hello podstawowej tożsamości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="ec6b5-115">Odczyt [jak tooretrieve odcisk palca certyfikatu](https://msdn.microsoft.com/library/ms734695.aspx) toofind limit odcisk palca hello hello certyfikatów, które możesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="ec6b5-116">Witaj poniższej tabeli wymieniono hello certyfikaty, które będą potrzebne w konfiguracji klastra:</span><span class="sxs-lookup"><span data-stu-id="ec6b5-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="ec6b5-117">**Ustawienie CertificateInformation**</span><span class="sxs-lookup"><span data-stu-id="ec6b5-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="ec6b5-118">**Opis**</span><span class="sxs-lookup"><span data-stu-id="ec6b5-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="ec6b5-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="ec6b5-119">ClusterCertificate</span></span> |<span data-ttu-id="ec6b5-120">Zalecana dla środowiska testowego.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-120">Recommended for test environment.</span></span> <span data-ttu-id="ec6b5-121">Ten certyfikat jest wymagany toosecure hello komunikacji między węzłami hello w klastrze.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="ec6b5-122">Dwa różne certyfikaty, podstawowego i pomocniczego służy do uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="ec6b5-123">Ustaw hello odcisk palca certyfikatu podstawowego hello w hello **odcisk palca** sekcji i który hello pomocniczym w hello **ThumbprintSecondary** zmiennych.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="ec6b5-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="ec6b5-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="ec6b5-125">Zalecana dla środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-125">Recommended for production environment.</span></span> <span data-ttu-id="ec6b5-126">Ten certyfikat jest wymagany toosecure hello komunikacji między węzłami hello w klastrze.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="ec6b5-127">Można użyć jednego lub dwóch klastra wspólnej nazwy certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="ec6b5-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="ec6b5-128">ServerCertificate</span></span> |<span data-ttu-id="ec6b5-129">Zalecana dla środowiska testowego.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-129">Recommended for test environment.</span></span> <span data-ttu-id="ec6b5-130">Ten certyfikat jest widoczne toohello klienta po próbie tooconnect toothis klastra.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="ec6b5-131">Dla wygody można wybrać toouse hello sam certyfikat dla *ClusterCertificate* i *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="ec6b5-132">Do uaktualnienia, można użyć dwóch różnych certyfikatów, podstawowego i pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="ec6b5-133">Ustaw hello odcisk palca certyfikatu podstawowego hello w hello **odcisk palca** sekcji i który hello pomocniczym w hello **ThumbprintSecondary** zmiennych.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="ec6b5-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="ec6b5-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="ec6b5-135">Zalecana dla środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-135">Recommended for production environment.</span></span> <span data-ttu-id="ec6b5-136">Ten certyfikat jest widoczne toohello klienta po próbie tooconnect toothis klastra.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="ec6b5-137">Dla wygody można wybrać toouse hello sam certyfikat dla *ClusterCertificateCommonNames* i *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="ec6b5-138">Można użyć jednego lub dwóch certyfikatu wspólnej nazwy serwerów.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="ec6b5-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="ec6b5-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="ec6b5-140">Jest to zestaw certyfikatów, które mają tooinstall na klientach hello uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="ec6b5-141">Może mieć wiele różnych klientów certyfikatów zainstalowanych na powitania maszyny, które mają tooallow dostępu toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="ec6b5-142">Ustaw hello odcisk palca każdy z certyfikatów w hello **CertificateThumbprint** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="ec6b5-143">Jeśli ustawisz hello **IsAdmin** za*true*, a następnie powitania klienta przy użyciu tego certyfikatu na nim zainstalowany zrobić administrator działaniach zarządzania na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="ec6b5-144">Jeśli hello **IsAdmin** jest *false*, powitania klienta przy użyciu tego certyfikatu można wykonać tylko akcje hello dozwolone praw dostępu użytkownika, zwykle tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="ec6b5-145">Aby uzyskać więcej informacji na temat ról przeczytaj [oparta na rolach kontrola dostępu (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="ec6b5-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="ec6b5-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="ec6b5-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="ec6b5-147">Zestaw hello nazwa pospolita hello pierwszego certyfikatu klienta na powitania **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="ec6b5-148">Witaj **CertificateIssuerThumbprint** jest hello odcisk palca wystawcy hello tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="ec6b5-149">Odczyt [Praca z certyfikatami](https://msdn.microsoft.com/library/ms731899.aspx) tooknow więcej informacji na temat wspólnej nazwy i Witaj Wystawca.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="ec6b5-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="ec6b5-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="ec6b5-151">Zalecana dla środowiska testowego.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-151">Recommended for test environment.</span></span> <span data-ttu-id="ec6b5-152">Jest opcjonalny certyfikat, który może być określony, jeśli chcesz, aby toosecure Twojego [wstecznego Proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="ec6b5-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="ec6b5-153">Upewnij się, że reverseProxyEndpointPort jest ustawiony w elementów NodeType, jeśli używasz tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="ec6b5-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="ec6b5-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="ec6b5-155">Zalecana dla środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-155">Recommended for production environment.</span></span> <span data-ttu-id="ec6b5-156">Jest opcjonalny certyfikat, który może być określony, jeśli chcesz, aby toosecure Twojego [wstecznego Proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="ec6b5-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="ec6b5-157">Upewnij się, że reverseProxyEndpointPort jest ustawiony w elementów NodeType, jeśli używasz tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="ec6b5-158">Oto przykład konfiguracji klastra gdzie dostarczono hello certyfikatów klastra, klientów i serwerów.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="ec6b5-159">Należy pamiętać, że dla klastra / server / reverseProxy certyfikatów, odcisk palca i nazwa pospolita nie są dozwolone toobe skonfigurowanych dla hello sam typ certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a><span data-ttu-id="ec6b5-160">Przerzuć certyfikatu</span><span class="sxs-lookup"><span data-stu-id="ec6b5-160">Certificate roll over</span></span>
<span data-ttu-id="ec6b5-161">Używając nazwa pospolita certyfikatu zamiast odcisku palca, wycofywanie certyfikatu za pośrednictwem nie wymaga uaktualnienia konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="ec6b5-162">Jeśli wycofywanie certyfikatu za pośrednictwem obejmuje wystawcy przerzucane, pamiętaj o hello starego wystawcy certyfikatu w magazynie certyfikatów hello co najmniej 2 godziny po zainstalowaniu hello nowego wystawcy certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="ec6b5-163">Uzyskanie certyfikatów X.509 hello</span><span class="sxs-lookup"><span data-stu-id="ec6b5-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="ec6b5-164">toosecure komunikacji w ramach klastra hello, musisz najpierw certyfikatów X.509 tooobtain dla węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="ec6b5-165">Ponadto toolimit toothis połączenia klastra tooauthorized maszyny/użytkownicy, będzie konieczne tooobtain i instalowania certyfikatów dla komputerów klienckich hello.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="ec6b5-166">W przypadku klastrów z systemem obciążeń produkcyjnych należy używać [urzędu certyfikacji,](https://en.wikipedia.org/wiki/Certificate_authority) podpisany klastra hello toosecure certyfikatu X.509.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="ec6b5-167">Szczegółowe informacje dotyczące uzyskiwania tych certyfikatów, przejdź zbyt[porady: uzyskiwanie certyfikatu](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec6b5-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="ec6b5-168">W przypadku klastrów korzystających do celów testowych można toouse certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="ec6b5-169">Opcjonalnie: Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="ec6b5-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="ec6b5-170">Toouse hello jest jednym ze sposobów toocreate podpisanych certyfikatów, które mogą być chronione poprawnie *CertSetup.ps1* skryptu w folderze zestawu SDK usług sieci szkieletowej hello w katalogu hello *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="ec6b5-171">Edytowanie tego pliku toochange hello domyślną nazwę certyfikatu hello (Wyszukaj wartość hello *CN = ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="ec6b5-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="ec6b5-172">Uruchom ten skrypt jako `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="ec6b5-173">Obecnie można wyeksportować plik PFX tooa hello certyfikatu chronione hasłem.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="ec6b5-174">Najpierw pobierz hello odcisk palca certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="ec6b5-175">Z hello *Start* menu, uruchom hello *zarządzanie certyfikatami komputera*.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="ec6b5-176">Przejdź toohello **komputera lokalnego** folder i Znajdź hello certyfikatu należy po prostu utworzyć.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="ec6b5-177">Kliknij dwukrotnie tooopen certyfikatu hello go, wybierz opcję hello *szczegóły* i przewiń w dół toohello *odcisk palca* pola.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="ec6b5-178">Skopiuj wartość odcisku palca hello do polecenia programu PowerShell hello poniżej, po usunięciu hello spacji.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="ec6b5-179">Zmień hello `String` wartość tooprotect odpowiedniego bezpieczne hasło tooa go i uruchom powitania po w programie PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ec6b5-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="ec6b5-180">Szczegóły hello toosee zainstalowanego na powitania certyfikatu komputera należy uruchomić następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="ec6b5-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="ec6b5-181">Alternatywnie, jeśli masz subskrypcję platformy Azure, wykonaj sekcji hello [Dodaj certyfikaty tooKey magazynu](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="ec6b5-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="ec6b5-182">Instalowanie certyfikatów hello</span><span class="sxs-lookup"><span data-stu-id="ec6b5-182">Install hello certificates</span></span>
<span data-ttu-id="ec6b5-183">Po utworzeniu certyfikaty, można je zainstalować na węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="ec6b5-184">Węzły muszą toohave hello najnowsze środowiska Windows PowerShell 3.x na nich zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="ec6b5-185">Konieczne będzie toorepeat następujące kroki na każdym węźle, zarówno w przypadku klastra, jak i serwera certyfikatów i wszystkie pomocnicze certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="ec6b5-186">Skopiuj hello PFX pliki toohello węzła.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="ec6b5-187">Otwórz okno programu PowerShell jako administrator, a następnie wprowadź hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="ec6b5-188">Zastąp hello *$pswd* hasłem hello używane toocreate tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="ec6b5-189">Zastąp hello *$PfxFilePath* mającym pełną ścieżkę hello hello PFX skopiowanych toothis węzła.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="ec6b5-190">Teraz ustawić hello kontrolę dostępu dla tego certyfikatu, aby proces sieci szkieletowej usług hello, który jest uruchamiana hello konto Usługa sieciowa, może być używany przez uruchomienie hello następującego skryptu.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="ec6b5-191">Podaj odcisk palca hello hello certyfikatu i 'Usługa sieciowa"hello konta usługi.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="ec6b5-192">Możesz sprawdzić hello tej listy ACL w certyfikacie hello są poprawne, otwierając hello certyfikatu w *Start* > *zarządzanie certyfikatami komputera* i patrzeć *wszystkie zadania*  >  *Zarządzaj kluczami prywatnymi*.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="ec6b5-193">Powtórz powyższe kroki powitania dla każdego certyfikatu serwera.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="ec6b5-194">Umożliwia także te kroki tooinstall hello certyfikaty klienta na powitania maszynach, które mają tooallow dostępu toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="ec6b5-195">Tworzenie klastra bezpiecznego hello</span><span class="sxs-lookup"><span data-stu-id="ec6b5-195">Create hello secure cluster</span></span>
<span data-ttu-id="ec6b5-196">Po skonfigurowaniu hello **zabezpieczeń** sekcji hello **ClusterConfig.X509.MultiMachine.json** plików, można przejść za[tworzenia klastra](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure sekcji Witaj węzłów i utworzenie klastra autonomiczny hello.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="ec6b5-197">Pamiętaj toouse hello **ClusterConfig.X509.MultiMachine.json** pliku podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="ec6b5-198">Na przykład polecenie może wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ec6b5-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="ec6b5-199">Po utworzeniu hello bezpiecznego autonomicznego Windows klastra pomyślnie uruchomione, a następnie Instalator tooit tooconnect uwierzytelnionym klientom Witaj, wykonaj sekcji hello [Connect tooa bezpiecznego klastra przy użyciu programu PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="ec6b5-200">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ec6b5-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="ec6b5-201">Następnie możesz uruchomić inne toowork poleceń programu PowerShell z tym klastrem.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="ec6b5-202">Na przykład [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow listy węzłów w tym klastrze bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="ec6b5-203">tooremove hello klastra, połączenia z toohello węzła w klastrze hello którego został pobrany pakiet sieci szkieletowej usług hello, otwórz wiersz polecenia i przejdź do folderu pakietu toohello.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="ec6b5-204">Teraz uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ec6b5-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="ec6b5-205">Nieprawidłowy certyfikat konfiguracji może uniemożliwić powtarzający się podczas wdrażania klastra hello.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="ec6b5-206">tooself-diagnozowanie problemów z zabezpieczeniami, zapoznaj się w grupie podglądu zdarzeń *Dzienniki aplikacji i usług* > *sieci szkieletowej usług Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="ec6b5-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

