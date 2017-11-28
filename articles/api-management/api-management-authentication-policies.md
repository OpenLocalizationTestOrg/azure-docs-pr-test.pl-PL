---
title: "zasady uwierzytelniania interfejsu API zarządzania aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad uwierzytelniania hello dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="577dd-103">Zarządzanie interfejsami API zasady uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="577dd-103">API Management authentication policies</span></span>
<span data-ttu-id="577dd-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management hello.</span><span class="sxs-lookup"><span data-stu-id="577dd-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="577dd-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="577dd-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="577dd-106"><a name="AuthenticationPolicies"></a>Zasady uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="577dd-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="577dd-107">[Uwierzytelnianie za pomocą Basic](api-management-authentication-policies.md#Basic) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="577dd-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="577dd-108">[Uwierzytelniania za pomocą certyfikatu klienta](api-management-authentication-policies.md#ClientCertificate) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="577dd-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="577dd-109"><a name="Basic"></a>Uwierzytelniania Basic</span><span class="sxs-lookup"><span data-stu-id="577dd-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="577dd-110">Użyj hello `authentication-basic` tooauthenticate zasad z usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="577dd-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="577dd-111">Ta zasada efektywnie ustawia wartość odpowiednie poświadczenia toohello podany w zasadzie hello toohello nagłówek autoryzacji HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="577dd-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="577dd-112">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="577dd-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="577dd-113">Przykład</span><span class="sxs-lookup"><span data-stu-id="577dd-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="577dd-114">Elementy</span><span class="sxs-lookup"><span data-stu-id="577dd-114">Elements</span></span>  
  
|<span data-ttu-id="577dd-115">Nazwa</span><span class="sxs-lookup"><span data-stu-id="577dd-115">Name</span></span>|<span data-ttu-id="577dd-116">Opis</span><span class="sxs-lookup"><span data-stu-id="577dd-116">Description</span></span>|<span data-ttu-id="577dd-117">Wymagane</span><span class="sxs-lookup"><span data-stu-id="577dd-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="577dd-118">Uwierzytelnianie — podstawowy</span><span class="sxs-lookup"><span data-stu-id="577dd-118">authentication-basic</span></span>|<span data-ttu-id="577dd-119">Element główny.</span><span class="sxs-lookup"><span data-stu-id="577dd-119">Root element.</span></span>|<span data-ttu-id="577dd-120">Tak</span><span class="sxs-lookup"><span data-stu-id="577dd-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="577dd-121">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="577dd-121">Attributes</span></span>  
  
|<span data-ttu-id="577dd-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="577dd-122">Name</span></span>|<span data-ttu-id="577dd-123">Opis</span><span class="sxs-lookup"><span data-stu-id="577dd-123">Description</span></span>|<span data-ttu-id="577dd-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="577dd-124">Required</span></span>|<span data-ttu-id="577dd-125">Domyślne</span><span class="sxs-lookup"><span data-stu-id="577dd-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="577dd-126">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="577dd-126">username</span></span>|<span data-ttu-id="577dd-127">Określa nazwy użytkownika hello hello podstawowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="577dd-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="577dd-128">Tak</span><span class="sxs-lookup"><span data-stu-id="577dd-128">Yes</span></span>|<span data-ttu-id="577dd-129">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="577dd-129">N/A</span></span>|  
|<span data-ttu-id="577dd-130">hasło</span><span class="sxs-lookup"><span data-stu-id="577dd-130">password</span></span>|<span data-ttu-id="577dd-131">Określa hasło hello hello podstawowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="577dd-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="577dd-132">Tak</span><span class="sxs-lookup"><span data-stu-id="577dd-132">Yes</span></span>|<span data-ttu-id="577dd-133">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="577dd-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="577dd-134">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="577dd-134">Usage</span></span>  
 <span data-ttu-id="577dd-135">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="577dd-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="577dd-136">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="577dd-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="577dd-137">**Zakresy zasad:** interfejsu API</span><span class="sxs-lookup"><span data-stu-id="577dd-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="577dd-138"><a name="ClientCertificate"></a>Uwierzytelniania za pomocą certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="577dd-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="577dd-139">Użyj hello `authentication-certificate` tooauthenticate zasad z usługi wewnętrznej bazy danych przy użyciu certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="577dd-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="577dd-140">certyfikat Hello musi toobe [zainstalowane do interfejsu API zarządzania](http://go.microsoft.com/fwlink/?LinkID=511599) pierwszy i jest identyfikowany przez jego odcisk palca.</span><span class="sxs-lookup"><span data-stu-id="577dd-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="577dd-141">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="577dd-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="577dd-142">Przykład</span><span class="sxs-lookup"><span data-stu-id="577dd-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="577dd-143">Elementy</span><span class="sxs-lookup"><span data-stu-id="577dd-143">Elements</span></span>  
  
|<span data-ttu-id="577dd-144">Nazwa</span><span class="sxs-lookup"><span data-stu-id="577dd-144">Name</span></span>|<span data-ttu-id="577dd-145">Opis</span><span class="sxs-lookup"><span data-stu-id="577dd-145">Description</span></span>|<span data-ttu-id="577dd-146">Wymagane</span><span class="sxs-lookup"><span data-stu-id="577dd-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="577dd-147">certyfikat uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="577dd-147">authentication-certificate</span></span>|<span data-ttu-id="577dd-148">Element główny.</span><span class="sxs-lookup"><span data-stu-id="577dd-148">Root element.</span></span>|<span data-ttu-id="577dd-149">Tak</span><span class="sxs-lookup"><span data-stu-id="577dd-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="577dd-150">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="577dd-150">Attributes</span></span>  
  
|<span data-ttu-id="577dd-151">Nazwa</span><span class="sxs-lookup"><span data-stu-id="577dd-151">Name</span></span>|<span data-ttu-id="577dd-152">Opis</span><span class="sxs-lookup"><span data-stu-id="577dd-152">Description</span></span>|<span data-ttu-id="577dd-153">Wymagane</span><span class="sxs-lookup"><span data-stu-id="577dd-153">Required</span></span>|<span data-ttu-id="577dd-154">Domyślne</span><span class="sxs-lookup"><span data-stu-id="577dd-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="577dd-155">Odcisk palca</span><span class="sxs-lookup"><span data-stu-id="577dd-155">thumbprint</span></span>|<span data-ttu-id="577dd-156">Witaj odcisk palca certyfikatu klienta hello.</span><span class="sxs-lookup"><span data-stu-id="577dd-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="577dd-157">Tak</span><span class="sxs-lookup"><span data-stu-id="577dd-157">Yes</span></span>|<span data-ttu-id="577dd-158">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="577dd-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="577dd-159">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="577dd-159">Usage</span></span>  
 <span data-ttu-id="577dd-160">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="577dd-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="577dd-161">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="577dd-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="577dd-162">**Zakresy zasad:** interfejsu API</span><span class="sxs-lookup"><span data-stu-id="577dd-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="577dd-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="577dd-163">Next steps</span></span>
<span data-ttu-id="577dd-164">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="577dd-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  