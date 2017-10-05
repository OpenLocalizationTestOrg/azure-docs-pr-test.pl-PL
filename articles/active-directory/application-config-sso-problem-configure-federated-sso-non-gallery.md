---
title: "Problem podczas konfiguracji federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii | Dokumentacja firmy Microsoft"
description: "Rozwiązania niektórych typowych problemów, które mogą wystąpić podczas konfigurowania federacyjne logowanie jednokrotne do aplikacji SAML niestandardowego, który nie znajduje się w galerii aplikacji usługi Azure AD"
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
ms.openlocfilehash: 4eb2c04c940dd6ad15a491a331aed76c237f0387
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="b44fe-103">Problem podczas konfiguracji federacyjne logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="b44fe-103">Problem configuring federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="b44fe-104">Jeśli napotkasz problem podczas konfigurowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b44fe-104">If you encounter a problem when configuring an application.</span></span> <span data-ttu-id="b44fe-105">Sprawdź zostały wykonane wszystkie kroki opisane w artykule [konfigurowania rejestracji jednokrotnej do aplikacji, które nie znajdują się w galerii aplikacji usługi Azure Active Directory.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span><span class="sxs-lookup"><span data-stu-id="b44fe-105">Verify you have followed all the steps in the article [Configuring single sign-on to applications that are not in the Azure Active Directory application gallery.](https://docs.microsoft.com/azure/active-directory/active-directory-saas-custom-apps)</span></span>

## <a name="cant-add-another-instance-of-the-application"></a><span data-ttu-id="b44fe-106">Nie można dodać inne wystąpienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b44fe-106">Can’t add another instance of the application</span></span>

<span data-ttu-id="b44fe-107">Aby dodać drugie wystąpienie aplikacji, musisz mieć możliwość:</span><span class="sxs-lookup"><span data-stu-id="b44fe-107">To add a second instance of an application, you need to be able to:</span></span>

-   <span data-ttu-id="b44fe-108">Skonfiguruj Unikatowy identyfikator dla drugiego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="b44fe-108">Configure a unique identifier for the second instance.</span></span> <span data-ttu-id="b44fe-109">Nie można skonfigurować w taki sam identyfikator używany po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="b44fe-109">You won’t be able to configure the same identifier used for the first instance.</span></span>

-   <span data-ttu-id="b44fe-110">Skonfiguruj inny certyfikat niż w pierwszym wystąpieniu.</span><span class="sxs-lookup"><span data-stu-id="b44fe-110">Configure a different certificate than the one used for the first instance.</span></span>

<span data-ttu-id="b44fe-111">Jeśli aplikacja nie obsługuje dowolne z powyższych.</span><span class="sxs-lookup"><span data-stu-id="b44fe-111">If the application doesn’t support any of the above.</span></span> <span data-ttu-id="b44fe-112">Następnie, nie będzie można skonfigurować drugie wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="b44fe-112">Then, you won’t be able to configure a second instance.</span></span>

## <a name="where-do-i-set-the-entityid-user-identifier-format"></a><span data-ttu-id="b44fe-113">Gdy ustawienie formatu EntityID (identyfikator użytkownika)</span><span class="sxs-lookup"><span data-stu-id="b44fe-113">Where do I set the EntityID (User Identifier) format</span></span>

<span data-ttu-id="b44fe-114">Nie można wybrać format EntityID (identyfikator użytkownika) usługi Azure AD wysyła do aplikacji w odpowiedzi po uwierzytelnieniu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b44fe-114">You won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="b44fe-115">Wybrano Azure wybierz AD format dla atrybutu NameID (identyfikator użytkownika) na podstawie wartości lub format żądany przez aplikację w SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="b44fe-115">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="b44fe-116">Aby uzyskać więcej informacji można znaleźć w artykule [protokołu SAML rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) w sekcji NameIDPolicy,</span><span class="sxs-lookup"><span data-stu-id="b44fe-116">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy,</span></span>

## <a name="where-do-i-get-the-application-metadata-or-certificate-from-azure-ad"></a><span data-ttu-id="b44fe-117">Gdzie uzyskać metadanych aplikacji lub certyfikatu z usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b44fe-117">Where do I get the application metadata or certificate from Azure AD</span></span>

<span data-ttu-id="b44fe-118">Aby pobrać metadanych aplikacji lub certyfikatu z usługi Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b44fe-118">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="b44fe-119">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="b44fe-119">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="b44fe-120">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b44fe-120">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="b44fe-121">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="b44fe-121">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="b44fe-122">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b44fe-122">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="b44fe-123">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b44fe-123">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="b44fe-124">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="b44fe-124">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="b44fe-125">Wybierz aplikację, skonfigurowaniu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="b44fe-125">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="b44fe-126">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b44fe-126">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="b44fe-127">Przejdź do **certyfikat podpisywania SAML** sekcji, a następnie kliknij przycisk **Pobierz** wartość w kolumnie.</span><span class="sxs-lookup"><span data-stu-id="b44fe-127">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="b44fe-128">W zależności od tego, jakie aplikacji wymaga Konfigurowanie logowania jednokrotnego zobaczysz opcję, aby pobrać metadane XML albo certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="b44fe-128">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="b44fe-129">Usługi Azure AD nie udostępnia adresu URL można pobrać metadanych.</span><span class="sxs-lookup"><span data-stu-id="b44fe-129">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="b44fe-130">Można pobrać metadanych jako plik XML.</span><span class="sxs-lookup"><span data-stu-id="b44fe-130">The metadata can only be retrieved as a XML file.</span></span>

## <a name="dont-know-how-to-customize-saml-claims-sent-to-an-application"></a><span data-ttu-id="b44fe-131">Nie wiadomo, jak dostosować SAML oświadczenia wysyłane do aplikacji</span><span class="sxs-lookup"><span data-stu-id="b44fe-131">Don't know how to customize SAML claims sent to an application</span></span>

<span data-ttu-id="b44fe-132">Aby dowiedzieć się, jak dostosować oświadczeń atrybutów SAML wysyłanych do aplikacji, zobacz [oświadczeń mapowanie w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="b44fe-132">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b44fe-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b44fe-133">Next steps</span></span>
[<span data-ttu-id="b44fe-134">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b44fe-134">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
