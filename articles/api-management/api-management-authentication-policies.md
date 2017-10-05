---
title: "Zasady uwierzytelniania usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad uwierzytelniania można używać usługi Azure API Management."
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
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="0ce95-103">Zarządzanie interfejsami API zasady uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="0ce95-103">API Management authentication policies</span></span>
<span data-ttu-id="0ce95-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="0ce95-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="0ce95-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="0ce95-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="0ce95-106"><a name="AuthenticationPolicies"></a>Zasady uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="0ce95-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="0ce95-107">[Uwierzytelnianie za pomocą Basic](api-management-authentication-policies.md#Basic) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="0ce95-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="0ce95-108">[Uwierzytelniania za pomocą certyfikatu klienta](api-management-authentication-policies.md#ClientCertificate) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="0ce95-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="0ce95-109"><a name="Basic"></a>Uwierzytelniania Basic</span><span class="sxs-lookup"><span data-stu-id="0ce95-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="0ce95-110">Użyj `authentication-basic` zasad uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="0ce95-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="0ce95-111">Ta zasada efektywnie ustawia dla nagłówka HTTP autoryzacji wartość odpowiadającą poświadczenia podane w zasadach.</span><span class="sxs-lookup"><span data-stu-id="0ce95-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0ce95-112">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="0ce95-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="0ce95-113">Przykład</span><span class="sxs-lookup"><span data-stu-id="0ce95-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="0ce95-114">Elementy</span><span class="sxs-lookup"><span data-stu-id="0ce95-114">Elements</span></span>  
  
|<span data-ttu-id="0ce95-115">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0ce95-115">Name</span></span>|<span data-ttu-id="0ce95-116">Opis</span><span class="sxs-lookup"><span data-stu-id="0ce95-116">Description</span></span>|<span data-ttu-id="0ce95-117">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0ce95-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0ce95-118">Uwierzytelnianie — podstawowy</span><span class="sxs-lookup"><span data-stu-id="0ce95-118">authentication-basic</span></span>|<span data-ttu-id="0ce95-119">Element główny.</span><span class="sxs-lookup"><span data-stu-id="0ce95-119">Root element.</span></span>|<span data-ttu-id="0ce95-120">Tak</span><span class="sxs-lookup"><span data-stu-id="0ce95-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0ce95-121">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0ce95-121">Attributes</span></span>  
  
|<span data-ttu-id="0ce95-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0ce95-122">Name</span></span>|<span data-ttu-id="0ce95-123">Opis</span><span class="sxs-lookup"><span data-stu-id="0ce95-123">Description</span></span>|<span data-ttu-id="0ce95-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0ce95-124">Required</span></span>|<span data-ttu-id="0ce95-125">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0ce95-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0ce95-126">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="0ce95-126">username</span></span>|<span data-ttu-id="0ce95-127">Określa nazwę użytkownika, podstawowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="0ce95-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="0ce95-128">Tak</span><span class="sxs-lookup"><span data-stu-id="0ce95-128">Yes</span></span>|<span data-ttu-id="0ce95-129">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0ce95-129">N/A</span></span>|  
|<span data-ttu-id="0ce95-130">hasło</span><span class="sxs-lookup"><span data-stu-id="0ce95-130">password</span></span>|<span data-ttu-id="0ce95-131">Określa hasło podstawowych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0ce95-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="0ce95-132">Tak</span><span class="sxs-lookup"><span data-stu-id="0ce95-132">Yes</span></span>|<span data-ttu-id="0ce95-133">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0ce95-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0ce95-134">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="0ce95-134">Usage</span></span>  
 <span data-ttu-id="0ce95-135">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="0ce95-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0ce95-136">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="0ce95-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0ce95-137">**Zakresy zasad:** interfejsu API</span><span class="sxs-lookup"><span data-stu-id="0ce95-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="0ce95-138"><a name="ClientCertificate"></a>Uwierzytelniania za pomocą certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="0ce95-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="0ce95-139">Użyj `authentication-certificate` zasad uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="0ce95-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="0ce95-140">Ten certyfikat musi być [zainstalowane do interfejsu API zarządzania](http://go.microsoft.com/fwlink/?LinkID=511599) pierwszy i jest identyfikowany przez jego odcisk palca.</span><span class="sxs-lookup"><span data-stu-id="0ce95-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0ce95-141">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="0ce95-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="0ce95-142">Przykład</span><span class="sxs-lookup"><span data-stu-id="0ce95-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="0ce95-143">Elementy</span><span class="sxs-lookup"><span data-stu-id="0ce95-143">Elements</span></span>  
  
|<span data-ttu-id="0ce95-144">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0ce95-144">Name</span></span>|<span data-ttu-id="0ce95-145">Opis</span><span class="sxs-lookup"><span data-stu-id="0ce95-145">Description</span></span>|<span data-ttu-id="0ce95-146">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0ce95-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0ce95-147">certyfikat uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="0ce95-147">authentication-certificate</span></span>|<span data-ttu-id="0ce95-148">Element główny.</span><span class="sxs-lookup"><span data-stu-id="0ce95-148">Root element.</span></span>|<span data-ttu-id="0ce95-149">Tak</span><span class="sxs-lookup"><span data-stu-id="0ce95-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0ce95-150">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0ce95-150">Attributes</span></span>  
  
|<span data-ttu-id="0ce95-151">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0ce95-151">Name</span></span>|<span data-ttu-id="0ce95-152">Opis</span><span class="sxs-lookup"><span data-stu-id="0ce95-152">Description</span></span>|<span data-ttu-id="0ce95-153">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0ce95-153">Required</span></span>|<span data-ttu-id="0ce95-154">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0ce95-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0ce95-155">Odcisk palca</span><span class="sxs-lookup"><span data-stu-id="0ce95-155">thumbprint</span></span>|<span data-ttu-id="0ce95-156">Odcisk palca certyfikatu klienta.</span><span class="sxs-lookup"><span data-stu-id="0ce95-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="0ce95-157">Tak</span><span class="sxs-lookup"><span data-stu-id="0ce95-157">Yes</span></span>|<span data-ttu-id="0ce95-158">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0ce95-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0ce95-159">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="0ce95-159">Usage</span></span>  
 <span data-ttu-id="0ce95-160">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="0ce95-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0ce95-161">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="0ce95-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0ce95-162">**Zakresy zasad:** interfejsu API</span><span class="sxs-lookup"><span data-stu-id="0ce95-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="0ce95-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ce95-163">Next steps</span></span>
<span data-ttu-id="0ce95-164">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="0ce95-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  