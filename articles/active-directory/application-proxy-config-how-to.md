---
title: tooconfigure aaaHow aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate Konfiguruj aplikację serwera Proxy aplikacji w kilku prostych krokach"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="76fd6-103">Jak tooconfigure aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="76fd6-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="76fd6-104">W tym artykule pomocy toounderstand jak tooconfigure aplikację serwera Proxy aplikacji w usłudze Azure AD tooexpose Twojego toohello aplikacji lokalnej w chmurze.</span><span class="sxs-lookup"><span data-stu-id="76fd6-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="76fd6-105">Zalecane dokumenty</span><span class="sxs-lookup"><span data-stu-id="76fd6-105">Recommended documents</span></span> 

<span data-ttu-id="76fd6-106">toolearn o hello początkowej konfiguracji i tworzenia aplikacji serwera Proxy aplikacji za pośrednictwem portalu administracyjnego hello wykonaj hello [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="76fd6-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="76fd6-107">Aby uzyskać więcej informacji na temat konfigurowania łączników, zobacz [Włączanie serwera Proxy aplikacji w portalu Azure hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="76fd6-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="76fd6-108">Aby uzyskać informacje na przekazywanie certyfikatów i przy użyciu domen niestandardowych, zobacz [Praca z domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="76fd6-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="76fd6-109">Utwórz hello adresy URL hello ustawienie/aplikacji</span><span class="sxs-lookup"><span data-stu-id="76fd6-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="76fd6-110">Jeśli wykonujesz hello etapami hello [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) dokumentacji i czy wprowadzenie błąd podczas tworzenia aplikacji hello, zobacz szczegóły błędu hello informacji i sugestie na temat Aplikacja hello toofix.</span><span class="sxs-lookup"><span data-stu-id="76fd6-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="76fd6-111">Większość komunikaty o błędach obejmują sugerowanej poprawki.</span><span class="sxs-lookup"><span data-stu-id="76fd6-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="76fd6-112">Sprawdź tooavoid typowych błędów:</span><span class="sxs-lookup"><span data-stu-id="76fd6-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="76fd6-113">Administratorzy z toocreate uprawnienia aplikacji serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="76fd6-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="76fd6-114">wewnętrzny adres URL Hello jest unikatowa</span><span class="sxs-lookup"><span data-stu-id="76fd6-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="76fd6-115">zewnętrzny adres URL Hello jest unikatowa</span><span class="sxs-lookup"><span data-stu-id="76fd6-115">hello external URL is unique</span></span>

-   <span data-ttu-id="76fd6-116">Witaj adresy URL rozpoczyna się od http lub https i kończyć się "/"</span><span class="sxs-lookup"><span data-stu-id="76fd6-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="76fd6-117">adres URL Hello powinien być nazwą domeny, a nie adres IP</span><span class="sxs-lookup"><span data-stu-id="76fd6-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="76fd6-118">komunikat o błędzie Hello powinien być wyświetlany w prawym górnym rogu hello podczas tworzenia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="76fd6-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="76fd6-119">Można również wybrać hello powiadomień ikona toosee hello komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="76fd6-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Wiersz powiadomień](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="76fd6-121">Konfigurowanie grup łączników/łącznika</span><span class="sxs-lookup"><span data-stu-id="76fd6-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="76fd6-122">Jeśli masz trudności w konfigurowaniu aplikacji z powodu ostrzeżenie o hello łączników i grupach łącznika, zobacz instrukcje na Włączanie serwera Proxy aplikacji, aby uzyskać więcej informacji na temat łączników toodownload.</span><span class="sxs-lookup"><span data-stu-id="76fd6-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="76fd6-123">Więcej informacji na temat łączników toolearn, zobacz hello [dokumentacji łączniki](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="76fd6-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="76fd6-124">Jeśli łączniki nie są aktywne, oznacza to, czy są one tooreach hello usługi.</span><span class="sxs-lookup"><span data-stu-id="76fd6-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="76fd6-125">Jest to często spowodowane wszystkie hello wymagane porty nie są otwarte.</span><span class="sxs-lookup"><span data-stu-id="76fd6-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="76fd6-126">toosee listę wymaganych portów zawiera sekcja wymagania wstępne hello hello włączenie dokumentacji serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="76fd6-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="76fd6-127">Przekaż certyfikaty dla domen niestandardowych</span><span class="sxs-lookup"><span data-stu-id="76fd6-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="76fd6-128">Domen niestandardowych można domeny hello toospecify Twojego zewnętrznych adresów URL.</span><span class="sxs-lookup"><span data-stu-id="76fd6-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="76fd6-129">domen niestandardowych toouse, potrzebujesz tooupload hello certyfikatu dla tej domeny.</span><span class="sxs-lookup"><span data-stu-id="76fd6-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="76fd6-130">Aby uzyskać informacje na temat używania domeny niestandardowej i certyfikatów, zobacz [Praca z domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="76fd6-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="76fd6-131">Pojawiły się problemy, przekazywanie certyfikatu, poszukaj komunikatów o błędach hello w portalu hello dodatkowe informacje na temat hello problem z certyfikatem hello.</span><span class="sxs-lookup"><span data-stu-id="76fd6-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="76fd6-132">Typowe problemy z certyfikatem obejmują:</span><span class="sxs-lookup"><span data-stu-id="76fd6-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="76fd6-133">Wygaśnięcie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="76fd6-133">Expired certificate</span></span>

-   <span data-ttu-id="76fd6-134">Certyfikat jest certyfikatem z podpisem</span><span class="sxs-lookup"><span data-stu-id="76fd6-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="76fd6-135">Certyfikat nie ma klucza prywatnego hello</span><span class="sxs-lookup"><span data-stu-id="76fd6-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="76fd6-136">Witaj błąd wyświetlania komunikatów w hello prawym górnym rogu jako spróbuj tooupload hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="76fd6-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="76fd6-137">Można również wybrać hello powiadomień ikona toosee hello komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="76fd6-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Wiersz powiadomień](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="76fd6-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="76fd6-139">Next steps</span></span>
[<span data-ttu-id="76fd6-140">Publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="76fd6-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
