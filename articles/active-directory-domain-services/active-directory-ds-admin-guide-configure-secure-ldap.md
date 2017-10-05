---
title: "Skonfigurować bezpiecznego protokołu LDAP (LDAPS) w usługach domenowych Azure AD | Dokumentacja firmy Microsoft"
description: "Skonfiguruj zabezpieczenia protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 93afa49166c5b31d23237c308b9d34f6d6f3507d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="66683-103">Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="66683-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="66683-104">W tym artykule opisano, jak można włączyć bezpieczny Lightweight Directory dostępu protokołu (LDAPS) dla domeny zarządzanej usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66683-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="66683-105">Bezpiecznego protokołu LDAP jest także znana jako "dostępu protokołu LDAP (Lightweight Directory) za pośrednictwem Secure Sockets Layer (SSL) / zabezpieczeń TLS (Transport Layer)".</span><span class="sxs-lookup"><span data-stu-id="66683-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="66683-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="66683-106">Before you begin</span></span>
<span data-ttu-id="66683-107">Aby wykonać zadania opisane w tym artykule, należy:</span><span class="sxs-lookup"><span data-stu-id="66683-107">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="66683-108">Prawidłowy **subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="66683-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="66683-109">**Katalog usługi Azure AD** -albo synchronizowane z katalogu lokalnego lub w katalogu tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="66683-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="66683-110">**Usługi domenowe Azure AD** musi być włączona dla katalogu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66683-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="66683-111">Jeśli nie zostało to jeszcze zrobione, należy wykonać wszystkie zadania opisane w temacie [Przewodnik wprowadzający](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="66683-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="66683-112">A **certyfikat użyty do włączenia bezpiecznego protokołu LDAP**.</span><span class="sxs-lookup"><span data-stu-id="66683-112">A **certificate to be used to enable secure LDAP**.</span></span>

   * <span data-ttu-id="66683-113">**Zalecane** -uzyskać certyfikat od zaufanego publicznego urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="66683-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="66683-114">Ta opcja konfiguracji jest bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="66683-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="66683-115">Alternatywnie można również wybrać opcję [Utwórz certyfikat z podpisem własnym](#task-1---obtain-a-certificate-for-secure-ldap) jak pokazano w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="66683-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-the-secure-ldap-certificate"></a><span data-ttu-id="66683-116">Wymagania dotyczące bezpiecznego certyfikatu LDAP</span><span class="sxs-lookup"><span data-stu-id="66683-116">Requirements for the secure LDAP certificate</span></span>
<span data-ttu-id="66683-117">Przed włączeniem bezpiecznego protokołu LDAP, należy uzyskać prawidłowy certyfikat dla następujących wytycznych.</span><span class="sxs-lookup"><span data-stu-id="66683-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="66683-118">Wystąpią błędy, jeśli próbujesz włączyć bezpiecznego protokołu LDAP do domeny zarządzanej za pomocą certyfikatu nieprawidłowa lub być niepoprawne.</span><span class="sxs-lookup"><span data-stu-id="66683-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="66683-119">**Zaufanych wystawców** — certyfikat musi być wystawiony przez urząd certyfikacji zaufany przez komputery łączenie domeny zarządzanej przy użyciu bezpiecznego protokołu LDAP.</span><span class="sxs-lookup"><span data-stu-id="66683-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers connecting to the managed domain using secure LDAP.</span></span> <span data-ttu-id="66683-120">Ten urząd może być publiczny urząd certyfikacji zaufany przez te komputery.</span><span class="sxs-lookup"><span data-stu-id="66683-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="66683-121">**Okres istnienia** — certyfikat musi być prawidłowy, przez co najmniej dalej 3 – 6 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="66683-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span></span> <span data-ttu-id="66683-122">Bezpieczny dostęp LDAP do domeny zarządzanej jest zakłócona po wygaśnięciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="66683-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span></span>
3. <span data-ttu-id="66683-123">**Nazwa podmiotu** — nazwa podmiotu certyfikatu musi być symbolem wieloznacznym dla domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="66683-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="66683-124">Na przykład, jeśli domena ma nazwę "contoso100.com", nazwa podmiotu certyfikatu musi być "*. contoso100.com".</span><span class="sxs-lookup"><span data-stu-id="66683-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="66683-125">Ustaw nazwę DNS (alternatywnej nazwy podmiotu) ta nazwa symbolu wieloznacznego.</span><span class="sxs-lookup"><span data-stu-id="66683-125">Set the DNS name (subject alternate name) to this wildcard name.</span></span>
4. <span data-ttu-id="66683-126">**Użycie klucza** — certyfikat musi być skonfigurowany dla poniżej używa - podpisy cyfrowe i szyfrowanie klucza.</span><span class="sxs-lookup"><span data-stu-id="66683-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="66683-127">**Cel certyfikatu** -musi to być prawidłowy do uwierzytelniania serwera SSL.</span><span class="sxs-lookup"><span data-stu-id="66683-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="66683-128">**Urzędy certyfikacji przedsiębiorstwa:** usługi domenowe Azure AD nie obsługuje korzystania z bezpiecznego certyfikatów LDAP wystawiony przez urząd certyfikacji przedsiębiorstwa w organizacji.</span><span class="sxs-lookup"><span data-stu-id="66683-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="66683-129">To ograniczenie obowiązuje, ponieważ usługa nie jest zaufany urząd certyfikacji jako główny urząd certyfikacji przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="66683-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="66683-130">Zadanie 1 — Uzyskaj certyfikat dla bezpiecznego protokołu LDAP</span><span class="sxs-lookup"><span data-stu-id="66683-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="66683-131">Pierwszym zadaniem obejmuje uzyskiwanie certyfikatu używany do bezpiecznego dostępu LDAP do domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="66683-131">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="66683-132">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="66683-132">You have two options:</span></span>

* <span data-ttu-id="66683-133">Uzyskaj certyfikat od urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="66683-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="66683-134">Urząd może być publiczny urząd certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="66683-134">The authority may be a public certification authority.</span></span>
* <span data-ttu-id="66683-135">Tworzenie certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="66683-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="66683-136">Opcja (zalecane) — Uzyskaj certyfikat bezpiecznego LDAP z urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="66683-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="66683-137">Jeśli Twoja organizacja uzyskuje jego certyfikatów z publicznego urzędu certyfikacji, należy uzyskać bezpiecznego certyfikatu LDAP z tym publicznego urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="66683-137">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="66683-138">Podczas żądania certyfikatu, upewnij się, że spełniają wszystkie wymagania opisane w temacie [wymagania dotyczące bezpiecznego certyfikatu LDAP](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="66683-138">When requesting a certificate, ensure that you satisfy all the requirements outlined in [Requirements for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="66683-139">Komputery klienckie, które łączą się do domeny zarządzanej przy użyciu bezpiecznego protokołu LDAP muszą ufać wystawcy certyfikatu bezpiecznego LDAP.</span><span class="sxs-lookup"><span data-stu-id="66683-139">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="66683-140">Opcja B - Tworzenie certyfikatu z podpisem własnym dla bezpiecznego protokołu LDAP</span><span class="sxs-lookup"><span data-stu-id="66683-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="66683-141">Jeśli nie planujesz używać certyfikatów z publicznego urzędu certyfikacji, można utworzyć certyfikatu z podpisem własnym dla bezpiecznego protokołu LDAP.</span><span class="sxs-lookup"><span data-stu-id="66683-141">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="66683-142">**Tworzenie certyfikatu z podpisem własnym za pomocą programu PowerShell**</span><span class="sxs-lookup"><span data-stu-id="66683-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="66683-143">Na komputerze z systemem Windows, Otwórz nowe okno programu PowerShell jako **administratora** i wpisz następujące polecenia, aby utworzyć nowy certyfikat z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="66683-143">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="66683-144">W poprzednim przykładzie Zastąp "*. contoso100.com" z nazwą domeny DNS domeny zarządzanej. For example, jeśli utworzono o nazwie "contoso100.onmicrosoft.com" domeny zarządzanej, zastąp "*. contoso100.com" w powyższym skryptu "*. contoso100.onmicrosoft.com").</span><span class="sxs-lookup"><span data-stu-id="66683-144">In the preceding sample, replace '*.contoso100.com' with the DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in the above script with '*.contoso100.onmicrosoft.com').</span></span>

![Wybieranie katalogu usługi Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="66683-146">Nowo utworzony certyfikat z podpisem własnym znajduje się w magazynie certyfikatów komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="66683-146">The newly created self-signed certificate is placed in the local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="66683-147">Następny krok</span><span class="sxs-lookup"><span data-stu-id="66683-147">Next step</span></span>
[<span data-ttu-id="66683-148">Zadanie 2 — wyeksportowany certyfikat bezpiecznego LDAP. Plik PFX</span><span class="sxs-lookup"><span data-stu-id="66683-148">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
