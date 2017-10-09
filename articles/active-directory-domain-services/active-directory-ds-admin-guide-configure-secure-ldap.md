---
title: "aaaConfigure bezpieczny protokół LDAP (LDAPS) w usługach domenowych Azure AD | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="fe318-103">Konfigurowanie bezpiecznego protokołu LDAP (LDAPS) dla domeny zarządzanej usług domenowych Azure AD</span><span class="sxs-lookup"><span data-stu-id="fe318-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="fe318-104">W tym artykule opisano, jak można włączyć bezpieczny Lightweight Directory dostępu protokołu (LDAPS) dla domeny zarządzanej usług domenowych Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe318-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="fe318-105">Bezpiecznego protokołu LDAP jest także znana jako "dostępu protokołu LDAP (Lightweight Directory) za pośrednictwem Secure Sockets Layer (SSL) / zabezpieczeń TLS (Transport Layer)".</span><span class="sxs-lookup"><span data-stu-id="fe318-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fe318-106">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="fe318-106">Before you begin</span></span>
<span data-ttu-id="fe318-107">zadania hello tooperform wymienione w tym artykule, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="fe318-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="fe318-108">Prawidłowy **subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="fe318-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="fe318-109">**Katalog usługi Azure AD** -albo synchronizowane z katalogu lokalnego lub w katalogu tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="fe318-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="fe318-110">**Usługi domenowe Azure AD** musi być włączona dla katalogu hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fe318-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="fe318-111">Jeśli nie zostało to jeszcze zrobione, należy wykonać wszystkie zadania hello opisane w hello [Przewodnik wprowadzający](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fe318-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="fe318-112">A **tooenable toobe używany certyfikat bezpieczny protokół LDAP**.</span><span class="sxs-lookup"><span data-stu-id="fe318-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="fe318-113">**Zalecane** -uzyskać certyfikat od zaufanego publicznego urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="fe318-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="fe318-114">Ta opcja konfiguracji jest bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="fe318-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="fe318-115">Alternatywnie można też zbyt[Utwórz certyfikat z podpisem własnym](#task-1---obtain-a-certificate-for-secure-ldap) jak pokazano w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="fe318-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="fe318-116">Wymagania dotyczące bezpiecznego certyfikatu LDAP hello</span><span class="sxs-lookup"><span data-stu-id="fe318-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="fe318-117">Uzyskać prawidłowy certyfikat na powitania następujące wytyczne, przed włączeniem bezpiecznego protokołu LDAP.</span><span class="sxs-lookup"><span data-stu-id="fe318-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="fe318-118">Wystąpią błędy, Jeśli spróbujesz tooenable bezpieczny protokół LDAP do domeny zarządzanej za pomocą certyfikatu nieprawidłowa lub być niepoprawne.</span><span class="sxs-lookup"><span data-stu-id="fe318-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="fe318-119">**Zaufanych wystawców** -hello certyfikat musi być wystawiony przez urząd certyfikacji zaufany przez komputery łączenie toohello domeny zarządzanej przy użyciu bezpiecznego protokołu LDAP.</span><span class="sxs-lookup"><span data-stu-id="fe318-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="fe318-120">Ten urząd może być publiczny urząd certyfikacji zaufany przez te komputery.</span><span class="sxs-lookup"><span data-stu-id="fe318-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="fe318-121">**Okres istnienia** -hello certyfikatu musi być prawidłowy dla co najmniej hello kolejnych 3 – 6 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="fe318-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="fe318-122">Bezpieczne LDAP dostępu tooyour domeny zarządzanej jest zakłócona po wygaśnięciu certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="fe318-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="fe318-123">**Nazwa podmiotu** -hello nazwa podmiotu certyfikatu hello musi być symbolem wieloznacznym dla domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="fe318-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="fe318-124">Na przykład, jeśli domena ma nazwę "contoso100.com", nazwa podmiotu certyfikatu hello musi być "*. contoso100.com".</span><span class="sxs-lookup"><span data-stu-id="fe318-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="fe318-125">Ustaw hello DNS (alternatywnej nazwy podmiotu) toothis symbolu wieloznacznego nazwa.</span><span class="sxs-lookup"><span data-stu-id="fe318-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="fe318-126">**Użycie klucza** - hello certyfikat musi być skonfigurowany dla używa powitania po - podpisy cyfrowe i szyfrowanie klucza.</span><span class="sxs-lookup"><span data-stu-id="fe318-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="fe318-127">**Cel certyfikatu** -hello certyfikatu musi być prawidłowy do uwierzytelniania serwera SSL.</span><span class="sxs-lookup"><span data-stu-id="fe318-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="fe318-128">**Urzędy certyfikacji przedsiębiorstwa:** usługi domenowe Azure AD nie obsługuje korzystania z bezpiecznego certyfikatów LDAP wystawiony przez urząd certyfikacji przedsiębiorstwa w organizacji.</span><span class="sxs-lookup"><span data-stu-id="fe318-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="fe318-129">To ograniczenie obowiązuje, ponieważ hello usługi nie jest zaufany urząd certyfikacji jako główny urząd certyfikacji przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="fe318-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="fe318-130">Zadanie 1 — Uzyskaj certyfikat dla bezpiecznego protokołu LDAP</span><span class="sxs-lookup"><span data-stu-id="fe318-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="fe318-131">pierwszym zadaniem Hello obejmuje uzyskiwanie certyfikatu używany do bezpiecznego LDAP dostępu toohello domeny zarządzanej.</span><span class="sxs-lookup"><span data-stu-id="fe318-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="fe318-132">Dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="fe318-132">You have two options:</span></span>

* <span data-ttu-id="fe318-133">Uzyskaj certyfikat od urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="fe318-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="fe318-134">Urząd Hello może być publiczny urząd certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="fe318-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="fe318-135">Tworzenie certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="fe318-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="fe318-136">Opcja (zalecane) — Uzyskaj certyfikat bezpiecznego LDAP z urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="fe318-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="fe318-137">Jeśli Twoja organizacja uzyskuje jego certyfikatów z publicznego urzędu certyfikacji, należy tooobtain hello bezpiecznego LDAP certyfikatu z tym publicznego urzędu certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="fe318-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="fe318-138">Podczas żądania certyfikatu, upewnij się, że spełniają wszystkie wymagania hello opisane w temacie [wymagania dotyczące bezpiecznego certyfikatu LDAP hello](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="fe318-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="fe318-139">Komputery klienckie, które wymagają tooconnect toohello domeny zarządzanej przy użyciu bezpiecznego protokołu LDAP muszą ufać Witaj wystawca hello bezpiecznego LDAP certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="fe318-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="fe318-140">Opcja B - Tworzenie certyfikatu z podpisem własnym dla bezpiecznego protokołu LDAP</span><span class="sxs-lookup"><span data-stu-id="fe318-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="fe318-141">Jeśli nie planujesz toouse certyfikatów z publicznego urzędu certyfikacji, można wybrać toocreate certyfikatu z podpisem własnym dla bezpiecznego protokołu LDAP.</span><span class="sxs-lookup"><span data-stu-id="fe318-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="fe318-142">**Tworzenie certyfikatu z podpisem własnym za pomocą programu PowerShell**</span><span class="sxs-lookup"><span data-stu-id="fe318-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="fe318-143">Na komputerze z systemem Windows, Otwórz nowe okno programu PowerShell jako **administratora** i typ hello następujące polecenia, toocreate nowego certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="fe318-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="fe318-144">W powyższej przykładowej hello, zastąp "*. contoso100.com" z nazwą domeny DNS hello domeny zarządzanej. For example, jeśli utworzono o nazwie "contoso100.onmicrosoft.com" domeny zarządzanej, zastąp "*. contoso100.com" w hello powyżej skryptu "*. contoso100.onmicrosoft.com").</span><span class="sxs-lookup"><span data-stu-id="fe318-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![Wybieranie katalogu usługi Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="fe318-146">Witaj nowo utworzonego certyfikatu z podpisem własnym znajduje się w magazynie certyfikatów komputera lokalnego hello.</span><span class="sxs-lookup"><span data-stu-id="fe318-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="fe318-147">Następny krok</span><span class="sxs-lookup"><span data-stu-id="fe318-147">Next step</span></span>
[<span data-ttu-id="fe318-148">Zadanie 2 — wyeksportować hello bezpiecznego tooa certyfikatu LDAP. Plik PFX</span><span class="sxs-lookup"><span data-stu-id="fe318-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
