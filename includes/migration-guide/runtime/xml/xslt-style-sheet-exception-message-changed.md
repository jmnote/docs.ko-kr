### <a name="xslt-style-sheet-exception-message-changed"></a><span data-ttu-id="f711e-101">XSLT 스타일 시트 예외 메시지가 변경됨</span><span class="sxs-lookup"><span data-stu-id="f711e-101">XSLT style sheet exception message changed</span></span>

|   |   |
|---|---|
|<span data-ttu-id="f711e-102">설명</span><span class="sxs-lookup"><span data-stu-id="f711e-102">Details</span></span>|<span data-ttu-id="f711e-103">.NET Framework 4.5에서 XSLT 파일이 너무 복잡할 경우 오류 메시지의 텍스트는 &quot;스타일시트가 너무 복잡합니다.&quot; 이전 버전에서 오류 메시지는 &quot;XSLT 컴파일 오류입니다.&quot;였습니다. 오류 메시지 텍스트에 종속되어 있는 응용 프로그램 코드는 더 이상 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f711e-103">In the .NET Framework 4.5, the text of the error message when an XSLT file is too complex is &quot;The style sheet is too complex.&quot; In previous versions, the error message was &quot;XSLT compile error.&quot; Application code that depends on the text of the error message will no longer work.</span></span> <span data-ttu-id="f711e-104">그러나 예외 형식은 동일하게 유지되므로 이 변경은 실제 영향을 미쳐서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f711e-104">However, the exception types remain the same, so this change should have no real impact.</span></span>|
|<span data-ttu-id="f711e-105">제안 해결 방법</span><span class="sxs-lookup"><span data-stu-id="f711e-105">Suggestion</span></span>|<span data-ttu-id="f711e-106">이 오류 조건에서 새 메시지를 예상하여 예외 메시지에 따라 응용 프로그램 코드를 업데이트하거나 더욱 좋은 방법은 변경되지 않는 예외 형식(<xref:System.Xml.Xsl.XsltException?displayProperty=name>)에만 종속되도록 코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f711e-106">Update any app code depending on the exception message from this error condition to expect the new message, or (even better) update the code to depend only on the exception type (<xref:System.Xml.Xsl.XsltException?displayProperty=name>), which has not changed.</span></span>|
|<span data-ttu-id="f711e-107">범위</span><span class="sxs-lookup"><span data-stu-id="f711e-107">Scope</span></span>|<span data-ttu-id="f711e-108">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="f711e-108">Edge</span></span>|
|<span data-ttu-id="f711e-109">버전</span><span class="sxs-lookup"><span data-stu-id="f711e-109">Version</span></span>|<span data-ttu-id="f711e-110">4.5</span><span class="sxs-lookup"><span data-stu-id="f711e-110">4.5</span></span>|
|<span data-ttu-id="f711e-111">형식</span><span class="sxs-lookup"><span data-stu-id="f711e-111">Type</span></span>|<span data-ttu-id="f711e-112">런타임</span><span class="sxs-lookup"><span data-stu-id="f711e-112">Runtime</span></span>|
|<span data-ttu-id="f711e-113">영향을 받는 API</span><span class="sxs-lookup"><span data-stu-id="f711e-113">Affected APIs</span></span>|<ul><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Type)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XmlReader)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XPath.IXPathNavigable)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Reflection.MethodInfo,System.Byte[],System.Type[])?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.String,System.Xml.Xsl.XsltSettings,System.Xml.XmlResolver)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XmlReader,System.Xml.Xsl.XsltSettings,System.Xml.XmlResolver)?displayProperty=nameWithType></li><li><xref:System.Xml.Xsl.XslCompiledTransform.Load(System.Xml.XPath.IXPathNavigable,System.Xml.Xsl.XsltSettings,System.Xml.XmlResolver)?displayProperty=nameWithType></li></ul>|
