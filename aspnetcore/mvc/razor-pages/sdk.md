---
title: ASP.NET Core Razor SDK
author: Rick-Anderson
description: Informazioni su come Razor Pages in ASP.NET Core semplifica e rende più produttiva la scrittura di codice incentrata sulle pagine rispetto a MVC.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 4/12/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: content
uid: mvc/razor-pages/sdk
ms.openlocfilehash: 2cbebb12ccd1098e1950aa7eeb22fab4ffc689e6
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2018
---
# <a name="aspnet-core-razor-sdk"></a><span data-ttu-id="02839-103">ASP.NET Core Razor SDK</span><span class="sxs-lookup"><span data-stu-id="02839-103">ASP.NET Core Razor SDK</span></span>

<span data-ttu-id="02839-104">Di [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="02839-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[](~/includes/2.1.md)]

<span data-ttu-id="02839-105">[!INCLUDE[](~/includes/2.1-SDK.md)] include MSBuild SDK di `Microsoft.NET.Sdk.Razor` (Razor SDK).</span><span class="sxs-lookup"><span data-stu-id="02839-105">The [!INCLUDE[](~/includes/2.1-SDK.md)] includes the `Microsoft.NET.Sdk.Razor` MSBuild SDK (Razor SDK).</span></span> <span data-ttu-id="02839-106">Il Razor SDK:</span><span class="sxs-lookup"><span data-stu-id="02839-106">The Razor SDK:</span></span>

* <span data-ttu-id="02839-107">Consente di standardizzare l'esperienza in termini di compilazione, creazione dei pacchetti e pubblicazione dei progetti contenenti file [Razor](xref:mvc/views/razor) per i progetti ASP.NET Core basati su MVC.</span><span class="sxs-lookup"><span data-stu-id="02839-107">Standardizes the experience around building, packaging, and publishing projects containing [Razor](xref:mvc/views/razor) files for ASP.NET Core MVC-based projects.</span></span>
* <span data-ttu-id="02839-108">Include un set di destinazioni, proprietà e di elementi predefiniti che consentono di personalizzare la compilazione dei file Razor.</span><span class="sxs-lookup"><span data-stu-id="02839-108">Includes a set of predefined targets, properties, and items that allow customizing the compilation of Razor files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02839-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="02839-109">Prerequisites</span></span>

[!INCLUDE[](~/includes/2.1-SDK.md)]

## <a name="using-the-razor-sdk"></a><span data-ttu-id="02839-110">Uso di Razor SDK</span><span class="sxs-lookup"><span data-stu-id="02839-110">Using the Razor SDK</span></span>

<span data-ttu-id="02839-111">La maggior parte delle app Web non deve fare espressamente riferimento a Razor SDK.</span><span class="sxs-lookup"><span data-stu-id="02839-111">Most web apps don't need to expressly reference the Razor SDK.</span></span> 

<span data-ttu-id="02839-112">Per usare il Razor SDK per compilare librerie di classi contenenti visualizzazioni Razor o Razor Pages:</span><span class="sxs-lookup"><span data-stu-id="02839-112">To use the Razor SDK to build class libraries containing Razor views or Razor Pages:</span></span>

* <span data-ttu-id="02839-113">Usare `Microsoft.NET.Sdk.Razor` anziché `Microsoft.NET.Sdk`:</span><span class="sxs-lookup"><span data-stu-id="02839-113">Use `Microsoft.NET.Sdk.Razor` instead of `Microsoft.NET.Sdk`:</span></span>
```xml
<Project SDK="Microsoft.NET.Sdk.Razor">
  ...
</Project>
```

* <span data-ttu-id="02839-114">In genere serve un riferimento al pacchetto a `Microsoft.AspNetCore.Mvc` per importare le dipendenze aggiuntive necessarie per generare e compilare visualizzazioni Razor o Razor Pages.</span><span class="sxs-lookup"><span data-stu-id="02839-114">Typically a package reference to `Microsoft.AspNetCore.Mvc` is required to bring in additional dependencies required to build and compile Razor Pages and Razor views.</span></span> <span data-ttu-id="02839-115">Come minimo, è necessario che il progetto aggiunga riferimenti al pacchetto a:</span><span class="sxs-lookup"><span data-stu-id="02839-115">At minimum, your project needs to add package references to:</span></span>

    * `Microsoft.AspNetCore.Razor.Design` 
    * `Microsoft.AspNetCore.Mvc.Razor.Extensions`
    
 <span data-ttu-id="02839-116">I pacchetti precedenti sono inclusi in `Microsoft.AspNetCore.Mvc`.</span><span class="sxs-lookup"><span data-stu-id="02839-116">The preceding packages are included in `Microsoft.AspNetCore.Mvc`.</span></span> <span data-ttu-id="02839-117">Il markup seguente illustra un file *csproj* elementare che utilizza il Razor SDK per compilare i file Razor per un'app Razor Pages di ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="02839-117">The following markup shows a basic *.csproj* file that uses the Razor SDK to build Razor files for an ASP.NET Core Razor Pages app:</span></span>
    
 [!code-xml[Main](sdk/sample/RazorSDK.csproj)]

### <a name="properties"></a><span data-ttu-id="02839-118">Proprietà</span><span class="sxs-lookup"><span data-stu-id="02839-118">Properties</span></span>

<span data-ttu-id="02839-119">Le proprietà seguenti controllano il comportamento del Razor SDK come parte della compilazione del progetto:</span><span class="sxs-lookup"><span data-stu-id="02839-119">The following properties control the Razor's SDK behavior as part of a project build:</span></span>

* <span data-ttu-id="02839-120">`RazorCompileOnBuild`: Quando è `true`, compila e crea l'assembly Razor come parte della compilazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="02839-120">`RazorCompileOnBuild` : When `true`, compiles and emits the Razor assembly as part of building the project.</span></span> <span data-ttu-id="02839-121">Il valore predefinito è `true`.</span><span class="sxs-lookup"><span data-stu-id="02839-121">Defaults to `true`.</span></span>
* <span data-ttu-id="02839-122">`RazorCompileOnPublish`: Quando è `true`, compila e crea l'assembly Razor come parte della pubblicazione del progetto.</span><span class="sxs-lookup"><span data-stu-id="02839-122">`RazorCompileOnPublish` : When `true`, compiles and emits the Razor assembly as part of publishing the project.</span></span> <span data-ttu-id="02839-123">Il valore predefinito è `true`.</span><span class="sxs-lookup"><span data-stu-id="02839-123">Defaults to `true`.</span></span>

<span data-ttu-id="02839-124">Le proprietà e gli elementi seguenti vengono utilizzati per configurare gli input e l'output del Razor SDK:</span><span class="sxs-lookup"><span data-stu-id="02839-124">The following properties and items are used to configure inputs and output to the Razor SDK:</span></span>

| <span data-ttu-id="02839-125">Elementi</span><span class="sxs-lookup"><span data-stu-id="02839-125">Items</span></span>                                         | <span data-ttu-id="02839-126">Descrizione</span><span class="sxs-lookup"><span data-stu-id="02839-126">Description</span></span>                                                                   |
| ------------                                  | -------------                                                                 |
| <span data-ttu-id="02839-127">RazorGenerate</span><span class="sxs-lookup"><span data-stu-id="02839-127">RazorGenerate</span></span>                                 | <span data-ttu-id="02839-128">Elementi della voce (file *cshtml*) che sono input per le destinazioni di generazione del codice.</span><span class="sxs-lookup"><span data-stu-id="02839-128">Item elements (*.cshtml* files) that are inputs to code generation targets.</span></span> |
| <span data-ttu-id="02839-129">RazorCompile</span><span class="sxs-lookup"><span data-stu-id="02839-129">RazorCompile</span></span>                                  | <span data-ttu-id="02839-130">Elementi della voce (file cs) che sono input per le destinazioni di compilazione Razor.</span><span class="sxs-lookup"><span data-stu-id="02839-130">Item elements (.cs files) that are inputs to  Razor compilation targets.</span></span> <span data-ttu-id="02839-131">Usare questo ItemGroup per specificare ulteriori file da compilare nell'assembly Razor.</span><span class="sxs-lookup"><span data-stu-id="02839-131">Use this ItemGroup to specify additional files to be compiled in to the Razor assembly.</span></span> |
| <span data-ttu-id="02839-132">RazorAssemblyAttribute</span><span class="sxs-lookup"><span data-stu-id="02839-132">RazorAssemblyAttribute</span></span>                        | <span data-ttu-id="02839-133">Elementi della voce usati per attributi di generazione del codice per l'assembly Razor.</span><span class="sxs-lookup"><span data-stu-id="02839-133">Item elements used to code generate attributes for the Razor assembly.</span></span> <span data-ttu-id="02839-134">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="02839-134">For example:</span></span>  <br />`<RazorAssemblyAttribute ` <br />  `Include="System.Reflection.AssemblyMetadataAttribute"`<br />`  _Parameter1="BuildSource" _Parameter2="https://docs.asp.net/">` |
| <span data-ttu-id="02839-135">RazorEmbeddedResource</span><span class="sxs-lookup"><span data-stu-id="02839-135">RazorEmbeddedResource</span></span>                         | <span data-ttu-id="02839-136">Elementi della voce aggiunti come risorse incorporate all'assembly Razor generato</span><span class="sxs-lookup"><span data-stu-id="02839-136">Item elements added as embedded resources to the generated Razor assembly</span></span> |

| <span data-ttu-id="02839-137">Proprietà</span><span class="sxs-lookup"><span data-stu-id="02839-137">Property</span></span>                                      | <span data-ttu-id="02839-138">Descrizione</span><span class="sxs-lookup"><span data-stu-id="02839-138">Description</span></span>                                                                   |
| ------------                                  | -------------                                                                 |
| <span data-ttu-id="02839-139">RazorTargetName</span><span class="sxs-lookup"><span data-stu-id="02839-139">RazorTargetName</span></span>                               | <span data-ttu-id="02839-140">Nome di file (senza estensione) dell'assembly generato da Razor.</span><span class="sxs-lookup"><span data-stu-id="02839-140">File name (without extension) of the assembly produced by Razor.</span></span> | 
| <span data-ttu-id="02839-141">RazorOutputPath</span><span class="sxs-lookup"><span data-stu-id="02839-141">RazorOutputPath</span></span>                               | <span data-ttu-id="02839-142">Directory di output di Razor.</span><span class="sxs-lookup"><span data-stu-id="02839-142">The Razor output directory.</span></span>                                      |
| <span data-ttu-id="02839-143">RazorCompileToolset</span><span class="sxs-lookup"><span data-stu-id="02839-143">RazorCompileToolset</span></span>                           | <span data-ttu-id="02839-144">Usato per determinare il set di strumenti utilizzato per compilare l'assembly Razor.</span><span class="sxs-lookup"><span data-stu-id="02839-144">Used to determine the toolset used to build the Razor assembly.</span></span> <span data-ttu-id="02839-145">I valori validi sono `Implicit` e `PrecompilationTool`.</span><span class="sxs-lookup"><span data-stu-id="02839-145">Valid values are `Implicit`, , and `PrecompilationTool`.</span></span> |
| <span data-ttu-id="02839-146">EnableDefaultContentItems</span><span class="sxs-lookup"><span data-stu-id="02839-146">EnableDefaultContentItems</span></span>                     | <span data-ttu-id="02839-147">Quando è `true`, include alcuni tipi di file, ad esempio file *cshtml*, come contenuto nel progetto.</span><span class="sxs-lookup"><span data-stu-id="02839-147">When `true`, includes certain file types, such as *.cshtml* files, as content in the project.</span></span> <span data-ttu-id="02839-148">Quando il riferimento è fatto tramite Microsoft.NET.Sdk.Web, include anche tutti i file in *wwwroot* e i file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="02839-148">When referenced via Microsoft.NET.Sdk.Web, also includes all files under *wwwroot*, and config files.</span></span>         |
| <span data-ttu-id="02839-149">EnableDefaultRazorGenerateItems</span><span class="sxs-lookup"><span data-stu-id="02839-149">EnableDefaultRazorGenerateItems</span></span>               | <span data-ttu-id="02839-150">Quando è `true`, include i file *cshtml* degli elementi di `Content` negli elementi di `RazorGenerate`.</span><span class="sxs-lookup"><span data-stu-id="02839-150">When `true`, includes *.cshtml* files from `Content` items in `RazorGenerate` items.</span></span> |
| <span data-ttu-id="02839-151">GenerateRazorTargetAssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="02839-151">GenerateRazorTargetAssemblyInfo</span></span>               | <span data-ttu-id="02839-152">Quando è `true`, genera un file *cs* contenente attributi specificati da `RazorAssemblyAttribute` e li include nell'output compilato.</span><span class="sxs-lookup"><span data-stu-id="02839-152">When `true`, generates a *.cs* file containing attributes specified by `RazorAssemblyAttribute` and includes it in the compile output.</span></span> |
| <span data-ttu-id="02839-153">EnableDefaultRazorTargetAssemblyInfoAttributes</span><span class="sxs-lookup"><span data-stu-id="02839-153">EnableDefaultRazorTargetAssemblyInfoAttributes</span></span> | <span data-ttu-id="02839-154">Quando è `true`, aggiunge un set predefinito di attributi degli assembly a `RazorAssemblyAttribute`.</span><span class="sxs-lookup"><span data-stu-id="02839-154">When `true`, adds a default set of assembly attributes to `RazorAssemblyAttribute`.</span></span> |
| <span data-ttu-id="02839-155">CopyRazorGenerateFilesToPublishDirectory</span><span class="sxs-lookup"><span data-stu-id="02839-155">CopyRazorGenerateFilesToPublishDirectory</span></span>       | <span data-ttu-id="02839-156">Quando è `true`, copia i file (*cshtml*) degli elementi RazorGenerate nella directory di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="02839-156">When `true`, copies RazorGenerate items (*.cshtml*) files to the publish directory.</span></span> <span data-ttu-id="02839-157">In genere i file Razor non sono necessari per un'applicazione pubblicata se sono stati inclusi nella compilazione in fase di compilazione o di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="02839-157">Typically Razor files are not needed for a published application if they participate in compilation at build-time or publish-time.</span></span> <span data-ttu-id="02839-158">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="02839-158">Defaults to `false`.</span></span> |
| <span data-ttu-id="02839-159">CopyRefAssembliesToPublishDirectory</span><span class="sxs-lookup"><span data-stu-id="02839-159">CopyRefAssembliesToPublishDirectory</span></span>            | <span data-ttu-id="02839-160">Quando è `true`, copiare gli elementi dell'assembly di riferimento nella directory di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="02839-160">When `true`, copy reference assembly items to the publish directory.</span></span> <span data-ttu-id="02839-161">In genere gli assembly di riferimento non sono necessari per un'applicazione pubblicata se la compilazione di Razor avviene in fase di compilazione o di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="02839-161">Typically reference assemblies are not needed for a published application if Razor compilation occurs at build-time or publish-time.</span></span> <span data-ttu-id="02839-162">Impostare su `true` se l'applicazione pubblicata richiede la compilazione runtime, ad esempio, modifica i file cshtml in fase di esecuzione oppure utilizza viste incorporate.</span><span class="sxs-lookup"><span data-stu-id="02839-162">Set to `true`, if your published application requires runtime compilation, for example, modifies cshtml files at runtime, or uses embedded views.</span></span> <span data-ttu-id="02839-163">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="02839-163">Defaults to `false`.</span></span> |
| <span data-ttu-id="02839-164">IncludeRazorContentInPack</span><span class="sxs-lookup"><span data-stu-id="02839-164">IncludeRazorContentInPack</span></span>                      | <span data-ttu-id="02839-165">Quando è `true`, tutti gli elementi del contenuto Razor (file *cshtml*) verranno contrassegnati per l'inclusione nel pacchetto NuGet generato.</span><span class="sxs-lookup"><span data-stu-id="02839-165">When `true`, all Razor content items (*.cshtml* files) will be marked for inclusion in the generated NuGet package.</span></span> <span data-ttu-id="02839-166">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="02839-166">Defaults to `false`.</span></span> |
| <span data-ttu-id="02839-167">EmbedRazorGenerateSources</span><span class="sxs-lookup"><span data-stu-id="02839-167">EmbedRazorGenerateSources</span></span> | <span data-ttu-id="02839-168">Quando è `true`, aggiunge gli elementi (*cshtml*) di RazorGenerate come file incorporati nell'assembly Razor generato.</span><span class="sxs-lookup"><span data-stu-id="02839-168">When `true`, adds RazorGenerate (*.cshtml*) items as embedded files to the generated Razor assembly.</span></span> <span data-ttu-id="02839-169">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="02839-169">Defaults to `false`.</span></span> |
| <span data-ttu-id="02839-170">UseRazorBuildServer</span><span class="sxs-lookup"><span data-stu-id="02839-170">UseRazorBuildServer</span></span>                           | <span data-ttu-id="02839-171">Quando è `true`, usa un processo del server di compilazione permanente per ripartire il lavoro di generazione del codice.</span><span class="sxs-lookup"><span data-stu-id="02839-171">When `true`, uses a persistent build server process to offload code generation work.</span></span> <span data-ttu-id="02839-172">Valore predefinito è il valore di `UseSharedCompilation`.</span><span class="sxs-lookup"><span data-stu-id="02839-172">Defaults to the value of `UseSharedCompilation`.</span></span> |

### <a name="targets"></a><span data-ttu-id="02839-173">Destinazioni</span><span class="sxs-lookup"><span data-stu-id="02839-173">Targets</span></span>
<span data-ttu-id="02839-174">Il Razor SDK definisce due obiettivi principali:</span><span class="sxs-lookup"><span data-stu-id="02839-174">The Razor SDK defines two primary targets:</span></span>

* <span data-ttu-id="02839-175">`RazorGenerate`: il codice genera i file *cs* dagli elementi della voce RazorGenerate.</span><span class="sxs-lookup"><span data-stu-id="02839-175">`RazorGenerate` - Code generates *.cs* files from RazorGenerate item elements.</span></span> <span data-ttu-id="02839-176">Usa la proprietà `RazorGenerateDependsOn` per specificare le altre destinazioni che possono essere eseguite prima o dopo questa destinazione.</span><span class="sxs-lookup"><span data-stu-id="02839-176">Use `RazorGenerateDependsOn` property to specify additional targets that can run before or after this target.</span></span>
* <span data-ttu-id="02839-177">`RazorCompile`: compila i file *cs* generati in un assembly Razor.</span><span class="sxs-lookup"><span data-stu-id="02839-177">`RazorCompile` - Compiles generated *.cs* files in to a Razor assembly.</span></span> <span data-ttu-id="02839-178">Usare `RazorCompileDependsOn` per specificare le altre destinazioni che possono eseguite prima o dopo questa destinazione.</span><span class="sxs-lookup"><span data-stu-id="02839-178">Use `RazorCompileDependsOn` to specify additional targets that can run before or after this target.</span></span>