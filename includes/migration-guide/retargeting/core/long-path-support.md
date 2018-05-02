### <a name="long-path-support"></a><span data-ttu-id="2abed-101">Unterstützung für lange Pfade</span><span class="sxs-lookup"><span data-stu-id="2abed-101">Long path support</span></span>

|   |   |
|---|---|
|<span data-ttu-id="2abed-102">Details</span><span class="sxs-lookup"><span data-stu-id="2abed-102">Details</span></span>|<span data-ttu-id="2abed-103">Für Apps mit der Zielplattform .NET Framework 4.6.2 und höher werden lange Pfade (bis zu 32.000 Zeichen) unterstützt, und die Beschränkung auf 260 Zeichen (oder <code>MAX_PATH</code>) für die Pfadlänge wurde aufgehoben. Bei Apps, die neu kompiliert werden, um .NET Framework 4.6.2 als Zielplattform zu verwenden, lösen Codepfade, die zuvor aufgrund der Überschreitung der Pfadlänge von 260 Zeichen <xref:System.IO.PathTooLongException?displayProperty=name> ausgelöst haben, nun unter den folgenden Bedingungen <xref:System.IO.PathTooLongException?displayProperty=name> aus:</span><span class="sxs-lookup"><span data-stu-id="2abed-103">Starting with apps that target the .NET Framework 4.6.2, long paths (of up to 32K characters) are supported, and the 260-character (or <code>MAX_PATH</code>) limitation on path lengths has been removed.For apps that are recompiled to target the .NET Framework 4.6.2, code paths that previously threw a <xref:System.IO.PathTooLongException?displayProperty=name> because a path exceeded 260 characters will now throw a <xref:System.IO.PathTooLongException?displayProperty=name> only under the following conditions:</span></span><ul><li><span data-ttu-id="2abed-104">Die Zahl der Pfadzeichen überschreitet <xref:System.Int16.MaxValue> (32.767).</span><span class="sxs-lookup"><span data-stu-id="2abed-104">The length of the path is greater than <xref:System.Int16.MaxValue> (32,767) characters.</span></span></li><li><span data-ttu-id="2abed-105">Das Betriebssystem gibt <code>COR_E_PATHTOOLONG</code> oder einen dazu äquivalenten Wert zurück.</span><span class="sxs-lookup"><span data-stu-id="2abed-105">The operating system returns <code>COR_E_PATHTOOLONG</code> or its equivalent.</span></span></li></ul><span data-ttu-id="2abed-106">Bei Apps mit der Zielplattform .NET Framework 4.6.1 und früheren Versionen löst die Laufzeit automatisch eine <xref:System.IO.PathTooLongException?displayProperty=name> aus, wenn ein Pfad die Länge von 260 Zeichen überschreitet.</span><span class="sxs-lookup"><span data-stu-id="2abed-106">For apps that target the .NET Framework 4.6.1 and earlier versions, the runtime automatically throws a <xref:System.IO.PathTooLongException?displayProperty=name> whenever a path exceeds 260 characters.</span></span>|
|<span data-ttu-id="2abed-107">Vorschlag</span><span class="sxs-lookup"><span data-stu-id="2abed-107">Suggestion</span></span>|<span data-ttu-id="2abed-108">Für Apps mit der Zielplattform .NET Framework 4.6.2 können Sie sich gegen die Unterstützung von langen Pfaden entscheiden, wenn sie nicht erwünscht ist, indem Sie Folgendes dem Abschnitt <code>&lt;runtime&gt;</code> Ihrer <code>app.config</code>-Datei hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="2abed-108">For apps that target the .NET Framework 4.6.2, you can opt out of long path support if it is not desirable by adding the following to the <code>&lt;runtime&gt;</code> section of your <code>app.config</code> file:</span></span><pre><code class="language-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.BlockLongPaths=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre><span data-ttu-id="2abed-109">Sie können bei Anwendungen, die für frühere Versionen von .NET Framework vorgesehen sind, aber in .NET Framework 4.6.2 oder höher ausgeführt werden, lange Pfade unterstützen, indem Sie dem Abschnitt <code>&lt;runtime&gt;</code> der <code>app.config</code>-Datei Folgendes hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="2abed-109">For apps that target earlier versions of the .NET Framework but run on the .NET Framework 4.6.2 or later, you can opt in to long path support by adding the following to the <code>&lt;runtime&gt;</code> section of your <code>app.config</code> file:</span></span><pre><code class="language-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.IO.BlockLongPaths=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|<span data-ttu-id="2abed-110">Bereich</span><span class="sxs-lookup"><span data-stu-id="2abed-110">Scope</span></span>|<span data-ttu-id="2abed-111">Gering</span><span class="sxs-lookup"><span data-stu-id="2abed-111">Minor</span></span>|
|<span data-ttu-id="2abed-112">Version</span><span class="sxs-lookup"><span data-stu-id="2abed-112">Version</span></span>|<span data-ttu-id="2abed-113">4.6.2</span><span class="sxs-lookup"><span data-stu-id="2abed-113">4.6.2</span></span>|
|<span data-ttu-id="2abed-114">Typ</span><span class="sxs-lookup"><span data-stu-id="2abed-114">Type</span></span>|<span data-ttu-id="2abed-115">Neuzuweisung</span><span class="sxs-lookup"><span data-stu-id="2abed-115">Retargeting</span></span>|
