---
title: Configurare l'autenticazione di Windows in ASP.NET Core
author: ardalis
description: In questo articolo viene descritto come configurare l'autenticazione di Windows in ASP.NET Core, utilizzando IIS Express, IIS, HTTP.sys e WebListener.
keywords: ASP.NET Core, l'autenticazione di Windows, l'attributo Authorize, attributo AllowAnonymous
ms.author: riande
manager: wpickett
ms.date: 10/24/2017
ms.topic: article
ms.assetid: cf119f21-1a2b-49a2-b052-548ccb66ee83
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/windowsauth
ms.openlocfilehash: 703f924d049a267cb8bee22e63e6669b13099c53
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/10/2017
---
# <a name="configure-windows-authentication-in-an-aspnet-core-app"></a><span data-ttu-id="0ffd4-104">Configurare l'autenticazione di Windows in un'applicazione ASP.NET di base</span><span class="sxs-lookup"><span data-stu-id="0ffd4-104">Configure Windows authentication in an ASP.NET Core app</span></span>

<span data-ttu-id="0ffd4-105">Da [Steve Smith](https://ardalis.com) e [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="0ffd4-105">By [Steve Smith](https://ardalis.com) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="0ffd4-106">L'autenticazione di Windows può essere configurata per le applicazioni ASP.NET Core ospitate in IIS, [HTTP.sys](xref:fundamentals/servers/httpsys), o [WebListener](xref:fundamentals/servers/weblistener).</span><span class="sxs-lookup"><span data-stu-id="0ffd4-106">Windows authentication can be configured for ASP.NET Core apps hosted with IIS, [HTTP.sys](xref:fundamentals/servers/httpsys), or [WebListener](xref:fundamentals/servers/weblistener).</span></span>

## <a name="what-is-windows-authentication"></a><span data-ttu-id="0ffd4-107">Che cos'è l'autenticazione di Windows?</span><span class="sxs-lookup"><span data-stu-id="0ffd4-107">What is Windows authentication?</span></span>

<span data-ttu-id="0ffd4-108">L'autenticazione di Windows si basa sul sistema operativo per autenticare gli utenti delle applicazioni ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-108">Windows authentication relies on the operating system to authenticate users of ASP.NET Core apps.</span></span> <span data-ttu-id="0ffd4-109">Quando il server viene eseguito in una rete aziendale usando le identità di dominio Active Directory o altri account di Windows per identificare gli utenti, è possibile utilizzare l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-109">You can use Windows authentication when your server runs on a corporate network using Active Directory domain identities or other Windows accounts to identify users.</span></span> <span data-ttu-id="0ffd4-110">L'autenticazione di Windows è più adatta agli ambienti intranet in cui gli utenti, le applicazioni client e server web appartengono allo stesso dominio di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-110">Windows authentication is best suited to intranet environments in which users, client applications, and web servers belong to the same Windows domain.</span></span>

<span data-ttu-id="0ffd4-111">[Ulteriori informazioni sull'autenticazione di Windows e l'installazione di IIS](https://docs.microsoft.com/iis/configuration/system.webServer/security/authentication/windowsAuthentication/).</span><span class="sxs-lookup"><span data-stu-id="0ffd4-111">[Learn more about Windows authentication and installing it for IIS](https://docs.microsoft.com/iis/configuration/system.webServer/security/authentication/windowsAuthentication/).</span></span>

## <a name="enable-windows-authentication-in-an-aspnet-core-app"></a><span data-ttu-id="0ffd4-112">Abilitare l'autenticazione di Windows in un'applicazione ASP.NET di base</span><span class="sxs-lookup"><span data-stu-id="0ffd4-112">Enable Windows authentication in an ASP.NET Core app</span></span>

<span data-ttu-id="0ffd4-113">Il modello di applicazione Web di Visual Studio può essere configurato per supportare l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-113">The Visual Studio Web Application template can be configured to support Windows authentication.</span></span>

### <a name="use-the-windows-authentication-app-template"></a><span data-ttu-id="0ffd4-114">Utilizzare il modello di app di autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="0ffd4-114">Use the Windows authentication app template</span></span>

<span data-ttu-id="0ffd4-115">In Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="0ffd4-115">In Visual Studio:</span></span>
1. <span data-ttu-id="0ffd4-116">Creare una nuova applicazione Web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-116">Create a new ASP.NET Core Web Application.</span></span> 
1. <span data-ttu-id="0ffd4-117">Selezionare l'applicazione Web dall'elenco dei modelli.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-117">Select Web Application from the list of templates.</span></span>
1. <span data-ttu-id="0ffd4-118">Selezionare il **Modifica autenticazione** e selezionare **l'autenticazione di Windows**.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-118">Select the **Change Authentication** button and select **Windows Authentication**.</span></span> 

<span data-ttu-id="0ffd4-119">Eseguire l'app.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-119">Run the app.</span></span> <span data-ttu-id="0ffd4-120">Il nome utente viene visualizzato nella parte superiore destra dell'app.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-120">The username appears in the top right of the app.</span></span>

![Schermata di Browser l'autenticazione di Windows](windowsauth/_static/browser-screenshot.png)

<span data-ttu-id="0ffd4-122">Per progetti di sviluppo utilizzando IIS Express, il modello fornisce tutte la configurazione necessaria per utilizzare l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-122">For development work using IIS Express, the template provides all the configuration necessary to use Windows authentication.</span></span> <span data-ttu-id="0ffd4-123">Nella sezione seguente viene illustrato come configurare manualmente un'applicazione ASP.NET Core per l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-123">The following section shows how to manually configure an ASP.NET Core app for Windows authentication.</span></span>

### <a name="visual-studio-settings-for-windows-and-anonymous-authentication"></a><span data-ttu-id="0ffd4-124">Impostazioni di Visual Studio per Windows e l'autenticazione anonima</span><span class="sxs-lookup"><span data-stu-id="0ffd4-124">Visual Studio settings for Windows and anonymous authentication</span></span>

<span data-ttu-id="0ffd4-125">Il progetto di Visual Studio **proprietà** della pagina **Debug** scheda fornisce caselle di controllo per l'autenticazione di Windows e l'autenticazione anonima.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-125">The Visual Studio project **Properties** page's **Debug** tab provides check boxes for Windows authentication and anonymous authentication.</span></span>

![Schermata di Browser l'autenticazione di Windows](windowsauth/_static/vs-auth-property-menu.png)

<span data-ttu-id="0ffd4-127">In alternativa, queste due proprietà possono essere configurate nel *launchSettings.json* file:</span><span class="sxs-lookup"><span data-stu-id="0ffd4-127">Alternatively, these two properties can be configured in the *launchSettings.json* file:</span></span>

[!code-json[](windowsauth/sample/launchSettings.json?highlight=3-4)]

## <a name="enable-windows-authentication-with-iis"></a><span data-ttu-id="0ffd4-128">Abilitare l'autenticazione di Windows con IIS</span><span class="sxs-lookup"><span data-stu-id="0ffd4-128">Enable Windows authentication with IIS</span></span>

<span data-ttu-id="0ffd4-129">IIS Usa il [ASP.NET Core modulo](xref:fundamentals/servers/aspnet-core-module) (ANCM) per ospitare applicazioni ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-129">IIS uses the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) (ANCM) to host ASP.NET Core apps.</span></span> <span data-ttu-id="0ffd4-130">Il ANCM flussi l'autenticazione di Windows in IIS per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-130">The ANCM flows Windows authentication to IIS by default.</span></span> <span data-ttu-id="0ffd4-131">Configurazione dell'autenticazione di Windows viene eseguita in IIS, non il progetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-131">Configuration of Windows authentication is done within IIS, not the application project.</span></span> <span data-ttu-id="0ffd4-132">Nelle sezioni seguenti viene illustrato come utilizzare Gestione IIS per configurare un'app di ASP.NET Core per utilizzare l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-132">The following sections show how to use IIS Manager to configure an ASP.NET Core app to use Windows authentication.</span></span>

### <a name="create-a-new-iis-site"></a><span data-ttu-id="0ffd4-133">Creare un nuovo sito IIS</span><span class="sxs-lookup"><span data-stu-id="0ffd4-133">Create a new IIS site</span></span>

<span data-ttu-id="0ffd4-134">Specificare un nome e una cartella e consentono di creare un nuovo pool di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-134">Specify a name and folder and allow it to create a new application pool.</span></span>

### <a name="customize-authentication"></a><span data-ttu-id="0ffd4-135">Personalizzare l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="0ffd4-135">Customize authentication</span></span>

<span data-ttu-id="0ffd4-136">Aprire il menu di autenticazione per il sito.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-136">Open the Authentication menu for the site.</span></span>

![Menu di autenticazione IIS](windowsauth/_static/iis-authentication-menu.png)

<span data-ttu-id="0ffd4-138">Disabilitare l'autenticazione anonima e abilitare l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-138">Disable Anonymous Authentication and enable Windows Authentication.</span></span>

![Impostazioni di autenticazione IIS](windowsauth/_static/iis-auth-settings.png)

### <a name="publish-your-project-to-the-iis-site-folder"></a><span data-ttu-id="0ffd4-140">Pubblicare il progetto alla cartella del sito IIS</span><span class="sxs-lookup"><span data-stu-id="0ffd4-140">Publish your project to the IIS site folder</span></span>

<span data-ttu-id="0ffd4-141">Con Visual Studio o .NET Core CLI, pubblicare l'app nella cartella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-141">Using Visual Studio or the .NET Core CLI, publish the app to the destination folder.</span></span>

![Finestra di dialogo di pubblicazione di Visual Studio](windowsauth/_static/vs-publish-app.png)

<span data-ttu-id="0ffd4-143">Altre informazioni, vedere [la pubblicazione in IIS](xref:publishing/iis).</span><span class="sxs-lookup"><span data-stu-id="0ffd4-143">Learn more about [publishing to IIS](xref:publishing/iis).</span></span>

<span data-ttu-id="0ffd4-144">Avviare l'app per verificare l'autenticazione di Windows sia funzionante.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-144">Launch the app to verify Windows authentication is working.</span></span>

## <a name="enable-windows-authentication-with-httpsys-or-weblistener"></a><span data-ttu-id="0ffd4-145">Abilitare l'autenticazione di Windows con HTTP.sys o WebListener</span><span class="sxs-lookup"><span data-stu-id="0ffd4-145">Enable Windows authentication with HTTP.sys or WebListener</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="0ffd4-146">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="0ffd4-146">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="0ffd4-147">Sebbene Kestrel non supporta l'autenticazione di Windows, è possibile utilizzare [HTTP.sys](xref:fundamentals/servers/httpsys) per supportare gli scenari indipendenti che in Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-147">Although Kestrel doesn't support Windows authentication, you can use [HTTP.sys](xref:fundamentals/servers/httpsys) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="0ffd4-148">Nell'esempio seguente consente di configurare dell'host dell'applicazione web per l'utilizzo di HTTP.sys con l'autenticazione di Windows:</span><span class="sxs-lookup"><span data-stu-id="0ffd4-148">The following example configures the app's web host to use HTTP.sys with Windows authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program2x.cs?highlight=9-14)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="0ffd4-149">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="0ffd4-149">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="0ffd4-150">Sebbene Kestrel non supporta l'autenticazione di Windows, è possibile utilizzare [WebListener](xref:fundamentals/servers/weblistener) per supportare gli scenari indipendenti che in Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-150">Although Kestrel doesn't support Windows authentication, you can use [WebListener](xref:fundamentals/servers/weblistener) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="0ffd4-151">Nell'esempio seguente consente di configurare dell'host dell'applicazione web per utilizzare WebListener con l'autenticazione di Windows:</span><span class="sxs-lookup"><span data-stu-id="0ffd4-151">The following example configures the app's web host to use WebListener with Windows authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program1x.cs?highlight=6-11)]

---

## <a name="work-with-windows-authentication"></a><span data-ttu-id="0ffd4-152">Usare l'autenticazione di Windows</span><span class="sxs-lookup"><span data-stu-id="0ffd4-152">Work with Windows authentication</span></span>

<span data-ttu-id="0ffd4-153">Lo stato di configurazione dell'accesso anonimo determina il modo in cui il `[Authorize]` e `[AllowAnonymous]` attributi vengono usati nell'app.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-153">The configuration state of anonymous access determines the way in which the `[Authorize]` and `[AllowAnonymous]` attributes are used in the app.</span></span> <span data-ttu-id="0ffd4-154">Nelle due sezioni seguenti illustrano come gestire gli stati di configurazione non consentite e sono consentite dell'accesso anonimo.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-154">The following two sections explain how to handle the disallowed and allowed configuration states of anonymous access.</span></span>

### <a name="disallow-anonymous-access"></a><span data-ttu-id="0ffd4-155">Negare l'accesso anonimo</span><span class="sxs-lookup"><span data-stu-id="0ffd4-155">Disallow anonymous access</span></span>

<span data-ttu-id="0ffd4-156">Quando è abilitata l'autenticazione di Windows e accesso anonimo è disabilitato, il `[Authorize]` e `[AllowAnonymous]` gli attributi non hanno alcun effetto.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-156">When Windows authentication is enabled and anonymous access is disabled, the `[Authorize]` and `[AllowAnonymous]` attributes have no effect.</span></span> <span data-ttu-id="0ffd4-157">Se il sito IIS (o server HTTP. sys o WebListener) è configurato per negare l'accesso anonimo, la richiesta raggiunga mai l'app.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-157">If the IIS site (or HTTP.sys or WebListener server) is configured to disallow anonymous access, the request never reaches your app.</span></span> <span data-ttu-id="0ffd4-158">Per questo motivo, il `[AllowAnonymous]` attributo non è applicabile.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-158">For this reason, the `[AllowAnonymous]` attribute isn't applicable.</span></span>

### <a name="allow-anonymous-access"></a><span data-ttu-id="0ffd4-159">Consenti accesso anonimo</span><span class="sxs-lookup"><span data-stu-id="0ffd4-159">Allow anonymous access</span></span>

<span data-ttu-id="0ffd4-160">Quando sono abilitati sia l'autenticazione di Windows e l'accesso anonimo, usare il `[Authorize]` e `[AllowAnonymous]` gli attributi.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-160">When both Windows authentication and anonymous access are enabled, use the `[Authorize]` and `[AllowAnonymous]` attributes.</span></span> <span data-ttu-id="0ffd4-161">Il `[Authorize]` attributo consente di proteggere parti dell'app che richiedono effettivamente l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-161">The `[Authorize]` attribute allows you to secure pieces of the app which truly do require Windows authentication.</span></span> <span data-ttu-id="0ffd4-162">Il `[AllowAnonymous]` esegue l'override dell'attributo `[Authorize]` attributo utilizzo all'interno di applicazioni che consentono l'accesso anonimo.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-162">The `[AllowAnonymous]` attribute overrides `[Authorize]` attribute usage within apps which allow anonymous access.</span></span> <span data-ttu-id="0ffd4-163">Vedere [autorizzazione semplice](xref:security/authorization/simple) per informazioni dettagliate sull'utilizzo di attributi.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-163">See [Simple Authorization](xref:security/authorization/simple) for attribute usage details.</span></span>

<span data-ttu-id="0ffd4-164">In ASP.NET Core 2. x, il `[Authorize]` attributo richiede una configurazione aggiuntiva in *Startup.cs* di incentivare le richieste anonime per l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-164">In ASP.NET Core 2.x, the `[Authorize]` attribute requires additional configuration in *Startup.cs* to challenge anonymous requests for Windows authentication.</span></span> <span data-ttu-id="0ffd4-165">La configurazione consigliata varia leggermente in base al server web in uso.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-165">The recommended configuration varies slightly based on the web server being used.</span></span>

#### <a name="iis"></a><span data-ttu-id="0ffd4-166">IIS</span><span class="sxs-lookup"><span data-stu-id="0ffd4-166">IIS</span></span>

<span data-ttu-id="0ffd4-167">Se si utilizza IIS, aggiungere il comando seguente per il `ConfigureServices` metodo:</span><span class="sxs-lookup"><span data-stu-id="0ffd4-167">If using IIS, add the following to the `ConfigureServices` method:</span></span> 

```csharp
// IISDefaults requires the following import:
// using Microsoft.AspNetCore.Server.IISIntegration;
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

#### <a name="httpsys"></a><span data-ttu-id="0ffd4-168">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="0ffd4-168">HTTP.sys</span></span>

<span data-ttu-id="0ffd4-169">Se si utilizza HTTP.sys, aggiungere il comando seguente per il `ConfigureServices` metodo:</span><span class="sxs-lookup"><span data-stu-id="0ffd4-169">If using HTTP.sys, add the following to the `ConfigureServices` method:</span></span>

```csharp
// HttpSysDefaults requires the following import:
// using Microsoft.AspNetCore.Server.HttpSys;
services.AddAuthentication(HttpSysDefaults.AuthenticationScheme);
```

### <a name="impersonation"></a><span data-ttu-id="0ffd4-170">Rappresentazione</span><span class="sxs-lookup"><span data-stu-id="0ffd4-170">Impersonation</span></span>

<span data-ttu-id="0ffd4-171">ASP.NET Core non implementa la rappresentazione.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-171">ASP.NET Core doesn't implement impersonation.</span></span> <span data-ttu-id="0ffd4-172">Le app vengono eseguite con l'identità di applicazione per tutte le richieste, utilizzando l'identità di processo o i pool di app.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-172">Apps run with the application identity for all requests, using app pool or process identity.</span></span> <span data-ttu-id="0ffd4-173">Se si desidera eseguire in modo esplicito un'azione per conto dell'utente, utilizzare `WindowsIdentity.RunImpersonated`.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-173">If you need to explicitly perform an action on behalf of a user, use `WindowsIdentity.RunImpersonated`.</span></span> <span data-ttu-id="0ffd4-174">Eseguire un'unica azione in questo contesto e quindi chiudere il contesto.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-174">Run a single action in this context and then close the context.</span></span>

[!code-csharp[](windowsauth/sample/Startup.cs?name=snippet_Impersonate&highlight=10-18)]

<span data-ttu-id="0ffd4-175">Si noti che `RunImpersonated` non supporta le operazioni asincrone e non devono essere usate per scenari complessi.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-175">Note that `RunImpersonated` doesn't support asynchronous operations and shouldn't be used for complex scenarios.</span></span> <span data-ttu-id="0ffd4-176">Ad esempio, il wrapping di richieste intere o middleware catene, non è supportato o consigliato.</span><span class="sxs-lookup"><span data-stu-id="0ffd4-176">For example, wrapping entire requests or middleware chains isn't supported or recommended.</span></span>

---