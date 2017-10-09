---
title: "aaaAzure zarządzanych aplikacji przekazywaniem plików elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Common.FileUpload interfejsu użytkownika dla aplikacji Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="fe9d0-103">Element Microsoft.Common.FileUpload interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe9d0-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="fe9d0-104">Formant, który umożliwia toospecify użytkownika jednego lub więcej plików tooupload.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="fe9d0-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fe9d0-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="fe9d0-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fe9d0-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="fe9d0-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="fe9d0-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="fe9d0-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fe9d0-109">Remarks</span></span>
- <span data-ttu-id="fe9d0-110">`constraints.accept`Określa hello typy plików, które są wyświetlane w oknie dialogowym pliku hello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="fe9d0-111">Zobacz hello [specyfikacji HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) dla dozwolone wartości.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="fe9d0-112">Witaj, wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-112">hello default value is **null**.</span></span>
- <span data-ttu-id="fe9d0-113">Jeśli `options.multiple` ustawiono zbyt**true**, hello użytkownik może tooselect więcej niż jeden plik w przeglądarce hello okna dialogowego pliku.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="fe9d0-114">Witaj, wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-114">hello default value is **false**.</span></span>
- <span data-ttu-id="fe9d0-115">Ten element obsługuje przekazywanie plików w dwóch trybach na podstawie wartości hello `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="fe9d0-116">Jeśli **pliku** jest określony, dane wyjściowe hello zawierają hello zawartość pliku hello jako obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="fe9d0-117">Jeśli **adres url** jest określony, program hello plik jest przekazany tooa tymczasowej lokalizacji, a hello dane wyjściowe zawierają hello adres URL obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="fe9d0-118">Tymczasowe obiekty BLOB zostaną usunięte po 24 godzinach.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="fe9d0-119">Witaj, wartość domyślna to **pliku**.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-119">hello default value is **file**.</span></span>
- <span data-ttu-id="fe9d0-120">Witaj wartość `options.openMode` Określa, jak plik hello jest do odczytu.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="fe9d0-121">Jeśli plik hello jest oczekiwany toobe zwykłego tekstu, określ **tekst**; w przeciwnym razie, określ **binarne**.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="fe9d0-122">Witaj, wartość domyślna to **tekstu**.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-122">hello default value is **text**.</span></span>
- <span data-ttu-id="fe9d0-123">Jeśli `options.uploadMode` ustawiono zbyt**pliku** i `options.openMode` ustawiono zbyt**binarne**, dane wyjściowe hello jest zakodowany w formacie base64.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="fe9d0-124">`options.encoding`Określa kodowanie toouse hello podczas odczytywania pliku hello.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="fe9d0-125">Witaj, wartość domyślna to **UTF-8**i jest używany tylko wtedy, gdy `options.openMode` ustawiono zbyt**tekstu**.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="fe9d0-126">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="fe9d0-126">Sample output</span></span>
<span data-ttu-id="fe9d0-127">Jeśli options.uploadMode jest plikiem options.multiple ma wartość false, następnie dane wyjściowe zawierają hello zawartość pliku hello jako ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="fe9d0-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="fe9d0-128">Jeśli options.multiple ma wartość true and'options.uploadMode pliku, wówczas dane wyjściowe zawierają hello zawartość plików hello jako tablica JSON:</span><span class="sxs-lookup"><span data-stu-id="fe9d0-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="fe9d0-129">Jeśli adres url jest options.uploadMode options.multiple ma wartość false, następnie dane wyjściowe zawiera adres URL jako ciągu JSON:</span><span class="sxs-lookup"><span data-stu-id="fe9d0-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="fe9d0-130">Jeśli adres url jest options.uploadMode options.multiple ma wartość true, następnie dane wyjściowe zawierają listę adresów URL jako tablica JSON:</span><span class="sxs-lookup"><span data-stu-id="fe9d0-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="fe9d0-131">Podczas testowania CreateUiDefinition, niektóre przeglądarki (np. Google Chrome) obciąć wygenerowanym przez element Microsoft.Common.FileUpload hello w konsoli przeglądarki hello adresów URL.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="fe9d0-132">Może być konieczne kliknięcie tooright poszczególnych łączy toocopy hello pełne adresy URL.</span><span class="sxs-lookup"><span data-stu-id="fe9d0-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fe9d0-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe9d0-133">Next steps</span></span>
* <span data-ttu-id="fe9d0-134">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe9d0-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="fe9d0-135">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe9d0-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="fe9d0-136">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="fe9d0-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
