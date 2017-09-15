---
title: "Usługi Azure AD w wersji 2 dla systemu Android pobieranie rozpoczęte — Instalatora | Dokumentacja firmy Microsoft"
description: "Jak uzyskać token dostępu i wywołania interfejsu API programu Microsoft Graph lub interfejsów API, które wymagają tokenów dostępu z usługą Azure Active Directory v2 końcowego region systemu Android"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: a43d7e30a6f4176afba27f0de2c2c116df741080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="de8a6-103">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="de8a6-103">Set up your project</span></span>

> <span data-ttu-id="de8a6-104">Preferowane jest zamiast tego Pobierz ten przykładowy projekt programu Android Studio?</span><span class="sxs-lookup"><span data-stu-id="de8a6-104">Prefer to download this sample's Android Studio project instead?</span></span> <span data-ttu-id="de8a6-105">[Pobieranie projektu](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) i przejść [kroku konfiguracji](#create-an-application-express) skonfigurować przykładowy kod przed wykonaniem.</span><span class="sxs-lookup"><span data-stu-id="de8a6-105">[Download a project](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing    .</span></span>


### <a name="create-a-new-project"></a><span data-ttu-id="de8a6-106">Tworzenie nowego projektu</span><span class="sxs-lookup"><span data-stu-id="de8a6-106">Create a new project</span></span> 
1.  <span data-ttu-id="de8a6-107">Otwórz program Android Studio, przejdź do:`File` > `New` > `New Project`</span><span class="sxs-lookup"><span data-stu-id="de8a6-107">Open Android Studio, go to: `File` > `New` > `New Project`</span></span>
2.  <span data-ttu-id="de8a6-108">Nazwa aplikacji, a następnie kliknij przycisk`Next`</span><span class="sxs-lookup"><span data-stu-id="de8a6-108">Name your application and click `Next`</span></span>
3.  <span data-ttu-id="de8a6-109">Upewnij się wybrać *21 interfejsu API lub nowszej (Android 5.0)* i kliknij przycisk`Next`</span><span class="sxs-lookup"><span data-stu-id="de8a6-109">Make sure to select *API 21 or newer (Android 5.0)* and click `Next`</span></span>
4.  <span data-ttu-id="de8a6-110">Pozostaw `Empty Activity`, kliknij przycisk `Next`, następnie`Finish`</span><span class="sxs-lookup"><span data-stu-id="de8a6-110">Leave `Empty Activity`, click `Next`, then `Finish`</span></span>


### <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="de8a6-111">Dodaj do projektu biblioteki uwierzytelniania firmy Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="de8a6-111">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1.  <span data-ttu-id="de8a6-112">W programie Android Studio przejdź do:`Gradle Scripts` > `build.gradle (Module: app)`</span><span class="sxs-lookup"><span data-stu-id="de8a6-112">In Android Studio, go to: `Gradle Scripts` > `build.gradle (Module: app)`</span></span>
2.  <span data-ttu-id="de8a6-113">Skopiuj i wklej następujący kod w obszarze `Dependencies`:</span><span class="sxs-lookup"><span data-stu-id="de8a6-113">Copy and paste the following code under `Dependencies`:</span></span>

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a><span data-ttu-id="de8a6-114">O tym pakiecie</span><span class="sxs-lookup"><span data-stu-id="de8a6-114">About this package</span></span>

<span data-ttu-id="de8a6-115">Powyżej pakiet instaluje biblioteki uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="de8a6-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="de8a6-116">MSAL obsługuje pobieranie, buforowanie i odświeżanie tokenów użytkownika, które umożliwiają dostęp do interfejsów API chronione przez punkt końcowy w wersji 2 usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="de8a6-116">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by Azure Active Directory v2 endpoint.</span></span>
<!--end-collapse-->

## <a name="create-your-applications-ui"></a><span data-ttu-id="de8a6-117">Tworzenie aplikacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="de8a6-117">Create your application’s UI</span></span>

1.  <span data-ttu-id="de8a6-118">Otwórz: `activity_main.xml` w obszarze`res` > `layout`</span><span class="sxs-lookup"><span data-stu-id="de8a6-118">Open: `activity_main.xml` under `res` > `layout`</span></span>
2.  <span data-ttu-id="de8a6-119">Zmian układu działania z `android.support.constraint.ConstraintLayout` lub innych do`LinearLayout`</span><span class="sxs-lookup"><span data-stu-id="de8a6-119">Change the activity layout from `android.support.constraint.ConstraintLayout` or other to `LinearLayout`</span></span>
3.  <span data-ttu-id="de8a6-120">Dodaj `android:orientation="vertical"` właściwości `LinearLayout` węzła</span><span class="sxs-lookup"><span data-stu-id="de8a6-120">Add `android:orientation="vertical"` property to `LinearLayout` node</span></span>
4.  <span data-ttu-id="de8a6-121">Skopiuj i wklej następujący kod do `LinearLayout` węzła, zastępując bieżący zawartości:</span><span class="sxs-lookup"><span data-stu-id="de8a6-121">Copy and paste the following code into the `LinearLayout` node, replacing the current content:</span></span>

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

