***

### Part 3 (Lines 561 to end)

```markdown
<!-- Context: Part 3 of 3 for LLM ingestion - PowerShell Writing Style Guide -->
<!-- markdownlint-disable MD013 -->

# PowerShell Writing Style (Part 3)

**Example of complete help block** (from a generic parsing function):

```powershell
# .SYNOPSIS
# Processes a string input with flexible handling of non-standard formats.
#
# .DESCRIPTION
# Attempts direct processing. On failure, iteratively handles problematic segments...
#
# .PARAMETER ReferenceToResultObject
# Reference to store the resulting object.
#
# .EXAMPLE
# $result = $null; $extras = @('','','','',''); $status = Process-String ([ref]$result) ([ref]$extras) 'input-string'
#
# # $status = 4, $result = processed value, $extras[3] = 'leftover'
#
# .INPUTS
# None. You can't pipe objects to this function.
#
# .OUTPUTS
# [int] Status code: 0=success, 1-5=partial success with extras, -1=failure
#
# .NOTES
# This function/script supports positional parameters:
#
#   Position 0: ReferenceToResultObject
#   Position 1: ReferenceArrayOfExtraStrings
#   Position 2: InputString
#
# Version: 1.0.20250218.0
Note: The terse form is acceptable where brevity is preferred, forexample: # Supports positional parameters. followed by# Version: 1.0.20250218.0. The multi-line format shown above isRECOMMENDED because it explicitly identifies which parameters arepositional and at which positions. SeePositional Parameter Support for fullguidance.Comment-Based Help SpacingA comment blank line is a line inside comment-based help that contains onlythe comment marker (#), with the same indentation as the surrounding helpblock. For function-level help, the comment blank line is indented with the helpblock:PowerShellfunction Get-Example {
    # .SYNOPSIS
    # Does something.
    #
    # .DESCRIPTION
    # Does something in more detail.
    param ()
}
Comment-based help MUST use exactly one comment blank line betweentop-level help sections. Top-level help sections include .SYNOPSIS,.DESCRIPTION, .PARAMETER, .EXAMPLE, .INPUTS, .OUTPUTS, and .NOTES.A comment blank line MUST NOT appear before the first help keyword.Consecutive .PARAMETER sections MUST be separated by exactly one commentblank line. Consecutive .EXAMPLE sections MUST be separated by exactly onecomment blank line.A comment blank line SHOULD NOT appear immediately after a dotted helpkeyword when the section content begins on the next line. Wrapped linesbelonging to the same paragraph MUST NOT be separated by comment blanklines.Inside .EXAMPLE sections, executable sample code SHOULD be separated fromexplanatory rendered-comment lines by exactly one comment blank line. Theexisting requirement that explanatory or output-description lines use exactly# # <text> remains unchanged:PowerShell# .EXAMPLE
# $arrResult = @(Get-Example)
#
# # Returns zero or more example objects.
Within .NOTES, distinct note groups SHOULD be separated by exactly onecomment blank line, especially positional parameter documentation, additionalnote text, private/internal helper banners, and version metadata:PowerShell# .NOTES
# This script supports positional parameters:
#
#   Position 0: RootDirectoryPath
#
# Parameters without a listed position must be named.
#
# Version: 1.0.20260517.0
Inline Comments Within .EXAMPLE BlocksWhen writing explanatory or output-description lines within a .EXAMPLE section of comment-based help, use double # — that is, # # <text>. The first # is the standard comment-based help line prefix (required for all help content). The second # creates a PowerShell comment within the rendered example output so that:Get-Help -Examples renders the line as # <text>, which is valid PowerShell syntax and can be safely copy-pasted.The explanatory text is visually distinct from executable code lines in the example.Compliant — explanatory lines use # #:PowerShell# .EXAMPLE
# $arrRows = @(ConvertTo-VectorRow -Counts $arrCounts -FeatureIndexObject $objIndex)
#
# # $arrRows[0].PrincipalKey = 'user-abc'
# # $arrRows[0].Vector = [double[]] (fixed-length array)
Rendered by Get-Help:Plaintext$arrRows = @(ConvertTo-VectorRow -Counts $arrCounts -FeatureIndexObject $objIndex)
# $arrRows[0].PrincipalKey = 'user-abc'
# $arrRows[0].Vector = [double[]] (fixed-length array)
Non-compliant — single # for explanation text:PowerShell# .EXAMPLE
# $arrRows = @(ConvertTo-VectorRow -Counts $arrCounts -FeatureIndexObject $objIndex)
#
# Returns vector row objects with PrincipalKey, Vector, and TotalActions.
Rendered by Get-Help:Plaintext$arrRows = @(ConvertTo-VectorRow -Counts $arrCounts -FeatureIndexObject $objIndex)
Returns vector row objects with PrincipalKey, Vector, and TotalActions.
The non-compliant form renders bare prose that (a) is not valid PowerShell, (b) can be confused with actual command output, and (c) is not safely copy-pasteable.Non-compliant — triple # for explanation text:PowerShell# .EXAMPLE
# $arrRows = @(ConvertTo-VectorRow -Counts $arrCounts -FeatureIndexObject $objIndex)
#
# # # Returns vector row objects with PrincipalKey and Vector.
Rendered by Get-Help:Plaintext$arrRows = @(ConvertTo-VectorRow -Counts $arrCounts -FeatureIndexObject $objIndex)
## Returns vector row objects with PrincipalKey and Vector.
Lines within .EXAMPLE blocks that are intended to render as PowerShell comments in Get-Help output MUST use exactly two # characters (# # <text>). Using three or more # characters (for example, # # # <text>) is non-compliant because it does not preserve the intended rendered form of # <text> in Get-Help output.Help Content Quality: High StandardsBehavioral Contracts: Every possible output/return value documented with exact type and meaning (in .OUTPUTS) and example (in .EXAMPLE blocks); when integer status codes are used, include full mapping of codes to meanings.Edge Case Coverage: Examples include valid input, invalid segments, overflow conditions, excess parts.Positional Parameter Support: .NOTES explicitly documents positional ordering.Versioning: Includes internal version in .NOTES for change tracking.Private/Internal Helper Function Documentation[All] If a function exists only to serve a specific script, module, or tool and is not part of that script, module, or tool's public API surface, its .NOTES section MUST begin with a clear private-helper banner. That banner MUST state that the function is not part of the public API surface, and MUST warn that parameters, return shape, and positional contract may change without notice.[Modern] In module-based code, a function intentionally omitted from the module manifest's FunctionsToExport is treated as a private/internal helper for purposes of the documentation requirements above unless the distributable/vendored-helper exemption applies.A distributable/vendored helper is a reusable helper function that carries its own per-function #region License block and has clear cross-project reuse intent rather than existing as script/module/tool-specific glue. A per-function license region is a strong distributability signal for this exemption, but it is not standalone proof: if reuse intent is unclear, document the function's distributable intent or treat the function as a script/module/tool-specific internal helper. A Version: line by itself is not sufficient for the exemption, because ordinary internal helpers also carry version metadata.Distributable/vendored helpers are exempt from the PRIVATE/INTERNAL HELPER banner, even when placed under Private/ and omitted from FunctionsToExport. When they document positional parameters, they document a stable distributable contract rather than using the private-helper "internal-caller contract only; subject to change" header. Export visibility and API stability are separate concerns; an unexported helper can still have a stable distributable contract.All other comment-based help requirements (.SYNOPSIS, .DESCRIPTION, .PARAMETER, .EXAMPLE, .INPUTS, .OUTPUTS, .NOTES) still apply to private/internal helpers — the banner is an addition, not a replacement.Compliant — private/internal helper with required .NOTES banner:PowerShellfunction Convert-RawRecord {
    # .SYNOPSIS
    # Transforms a raw input record into a normalized internal format.
    #
    # .DESCRIPTION
    # Parses the raw record hashtable, validates required keys, and
    # returns a normalized [pscustomobject]. This function is used
    # only by Import-DataSet and is not part of the public API.
    #
    # .PARAMETER ReferenceToResultObject
    # Reference to store the resulting normalized object.
    #
    # .PARAMETER RawRecord
    # The raw hashtable to normalize.
    #
    # .EXAMPLE
    # $objResult = $null
    # $intReturnCode = Convert-RawRecord ([ref]$objResult) $hashtableInput
    #
    # # $intReturnCode = 0, $objResult contains the normalized record
    #
    # .INPUTS
    # None. You can't pipe objects to this function.
    #
    # .OUTPUTS
    # [int] Status code: 0 = success, -1 = failure (missing keys)
    #
    # .NOTES
    # PRIVATE/INTERNAL HELPER — This function is not part of the
    # public API surface. Parameters, return shape, and positional
    # contract may change without notice.
    #
    # This function supports positional parameters
    # (internal-caller contract only; subject to change):
    #
    #   Position 0: ReferenceToResultObject
    #   Position 1: RawRecord
    #
    # Version: 1.0.20260415.0
    param (
        [ref]$ReferenceToResultObject,
        [hashtable]$RawRecord
    )

    # Implementation omitted for brevity
}
Compliant - distributable/vendored helper exempt from the private-helper banner:PowerShellfunction Convert-DelimitedRecord {
    # .SYNOPSIS
    # Converts one delimited record into a normalized object.
    #
    # .DESCRIPTION
    # Parses a delimited record using a caller-provided delimiter and returns
    # a normalized [pscustomobject]. This helper is versioned and licensed for
    # reuse across projects, so its parameter order is a stable distributable
    # contract even when a consuming module does not export it.
    #
    # .PARAMETER RecordText
    # The delimited record text to parse.
    #
    # .PARAMETER Delimiter
    # The delimiter that separates fields in the record.
    #
    # .EXAMPLE
    # $objRecord = Convert-DelimitedRecord 'alpha,beta' ','
    #
    # # Returns a normalized record object.
    #
    # .INPUTS
    # None. You can't pipe objects to this function.
    #
    # .OUTPUTS
    # [pscustomobject] Normalized record object.
    #
    # .NOTES
    # This distributable helper supports positional parameters
    # (stable distributable contract):
    #
    #   Position 0: RecordText
    #   Position 1: Delimiter
    #
    # Version: 1.0.20260629.0
    param (
        [string]$RecordText,
        [string]$Delimiter
    )

    #region License ########################################################
    # MIT License or other per-function license text.
    #endregion License ########################################################

    # Implementation omitted for brevity
}
Inline Comments: Purpose and PlacementInline comments SHOULD focus on "why" rather than "what", be used only when behavior is non-obvious, and be aligned with at least two spaces from code.Structural Documentation: Regions and LicensingThe script uses #region / #endregion blocks to create logical code folding:PowerShell#region License ########################################################
# Full MIT-style license
#endregion License ########################################################

#region FunctionsToSupportErrorHandling ############################
# Get-ReferenceToLastError
# Test-ErrorOccurred
#endregion FunctionsToSupportErrorHandling ############################
For distributable helper functions, the structure MUST be: function declaration, comment-based help, param() block, then #region License block.Example:PowerShellfunction Get-Example {
    # .SYNOPSIS
    # Example function with license
    #
    # .DESCRIPTION
    # This demonstrates the correct placement of param() before license.
    #
    # .NOTES
    # Version: 1.0.20260109.0

    param(
        [string]$Parameter
    )

    #region License ########################################################
    # MIT License or other license text
    #endregion License ########################################################

    # Function implementation
    return 0
}
Function and Script VersioningAll distributable functions and scripts MUST include a version number in the .NOTES section of their comment-based help. This version number provides critical change tracking and MUST follow a strict, [System.Version]-compatible format: Major.Minor.Build.Revision.For this section, the previously published version means the most recent .NOTES version published for the same distributable function or script before this change. In repository work, this is the version already on the branch the change lands on, not an in-progress value produced earlier in the same change. For a brand-new function or script, there is no previously published version.Major: Increment the Major version (e.g., 1.0.20251103.0 to 2.0.20251230.0) any time a breaking change is introduced. Breaking changes include:Removing or renaming a function, parameter, or public interfaceChanging parameter types in incompatible waysAltering return types or output formats that break existing consumersAny modification that requires users to update their codeMinor: Increment the Minor version (e.g., 1.0.20251103.0 to 1.1.20251230.0) any time a feature or function change is introduced that is non-breaking. This includes:Adding new functions or capabilitiesAdding new optional parametersEnhancing existing functionality without changing interfacesPerformance improvements that don't affect behaviorBuild: This component MUST be an integer in the format YYYYMMDD, representing the date the code was last modified. This date MUST be updated to the current date for any modification, however minor.Revision: This component is typically 0 for the first published version of a given distributable function or script at a given Major.Minor.Build. It counts same-day published updates of the same function or script relative to the previously published version, not work-in-progress iterations or commits. When a .NOTES version is assigned or updated, after applying the required Major, Minor, and Build values above, Revision MUST be 0 if the resulting Major.Minor.Build differs from the previously published version's Major.Minor.Build or if there is no previously published version. If the previously published version already records the same Major.Minor.Build at revision N, Revision MUST be N + 1. Same-day updates at the same Major.Minor.Build that increment Revision can include, but are not limited to:Trivial edits, such as typos, formatting, or comment fixesBug fixes that do not require a Major or Minor version bumpDocumentation-only updatesCasePreviously published versionThis changeReasonSame-day update1.2.20260619.01.2.20260619.1Same Major.Minor.Build, so N + 1.Same-day breaking change1.2.20260619.12.0.20260619.0Major changed, so reset to 0.Next-day update1.2.20260619.11.2.20260620.0Build date changed, so reset to 0.Compliant Example:PowerShell# .NOTES
# Version: 1.2.20251230.0
This example assumes that the current date is December 30, 2025. In any code you write, use the current date in place of December 30, 2025.Parameter Documentation Placement: Strategic ChoiceParameter help SHOULD be centralized in the comment-based help block, not duplicated above individual parameters in the param block.Help Format Options: ComparisonComment-based help MUST use single-line comments (#) for v1.0-compatible code. Block comments (<# ... #>) MUST NOT be used when v1.0 compatibility is required.⚠ PowerShell v1.0 Compatibility Warning: Block comments (<# ... #>) were introduced in PowerShell v2.0. In PowerShell v1.0, attempting to use block comments results in a parser error that prevents the script from running. Scripts targeting v1.0 compatibility MUST use only single-line comments (#). This applies to both comment-based help and general-purpose comments.Example — what fails in PowerShell v1.0:PowerShell# This will cause a parser error in PowerShell v1.0:
function Get-Example {
    <#
    .SYNOPSIS
        Example function.
    #>
    param ()
}
Correct approach for v1.0 compatibility:PowerShell# This works in all PowerShell versions, including v1.0:
function Get-Example {
    # .SYNOPSIS
    #     Example function.
    param ()
}
Functions and Parameter BlocksFunction Declaration and StructureAll functions MUST follow a strict, uniform template:PowerShellfunction Verb-Noun {
    # Full comment-based help block
    param (
        [type]$ParameterName1,
        [type]$ParameterName2 = default
    )
    # Implementation
    return $statusCode
}
Key characteristics:No [CmdletBinding()] → intentional omission for v1.0 compatibility; v1.0-targeted functions MUST NOT use thisNo pipeline blocks → process block would imply pipeline input, which MUST NOT be supported in v1.0-targeted functionsExplicit return → MUST be used to guarantee single-value output and prevent accidental pipeline leakageStrongly typed param block → MUST validate input at parse time[CmdletBinding()] and [OutputType()] Present → MUST be included for modern, non-v1.0 functions where either the function or script it sits in relies on external dependencies (e.g., a module that only supports Windows PowerShell v5.1 or PowerShell 7.x), making the function explicitly non-v1.0-compatible.Parameter Block Design: Detailed AnalysisThe param block is the primary contract between caller and function. Every parameter MUST be:Strongly typed using .NET typesFully documented in comment-based helpDefaulted where appropriate to ensure predictable behaviorException for Polymorphic Parameters:In rare cases, a function MAY be intentionally designed to accept a parameter that can be one of several different, incompatible types (e.g., a string or an object). This is common in "safe wrapper" functions that process dynamic input, such as the Principal element from an IAM policy.In this scenario, the parameter SHOULD be left un-typed (or explicitly typed as [object]). The function's internal logic is then responsible for inspecting the received object's type (e.g., using if ($MyParameter -is [string])) and handling it appropriately. This pattern SHOULD be used sparingly and only when required by the function's core purpose.Parameter typing examples:ParameterTypePurpose$ReferenceToResultObject[ref]Output: stores processed result (used only when modification in caller scope is needed)$ReferenceArrayOfExtraStrings[ref]Output: array for additional data (used only for write-back)$StringToProcess[string]Input: string to handle$PSVersion[version]Optional: runtime version for optimizationReference parameters ([ref]) are used exclusively for output where data MUST be written back to the caller's scope—a deliberate pattern to:Return multiple complex valuesAvoid pipeline interferenceMaintain v1.0 compatibilityEnsure caller controls variable lifetime[ref] SHOULD NOT be used for passing complex objects that do not require modification, as PowerShell passes object references by default without performance gains from [ref] in such cases.Default values are used judiciously:PowerShell[string]$StringToProcess = '',
[version]$PSVersion = ([version]'0.0')
This ensures the function can be called with minimal arguments while maintaining type safety.Return Semantics: Explicit Status CodesEvery v1.0-targeted function MUST return a single integer status code via explicit return statement:CodeMeaning0Full success1–5Partial success with additional data-1Complete failureException for Test-* Functions:For PowerShell v1.0 scripts/functions that use the Test- verb (in a Verb-Noun naming convention) and are not reasonably anticipated to encounter errors that the caller needs to detect and react to programmatically, a Boolean return MAY be used instead of an integer status code.This exception applies when:The function's verb is Test-The function is designed to return a simple true/false result (e.g., testing for the existence of a condition)There is no practical need for the caller to distinguish between different error conditions or partial success statesExample of Compliant Test Function with Boolean Return:PowerShellfunction Test-PathExists {
    # .SYNOPSIS
    # Tests whether a path exists.
    #
    # .DESCRIPTION
    # Returns $true if the path exists, $false otherwise.
    #
    # .PARAMETER Path
    # The path to test.
    #
    # .EXAMPLE
    # $boolPathExists = Test-PathExists -Path 'C:\Temp'
    #
    # # $boolPathExists is $true when the path exists.
    #
    # .INPUTS
    # None. You can't pipe objects to this function.
    #
    # .OUTPUTS
    # [bool] $true if the path exists, $false otherwise.
    #
    # .NOTES
    # This function supports positional parameters:
    #
    #   Position 0: Path
    #
    # Version: 1.0.20260517.0
    param (
        [string]$Path
    )

    return (Test-Path -LiteralPath $Path)
}
For Test-* functions that might encounter meaningful errors (e.g., access denied, network issues) that the caller SHOULD be able to detect, the standard integer status code pattern SHOULD still be used.Input/Output Contract: Reference ParametersFunctions MUST use [ref] parameters to return complex data only when write-back is required:PowerShell[ref]$ReferenceToResultObject     → [object]
[ref]$ReferenceArrayOfExtraStrings → [string[]]
[ref] SHOULD NOT be used for passing complex objects that do not require modification, as PowerShell passes object references by default.Pipeline Behavior: Deliberately DisabledIn v1.0-targeted functions, pipeline input MUST be explicitly rejected:No ValueFromPipeline attributes.INPUTS section states "None"No process blockIn scripts requiring modern PowerShell, pipeline support is added as needed.Positional Parameter SupportFunctions SHOULD support positional parameter binding for v1.0 usability:PowerShell# Named parameters
Process-String ([ref]$r) ([ref]$e) $str

# Positional parameters (documented in .NOTES)
Process-String ([ref]$r) ([ref]$e) $str $psver
Important distinction: While functions SHOULD support positional parameters in their declarations (for flexibility and v1.0 usability), function calls throughout the codebase SHOULD use named parameters for clarity and maintainability. PSScriptAnalyzer's PSAvoidUsingPositionalParameters rule is documented as flagging commands called with three or more positional parameters.[All] As an explicit syntax exception to the general preference that calls use named parameters, one positional message/payload argument passed to a covered Write-* cmdlet is idiomatic and acceptable when the cmdlet is available in the target runtime and otherwise permitted by this guide. Because this uses only one positional message/payload argument, it is below the documented analyzer threshold described above. Additional options SHOULD be named:PowerShellWrite-Warning 'No managed devices were returned.'
Write-Error 'Invalid object' -ErrorId B1 -TargetObject $_
Write-Information 'Scan complete.' -Tags 'Audit'
The covered allow-list is Write-Verbose, Write-Warning, Write-Debug, Write-Error, and Write-Information (the last only when targeting PowerShell 5.0+ and otherwise permitted by this guide). For Write-Error, this exception covers the default message form (Write-Error 'message') only; positional -Exception and positional -ErrorRecord payloads remain governed by the general named-parameter preference. For Write-Error, cmdlet-specific options such as -Category, -ErrorId, and -TargetObject SHOULD be named. For Write-Information, cmdlet-specific options such as -Tags SHOULD be named. Common parameters supported by the target runtime, such as -WarningAction and, on PowerShell 5.0+, -InformationAction, SHOULD likewise be named as common parameters.This exception does not cover Write-Output, Write-Host, or Write-Progress, and no other stream-writing cmdlets are included by implication. A blanket "always -Message" rule is not adopted because the canonical first message/payload parameter varies across the family, and Write-Output has no -Message parameter or alias. This clarifies call syntax only; it does not change existing output rules, including v1.0 explicit return-code patterns, modern streaming-output guidance, success-stream guidance, or the Write-Host prohibition.This enables:Interactive use without namingScript compatibility with older calling patternsFlexibility without sacrificing type safetyDocumenting Positional Parameters in .NOTESWhen a function or script supports positional parameters, the .NOTES section SHOULD use the following multi-line format to document which parameters are positional and at which positions:PowerShell# .NOTES
# This function/script supports positional parameters:
#
#   Position 0: VectorRows
#   Position 1: KMeansResult
#
# Version: 1.0.20250218.0
Guidance for this format:The header line SHOULD be # This function/script supports positional parameters: followed by each position listed on its own indented line as #   Position N: ParameterName.Only list parameters that are expected to be used positionally. For functions or scripts with many optional parameters, listing only the mandatory or commonly-used positional parameters is acceptable.The parameter name SHOULD match the declared parameter name without the - prefix (e.g., VectorRows, not -VectorRows), since the .NOTES section documents the parameter's identity, not its call syntax.[All] If positional parameter behavior is documented for a script/module/tool-specific private/internal helper, that documentation SHOULD clearly state that it is an internal-caller contract only and is subject to change. For example, the header line SHOULD read # This function supports positional parameters / # (internal-caller contract only; subject to change): instead of the standard header. Distributable/vendored helpers are exempt from this private-helper header and SHOULD document positional parameters as a stable distributable contract instead.[Modern] Enforcing a Subset-Only Positional Contract[Modern] When a [CmdletBinding()] function or script documents only a subset of its parameters as positional, it MUST use [CmdletBinding(PositionalBinding = $false)] and MUST apply explicit [Parameter(Position = N)] attributes only to the parameters intended to be positional. This rule does not apply to v1.0-targeted functions, which cannot use [CmdletBinding()].Compliant — subset-only positional contract enforced:PowerShellfunction Import-DataSet {
    [CmdletBinding(PositionalBinding = $false)]
    [OutputType([pscustomobject])]
    param (
        [Parameter(Mandatory = $true, Position = 0)]
        [string]$InputMode,

        [Parameter(Mandatory = $true, Position = 1)]
        [string]$OutputPath,

        [Parameter()]
        [switch]$Force,

        [Parameter()]
        [int]$RetryCount
    )

    # Only InputMode and OutputPath are positional;
    # Force and RetryCount must always be named.
    # ...
}
Non-compliant — default PositionalBinding contradicts documented subset contract:PowerShell# BAD: Documentation claims only InputMode and OutputPath are positional,
# but CmdletBinding() defaults to PositionalBinding = $true, which silently
# makes Force and RetryCount positional as well.
function Import-DataSet {
    [CmdletBinding()]
    [OutputType([pscustomobject])]
    param (
        [Parameter(Mandatory = $true)]
        [string]$InputMode,

        [Parameter(Mandatory = $true)]
        [string]$OutputPath,

        [Parameter()]
        [switch]$Force,

        [Parameter()]
        [int]$RetryCount
    )

    # .NOTES claims "Position 0: InputMode, Position 1: OutputPath"
    # but all parameters accept positional input — mismatch.
    # ...
}
Rule: "Modern Advanced" Function/Script Requirements (v2.0+)The "v1.0 Classicist" style is the default for standalone, portable utilities that MUST maintain backward compatibility.However, if a script or function cannot target v1.0, it MUST be written in the "Modern Advanced" style. This condition is met if the code:Has external module dependencies that require a modern PowerShell version (e.g., AWS.Tools, Az, Microsoft.Graph).Intentionally uses features from PowerShell v2.0 or later (e.g., try/catch, [pscustomobject] literals, Add-Type -AssemblyName), and there are no reasonable alternative approaches that can be used to ensure support for PowerShell v1.0.Functions and scripts written in this "Modern Advanced" style MUST adhere to the following rules:Must Use [CmdletBinding()]: All modern functions and scripts MUST use the [CmdletBinding()] attribute. This is the non-negotiable identifier of an advanced function or script and enables support for common parameters (-Verbose, -Debug, -ErrorAction, etc.). For modern scripts (.ps1 files that are not functions), [CmdletBinding()] and the param block MUST appear as the first statement in the script, other than permitted using statements, comments, and blank lines. Placing other statements before [CmdletBinding()] / param causes a ParseException when the script is invoked via the call operator (& $path).Must Use [OutputType()]: All modern functions and scripts MUST declare their primary output object type using [OutputType()]. This is critical for discoverability, integration, and validating the function's or script's contract.Must Use Streaming Output: Functions and scripts that return collections MUST write objects directly to the pipeline (stream) from within a loop. They MUST NOT collect results in a List<T> or array to be returned at the end. (See Processing Collections in Modern Functions).Must Use try/catch: Error handling MUST use try/catch blocks. The v1.0 trap / preference-toggling pattern is prohibited in this style.Must Use Proper Streams: Verbose and debug messages MUST be written to their respective streams (Write-Verbose, Write-Debug). Manual toggling of $VerbosePreference is prohibited.Example of a Compliant Modern Function:PowerShellfunction Get-ModernData {
    [CmdletBinding()]
    [OutputType([pscustomobject])]
    param (
        [Parameter(Mandatory = $true)]
        [string]$InputPath
    )

    process {
        Write-Verbose "Processing file: $InputPath"

        try {
            $data = Get-Content -LiteralPath $InputPath -ErrorAction Stop
            foreach ($line in $data) {
                # This is streaming output.
                [pscustomobject]@{
                    Length = $line.Length
                    Line = $line
                }
            }
        } catch {
            Write-Error -Message "Failed to process $InputPath: $($_.Exception.Message)"
        }
    }
}
Benefits: Pipeline-friendly, discoverableTrade-off: Breaks v1.0 compatibility"Modern Advanced" Functions/Scripts: Exception for Suppressing Nested Verbose StreamsRule 5 states that manual toggling of $VerbosePreference is prohibited. This rule's primary intent is to ensure your function or script respects the user's desire for verbose output from your script (via Write-Verbose).An exception to this rule MAY be made when you MUST surgically suppress the verbose stream from a "chatty" or "noisy" nested command (a command you call within your function or script). This pattern allows your function or script to remain verbose while silencing the underlying tool.In this specific scenario, you MUST use the following pattern to temporarily set $VerbosePreference and guarantee it is restored, even if the command fails:PowerShell# Save the user's current preference
$VerbosePreferenceAtStartOfBlock = $VerbosePreference

try {
    # Temporarily silence the verbose stream for the nested command
    $VerbosePreference = [System.Management.Automation.ActionPreference]::SilentlyContinue

    # Call the noisy command.
    $result = Get-NoisyCommand -Parameter $foo -ErrorAction Stop

    # Restore the preference *immediately* after the call
    $VerbosePreference = $VerbosePreferenceAtStartOfBlock

    # All logic that depends on $result's success MUST
    # also be inside the 'try' block.
    Write-Verbose "Successfully processed result from noisy command."
    # ... (other code that uses $result) ...
} catch {
    # If Get-NoisyCommand fails, this block will run and
    # the dependent logic above will be skipped.
    # Re-throw the error so the caller knows what happened.
    throw
} finally {
    # This 'finally' block ensures the preference is restored,
    # even if the 'catch' block runs and throws an error.
    $VerbosePreference = $VerbosePreferenceAtStartOfBlock
}
This try/finally pattern is robust, safe, and compliantly achieves your goal of controlling output from third-party cmdlets."Modern Advanced" Functions/Scripts: Singular [OutputType()]When a function returns one or more objects via the pipeline (streaming), the [OutputType()] attribute MUST declare the singular type of object in the stream (e.g., [OutputType([pscustomobject])]). Code MUST NOT use the plural array type (e.g., [OutputType([pscustomobject[]])]). The pipeline always creates an array for the caller automatically if multiple objects are returned."Modern Advanced" Functions/Scripts: Handling Multiple or Dynamic Output TypesWhen a function is intentionally designed to return different, non-related object types (e.g., a wrapper for ConvertFrom-Json which can return a single object, an array, or a scalar type), it is preferred to list all primary output types using multiple [OutputType()] attributes. This is far more descriptive and helpful to the caller than using a single, generic [OutputType([System.Object])].If a function's output type is truly dynamic and unpredictable, [OutputType([System.Object])] SHOULD be used only as a last resort, as it provides minimal value for discoverability."Modern Advanced" Functions/Scripts: Prioritizing Primary Output TypesWhen using multiple [OutputType()] attributes, the goal is to list the primary, high-level object types a user can expect. It is not necessary to create an exhaustive list of every possible scalar or primitive type (e.g., [int], [bool], [double]) if they are not the main, intended output of the function.This practice avoids cluttering the function's definition and keeps the developer's focus on the most common and important return values. For example, a JSON parsing function SHOULD list [pscustomobject] and [object[]], but does not need to list [int]."Modern Advanced" Functions/Scripts: Parameter Validation and Attributes ([Parameter()])Using [CmdletBinding()] unlocks powerful parameter validation attributes like [Parameter(Mandatory = $true)], [ValidateNotNullOrEmpty()], and [ValidateSet()].These are not stylistic requirements; they are design tools that MUST be used deliberately to enforce a function's operational contract.Use [Parameter(Mandatory = $true)] when:The function cannot possibly perform its core purpose without this value (e.g., $Identity for a Get-User function).You want the PowerShell engine to fail fast and prompt the user if it's missing.DO NOT Use [Parameter(Mandatory = $true)] when:The function is a "safe" wrapper or helper designed to handle any input, including $null.The function has a clear, graceful default behavior when the parameter is omitted (e.g., returning $null, an empty array, or $false).Example: The Convert-JsonFromPossiblyUrlEncodedString function is a "safe" wrapper. Its contract is to try to convert a string. A $null string is a valid input that SHOULD gracefully return $null, not throw a script-terminating error. Making $InputString mandatory would violate this "safe" contract.Prefer [ValidateNotNullOrEmpty()] over [Parameter(Mandatory = $true)] when:The parameter is technically optional, but if it is provided, it MUST NOT be an empty string.This is common for optional parameters like $LogPath or $Description.Also use [ValidateNotNullOrEmpty()] on mandatory [string] parameters when:The function's logic depends on the parameter having a non-empty value (e.g., computing a hash, constructing a path, or performing a lookup).PowerShell coerces $null to [string]::Empty for [string]-typed parameters. Because [string]::Empty is not $null, a mandatory [string] parameter satisfied by this coercion will pass the mandatory check but silently bind an empty string. This can cause incorrect behavior—for example, hashing an empty string instead of rejecting invalid input.Adding [ValidateNotNullOrEmpty()] alongside [Parameter(Mandatory = $true)] catches this edge case at parameter-binding time and produces a clear error message.This guidance applies to functions and scripts targeting Windows PowerShell 2.0 or newer, because [ValidateNotNullOrEmpty()] is not available in Windows PowerShell v1.0.Use [ValidateRange(min, max)] on numeric parameters when:The parameter has a constrained valid domain, such as counts, delays or timeouts, thresholds, or percentages.Fail-fast parameter binding provides a clearer error than allowing an invalid value to surface later in downstream logic.When the domain is naturally bounded on both sides, prefer explicit bounds (for example 0, 100 for percentages). When only a lower bound is principled, a type maximum such as [int]::MaxValue or [double]::MaxValue SHOULD be used as the upper bound to preserve the fail-fast benefit for the lower bound without imposing an artificial ceiling.This attribute is available in Windows PowerShell 2.0 and newer.Consuming Streaming Functions (The 0-1-Many Problem)When a function or script streams its output (whether it's a "modern advanced" function/script as mandated by the "Processing Collections" rule, or whether it's a standard, v1.0-compatible function and just happens to be streaming its output), the caller's variable will be $null if zero objects are returned, a scalar object if one object is returned, or an [object[]] array if multiple objects are returned.This can cause errors in subsequent code that always expects an array (e.g., foreach ($item in $result) or $result.Count).To ensure the result is always an array (even if empty or with a single item), the caller SHOULD wrap the function call in the array subexpression operator @(...). This is the standard, robust way to consume a streaming function and SHOULD be the default way to demonstrate usage in .EXAMPLE blocks.Compliant .EXAMPLE:PowerShell# .EXAMPLE
# $arrPrincipals = @(Expand-TrustPrincipal -PrincipalNode $statement.Principal)
#
# # This example shows how to safely call the function and guarantee the
# # result is an array, even if only one principal is returned.
Error HandlingCore Error Suppression Mechanismv1.0-targeted functions MUST use two complementary v1.0-native suppression techniques:TechniqueImplementationPurposetrap { }Empty trap block at function scopeCatches terminating errors (e.g., type cast failures) and prevents script termination$global:ErrorActionPreference = 'SilentlyContinue'Temporarily set before risky operation, restored immediately afterSuppresses non-terminating error output to hostPowerShelltrap { }  # Intentional error suppression
$originalPref = $global:ErrorActionPreference
$global:ErrorActionPreference = [System.Management.Automation.ActionPreference]::SilentlyContinue
# Risky operation here
$global:ErrorActionPreference = $originalPref  # State restoration
Key characteristics:No error leakage to host → script continuesState preservation → original preference restoredv1.0 compatibility → works in all PowerShell versionsError Detection: Reference-Based ComparisonThe author rejects unreliable heuristics ($?, $Error[0].Exception, null checks) and implements a reference-equality detection system using two custom helper functions:Get-ReferenceToLastError: Returns [ref]$Error[0] if errors exist, [ref]$null otherwiseTest-ErrorOccurred: Compares two [ref] objects to determine if a new error appearedDetection workflow:PowerShell$refBefore = Get-ReferenceToLastError    # Snapshot pre-operation
# ... perform risky operation ...
$refAfter = Get-ReferenceToLastError     # Snapshot post-operation
$errorOccurred = Test-ErrorOccurred $refBefore $refAfter
Reference comparison logic:Before \ After$nullNot $null (same)Not $null (different)$nullNoYESN/ANot $nullNoNoYESThis eliminates false positives from $error array clearing and ensures 100% accurate error detection.Atomic Error Handling PatternEvery type conversion or risky operation MUST follow this exact atomic pattern:PowerShellfunction Convert-Safely {
    param([ref]$refOutput, [string]$input)

    trap { }  # Suppress termination
    $refBefore = Get-ReferenceToLastError
    $originalPref = $global:ErrorActionPreference
    $global:ErrorActionPreference = 'SilentlyContinue'

    $refOutput.Value = [type]$input  # Risky cast

    $global:ErrorActionPreference = $originalPref
    $refAfter = Get-ReferenceToLastError

    return (-not (Test-ErrorOccurred $refBefore $refAfter))
}
Key guarantees:Operation is isolated — error cannot affect callerState is restored — preference resetResult is boolean — $true = success, $false = failureNo side effects — even on failureAnomaly Reporting: Write-Warning for Logical ImpossibilitiesWrite-Warning MUST be used sparingly to flag logically impossible states (contract violations). Code MUST NOT suppress these warnings.PowerShellWrite-Warning -Message 'Conversion failed even though individual parts succeeded. This should not be possible!'
Error Context PreservationDespite suppression, full error context is preserved in the global $Error array (original ErrorRecord objects remain intact with stack trace and exception details).Modern catch Block RequirementsIn modern functions using try/catch (i.e., those not targeting v1.0), catch blocks MUST NOT be empty. An empty catch block is flagged by PSScriptAnalyzer and provides no diagnostic value.Architectural Context: Library/Helper Functions vs. Higher-Level CodeThe return-code and error-swallowing patterns described in the preceding v1.0 sections are primarily associated with library/helper functions — highly reusable building blocks that handle operational errors internally and communicate failure through an explicitly documented contract (e.g., integer return codes, reference outputs). These functions are designed to never throw, and their non-throwing behavior MUST be documented in .DESCRIPTION and .OUTPUTS. While v1.0 compatibility is a common consequence of this design goal, the non-throwing contract itself is the primary architectural motivation; a modern function can adopt the same pattern when the design requires it.For modern higher-level functions and scripts — code that orchestrates these building blocks or performs tasks for end users — the default expectation is that unexpected failures propagate to the caller.Default Pattern: Write-Debug + throwThe standard catch pattern for modern advanced functions and scripts SHOULD log the error to the Debug stream and then re-throw it so that unexpected failures propagate to the caller. This SHOULD be the default unless the function is explicitly designed as a non-throwing wrapper with a documented contract.PowerShell# Default: log and re-throw
try {
    ...
} catch {
    Write-Debug ("Failed to do X: {0}" -f $_)
    throw
}
Rethrow Anti-PatternWhen a catch block is intended to rethrow, throw "message" and throw ("format string" -f $args) MUST NOT be used. These forms throw a string that PowerShell wraps into a new RuntimeException/ErrorRecord, discarding the original exception type, stack trace, and ErrorRecord. This makes root-cause analysis significantly harder and breaks any caller logic that catches specific exception types. This prohibition applies only to catch blocks whose intent is to preserve and propagate the original failure; catch blocks that intentionally translate an error into a new, independently documented message (such as the file writeability tests) are not subject to this rule.PowerShell# WRONG — destroys the original exception:
try {
    Get-Item -LiteralPath $strPath -ErrorAction Stop
} catch {
    throw "Failed to get item: $($_.Exception.Message)"
}

# WRONG — same problem with -f operator:
try {
    Get-Item -LiteralPath $strPath -ErrorAction Stop
} catch {
    throw ("Failed to get item: {0}" -f $_.Exception.Message)
}
Adding Context Before RethrowingIf contextual information is needed before rethrowing, it SHOULD be logged via Write-Debug before the bare throw. This preserves the original exception while still providing diagnostic context on the Debug stream, reinforcing the Default Pattern.PowerShell# Correct — context logged, original exception preserved:
try {
    Get-Item -LiteralPath $strPath -ErrorAction Stop
} catch {
    Write-Debug ("Failed to get item at path '{0}': {1}" -f $strPath, $_)
    throw
}
Wrapping Exceptions with $PSCmdlet.ThrowTerminatingError()If an exception must be wrapped with additional context while still propagating, the preferred pattern for advanced functions SHOULD use $PSCmdlet.ThrowTerminatingError() and preserve the original exception as the InnerException. This approach maintains the full exception chain for callers while adding meaningful context.PowerShell# Correct — wraps with context, preserves original as InnerException:
function Get-ResolvedItem {
    [CmdletBinding()]
    param (
        [string]$Path
    )

    try {
        Get-Item -LiteralPath $Path -ErrorAction Stop
    } catch {
        $objException = [System.InvalidOperationException]::new(
            ("Failed to resolve item at path '{0}'" -f $Path),
            $_.Exception
        )
        $objErrorRecord = [System.Management.Automation.ErrorRecord]::new(
            $objException,
            'ResolvedItemFailure',
            [System.Management.Automation.ErrorCategory]::ObjectNotFound,
            $Path
        )
        $PSCmdlet.ThrowTerminatingError($objErrorRecord)
    }
}
Note: The above wrapping pattern is appropriate only when additional context is genuinely needed beyond what Write-Debug + bare throw provides. In most cases, the Default Pattern is sufficient.Documented Non-Throwing ExceptionA modern function MAY intentionally handle an exception without re-throwing only when its contract explicitly specifies non-throwing behavior. In that case, the function's comment-based help (.DESCRIPTION and .OUTPUTS) MUST clearly document that failures are communicated through return values, output state, warnings, or another defined mechanism rather than by throwing.PowerShell# Non-throwing wrapper with documented contract
function Convert-SafelyFromJson {
    # .SYNOPSIS
    # Converts a JSON string to an object without throwing on invalid input.
    #
    # .DESCRIPTION
    # Attempts to convert a JSON string to an object. This function does
    # NOT throw on invalid input; instead it returns $null and logs the
    # error to the Debug stream. Callers MUST check the return value.
    #
    # .PARAMETER JsonString
    # JSON string to convert.
    #
    # .EXAMPLE
    # $objResult = Convert-SafelyFromJson -JsonString '{"name":"example"}'
    #
    # # $objResult is a converted object on success, or $null on failure.
    #
    # .INPUTS
    # None. You can't pipe objects to this function.
    #
    # .OUTPUTS
    # [object] on success; $null on failure.
    #
    # .NOTES
    # This function supports positional parameters:
    #
    #   Position 0: JsonString
    #
    # Version: 1.0.20260517.0
    [CmdletBinding()]
    [OutputType([object])]
    param (
        [string]$JsonString
    )

    if ([string]::IsNullOrEmpty($JsonString)) {
        return $null
    }

    try {
        $JsonString | ConvertFrom-Json -ErrorAction Stop
    } catch {
        Write-Debug ("JSON conversion failed: {0}" -f $_)
        $null
    }
}
Set-StrictMode Considerations for finally BlocksWhen Set-StrictMode -Version Latest is in effect, referencing a variable that has never been assigned raises a terminating error. This creates a subtle but important pitfall when a finally block references a variable that is assigned inside the corresponding try block (for example, a disposable resource). If an exception occurs before the assignment executes, Set-StrictMode will raise a terminating error for the uninitialized variable inside finally, which can mask the original exception and interfere with proper cleanup.Rule: When a finally block references a variable that is assigned inside the corresponding try block, that variable MUST be initialized before the try block, typically to $null.Compliant Example:PowerShell$objResource = $null
try {
    $objResource = [SomeDisposable]::Create()
    # ... use $objResource ...
} finally {
    if ($null -ne $objResource) {
        $objResource.Dispose()
    }
}
In this example, $objResource is initialized to $null before the try block. If [SomeDisposable]::Create() throws before the assignment completes, the finally block can safely check $null -ne $objResource without triggering a Set-StrictMode violation.Set-StrictMode Placement for Dot-Sourced FilesWhere Set-StrictMode -Version Latest belongs depends on how the .ps1 file is consumed at runtime. A .ps1 file that is dot-sourced executes its script-scope statements in the caller's scope, which means a script-scope Set-StrictMode call leaks into the caller and silently changes the caller's strict-mode setting. By contrast, when code is consumed through an imported module or by executing a script or aggregate artifact normally (for example, .\Helpers.ps1, & .\Helpers.ps1, or Import-Module), script-scope statements run in that artifact's own script scope, so a script-scope Set-StrictMode call is contained to that scope.Rule (bundled files): For files bundled into a module or other aggregate script artifact, Set-StrictMode -Version Latest MUST be placed at script scope as the first executable statement in the file, after any required file-header constructs such as #requires comments, using statements, and any script-level [CmdletBinding()]/param block. The bundled artifact may also establish strict mode, making this redundant at runtime, but it preserves file-level correctness if the source file is ever executed directly. This rule does not make dot-sourcing the source file safe: dot-sourcing any .ps1 file — including an individual bundled source file or a monolithic bundled artifact — still runs its script-scope statements in the caller's scope and will leak strict mode.Rule (dot-sourced files): For files that are not bundled and are instead intended to be dot-sourced directly into the caller's scope (for example, test fixtures, ad-hoc scripts, or build tooling), Set-StrictMode -Version Latest MUST NOT be placed at script scope. Instead, it MUST be placed inside the function body — as the first statement in begin {} when the function uses a begin/process/end layout (so strict mode covers begin, process, and end, and is not re-invoked for every pipeline input), or otherwise as the first statement in the function body.Bundled File — Compliant ExamplePowerShell#requires -Version 5.1
using namespace System.Text

Set-StrictMode -Version Latest

function Get-Thing {
    [CmdletBinding()]
    [OutputType([string])]
    param (
        [string]$Name
    )

    process {
        # ... implementation ...
    }
}
Bundled File — Non-Compliant ExamplePowerShell# Set-StrictMode is missing at file scope. If the bundled artifact fails to
# establish strict mode, or if this file is executed independently,
# strict-mode guarantees are lost.
function Get-Thing {
    [CmdletBinding()]
    [OutputType([string])]
    param (
        [string]$Name
    )

    process {
        # ... implementation ...
    }
}
Dot-Sourced File — Compliant ExamplePowerShellfunction Invoke-TestFixture {
    [CmdletBinding()]
    [OutputType([void])]
    param (
        [string]$Path
    )

    begin {
        Set-StrictMode -Version Latest
    }

    process {
        # ... implementation ...
    }
}
Dot-Sourced File — Non-Compliant ExamplePowerShell# WRONG — when this file is dot-sourced, Set-StrictMode executes in the
# caller's scope and silently changes the caller's strict-mode setting.
Set-StrictMode -Version Latest

function Invoke-TestFixture {
    [CmdletBinding()]
    [OutputType([void])]
    param (
        [string]$Path
    )

    process {
        # ... implementation ...
    }
}
File Writeability TestingScripts that write output to files MUST verify the destination path is writable before performing any significant processing (preflight check for invalid paths, missing directories, insufficient permissions, read-only locations, locked files).Approaches.NET approach (Test-FileWriteability): Comprehensive, uses .NET file operations. MUST be used for v1.0-targeted scripts (since try/catch causes parser errors in v1.0).try/catch approach: Shorter (~10 lines), requires PowerShell v2.0+.Both use a create-then-delete pattern. The delete step catches additional failure modes (e.g., file locks on Windows) that file creation alone may miss.[v1.0] scripts MUST use the .NET approach. [Modern] scripts MAY use either approach.Prefer .NET for mission-critical/unattended scripts, or where v1.0 parseability is needed. Prefer try/catch for simple utilities or when minimizing size.Code Examples.NET ApproachBundle Test-FileWriteability from the reference implementation:PowerShell$errRecord = $null
$boolIsWritable = Test-FileWriteability -Path 'Z:\InvalidPath\file.log' -ReferenceToErrorRecord ([ref]$errRecord)
if (-not $boolIsWritable) {
    Write-Warning ('Failed to write to path. Error: ' + $errRecord.Exception.Message)
    return # replace with an appropriate exiting action
}
try/catch ApproachPowerShelltry {
    $strOutputPath = $ExecutionContext.SessionState.Path.GetUnresolvedProviderPathFromPSPath($OutputPath)
    $strWriteTestPath = [System.IO.Path]::Combine([System.IO.Path]::GetDirectoryName($strOutputPath), ('.write_test_{0}.tmp' -f [Guid]::NewGuid().ToString('N')))
    [System.IO.File]::Open($strWriteTestPath, [System.IO.FileMode]::CreateNew, [System.IO.FileAccess]::Write).Dispose()
    [System.IO.File]::Delete($strWriteTestPath)
} catch {
    throw ("Cannot write to '{0}': {1}" -f $OutputPath, $_.Exception.Message)
}
Warning: File APIs with create-or-overwrite semantics (e.g., [System.IO.File]::Create(), New-Item -Force) SHOULD NOT be used for writeability probes unless the probe filename is guaranteed unique. Using the actual output path as the probe can destroy pre-existing data or cause false failures when the file already exists.Reference ImplementationFull Test-FileWriteability implementation: https://github.com/franklesniak/PowerShell_Resources/blob/master/Test-FileWriteability.ps1Operating System Compatibility ChecksPlatform-specific scripts/functions MUST include OS checks before platform-specific operations. Fail early — perform checks at the beginning of the function or script.PowerShell Core 6.0+ OS DetectionUse built-in variables: $IsWindows, $IsMacOS, $IsLinux.PowerShellif (-not $IsWindows) {
    Write-Error -Message "This function only runs on Windows."
    return -1
}
Cross-Version OS DetectionFor scripts supporting PowerShell older than 6.0 (including Windows PowerShell 1.0–5.1), $IsWindows/$IsMacOS/$IsLinux do not exist; referencing them yields $null or throws under strict mode, causing incorrect behavior. Use safe detection functions from PowerShell_Resources:OSFunctionLinkWindowsTest-WindowsTest-Windows.ps1macOSTest-macOSTest-macOS.ps1LinuxTest-LinuxTest-Linux.ps1PowerShell$boolIsWindows = Test-Windows
if (-not $boolIsWindows) {
    Write-Warning -Message "This function only runs on Windows."
    return -1
}
Error Handling for Wrong OSReport errors consistently with the script's existing error handling pattern (status codes, exceptions, or Write-Error). Error messages SHOULD clearly state which OS(es) are required.Language Interop, Versioning, and .NETRuntime Version Detection: Get-PSVersionA dedicated version probe returns a [System.Version] object:PowerShellfunction Get-PSVersion {
    if (Test-Path variable:\PSVersionTable) {
        return $PSVersionTable.PSVersion
    } else {
        return [version]'1.0'
    }
}
Returns actual version on v2.0+; falls back to [version]'1.0' when $PSVersionTable is absent.Conditional .NET Feature Usage: Progressive EnhancementUse PowerShell version as a feature flag for .NET types:PowerShellif ($versionPowerShell.Major -ge 3) {
    $boolResult = Convert-StringToBigIntegerSafely ...
} else {
    $boolResult = Convert-StringToDoubleSafely ...
}
PowerShell Version.NET Type UsedNumeric Rangev3.0+[System.Numerics.BigInteger]Unlimited (subject to memory)v1.0–v2.0[double]±1.7 × 10³⁰⁸ (IEEE 754)All versions[int], [int64]Built-in safe conversions.NET Interop Patterns: Safe and Documented.NET UsageTechnical Justification[regex]::Escape() + [regex]::Split()Literal string splitting in v1.0 (alternative to v2.0+ -split)[System.Numerics.BigInteger]Overflow handling — only when PS v3+ detectedDeprecation of System.Collections.ArrayList: ArrayList is deprecated and MUST NOT be used in new code. Use System.Collections.Generic.List[T] instead (available since .NET 2.0 / PS v1.0). ArrayList is only permitted as a caught-exception fallback, reported via debug stream.PowerShell# Compliant
$list = New-Object System.Collections.Generic.List[PSCustomObject]

# Non-Compliant (Deprecated)
$list = New-Object System.Collections.ArrayList
Typed Generic Collections: The specific type T MUST be provided if known (e.g., [PSCustomObject], [string]), not [object].PowerShell Array Accumulation: Code MUST NOT grow a PowerShell array with += inside an accumulation loop. PowerShell arrays are fixed-size, so each += creates a new array and copies the existing elements. When a collection must be accumulated in memory, code MUST use System.Collections.Generic.List[T] with .Add() or .AddRange(), and convert to an array with .ToArray() only at a boundary where an array is actually required. This rule complements, and does not weaken, the requirement that modern functions stream output when streaming is the correct contract.PowerShell# Compliant
$listOutput = New-Object System.Collections.Generic.List[PSCustomObject]
foreach ($objItem in $InputObject) {
    [void]($listOutput.Add($objItem))
}
$arrOutput = $listOutput.ToArray()

# Non-Compliant
$arrOutput = @()
foreach ($objItem in $InputObject) {
    $arrOutput += $objItem
}
.NET Type Usage Summary.NET TypeFirst AvailableTechnical Purpose[regex].NET 2.0 (PS v1.0)Literal string parsing[System.Numerics.BigInteger].NET 4.0 (PS v3.0+)Unlimited integer precision[version].NET 2.0Standard version semantics[ref].NET 2.0Multiple return values (only for write-back)All types are v1.0-safe except BigInteger, which is guarded by version check.Output Formatting and StreamsPrimary Output: Integer Status Code via returnv1.0-targeted functions return a single [int] status code via explicit return:PowerShellreturn 0    # Full success
return 4    # Partial success
return -1   # Complete failure
Document in .OUTPUTS: # [int] Status code: 0=success, 1-5=partial with additional data, -1=failureProcessing Collections in Modern Functions (Streaming Output)A modern (non-v1.0) function SHOULD NOT build a large collection (like a List<T>) and return it at the end. This is memory-inefficient, as it requires holding all results in memory, and often creates an unnecessary O(n) performance hit when the list is copied.The preferred, idiomatic PowerShell pattern is to "stream" the output: write each result object directly to the pipeline from within the processing loop. This is highly memory-efficient and aligns with the pipeline's "one object at a time" philosophy.Compliant (Streaming): Write objects to the pipeline inside your loop.Non-Compliant (Collecting): Adding all objects to a $list and returning $list at the end.Compliant (Streaming) Example:PowerShell[CmdletBinding()]
[OutputType([pscustomobject])]
param(...)

foreach ($objItem in $SourceData) {
    # ... logic to create $objResult ...
    $objResult # This writes the object to the pipeline
}
# Note: There is no 'return' statement for the collection
Non-Compliant (Collecting) Example:PowerShell[CmdletBinding()]
[OutputType([pscustomobject[]])] # Unnecessary plural
param(...)

$listOutput = New-Object System.Collections.Generic.List[PSCustomObject]
foreach ($objItem in $SourceData) {
    # ... logic ...
    [void]($listOutput.Add($objResult))
}
return $listOutput.ToArray() # Unnecessary copy and non-idiomatic
This rule is distinct from the v1.0-native pattern, which uses explicit integer return codes and passes data via [ref] parameters. The v1.0-native pattern MAY be desireable in situations where the function SHOULD return no output in the event of any error occurring during processing, or where error/warning status needs to be passed back to the caller.Complex Output: Reference Parameters ([ref])All structured data is returned via [ref] parameters only when write-back to the caller is required.Stream Usage: Clear MappingStreamCommandPurposeSuccessreturnPrimary result (status code)WarningWrite-WarningLogical anomalies (contract violations)HostNever usedProhibited — Write-Host MUST NOT be usedv1.0-targeted functions MUST NOT emit mixed object types on the success stream.Choosing Between Warning and Debug StreamsThe choice of output stream is critical for communicating intent:Warning Stream (Write-Warning): Reserved for logical anomalies or conditions that the end-user SHOULD be aware of, but which do not halt execution (e.g., "Could not determine root user email for account X").Debug Stream (Write-Debug): Used for logging internal function details that are not relevant to the end-user but are critical for diagnostics. This includes handled catch block errors, or fallback logic (e.g., "Failed to create generic lists; falling back to ArrayLists.").Suppression of Method OutputWhen calling .NET methods that return a value (like System.Collections.ArrayList.Add()), that output MUST be suppressed to avoid polluting the pipeline. The preferred method is to cast the entire statement to [void] for performance, as it is measurably faster than piping to | Out-Null.PowerShell# Compliant (Preferred for performance)
[void]($list.Add($item))

# Non-Compliant (Typically slower than casting to void)
$list.Add($item) | Out-Null
Sensitive Data in Verbose and Debug StreamsFunctions MUST NOT emit raw PII, credentials, secrets, tokens, or sensitive identifiers via Write-Verbose or Write-Debug. Use safe alternatives: boolean presence flags, non-sensitive metadata (length, count, type name), or redacted values.PowerShell# Non-Compliant
Write-Verbose -Message ('PrincipalKey: ' + $PrincipalKey)

# Compliant - logs whether the value is present (boolean)
Write-Verbose -Message ('PrincipalKey present: {0}' -f ($null -ne $PrincipalKey))
Performance-Sensitive Write-Verbose / Write-Debug in Hot Paths[Modern] functions that are called per-record or inside tight loops (that is, hot paths) SHOULD guard Write-Verbose and Write-Debug calls that perform string formatting — such as with the -f operator or string concatenation — behind an appropriate preference check to avoid unconditional string allocation overhead when the stream is not enabled.Recommended pattern for Write-Verbose:PowerShellif ($VerbosePreference -ne 'SilentlyContinue') {
    Write-Verbose ("Processing item: {0}" -f $strCurrentItem)
}
Recommended pattern for Write-Debug:PowerShellif ($DebugPreference -ne 'SilentlyContinue') {
    Write-Debug ("Processing item: {0}" -f $strCurrentItem)
}
Note: This guard is recommended only for performance-sensitive code paths and is NOT required for functions that run once, or only a small number of times, per pipeline or script execution.Testing with PesterPester 5.x is required. Legacy 3.x/4.x patterns MUST NOT be used. Pester requires PowerShell 3.0+ to run, but scripts under test can target any version. See pester.dev.Test File Naming and LocationTest files MUST use *.Tests.ps1 suffixTest files SHOULD be in a tests/ directory at the repository rootOne test file per function/script SHOULD be createdPester 5.x Syntax RequirementsTests MUST use Pester 5.x syntax. Legacy Pester 3.x/4.x patterns MUST NOT be used.BlockPurposeBeforeAllOne-time setup at the beginning of a Describe or Context block (e.g., dot-sourcing the function under test)BeforeEachSetup before each It block (use sparingly)AfterAll / AfterEachTeardown (cleanup resources, restore state)DescribeGroups tests for a single function or scriptContextGroups tests for a specific scenario or conditionItDefines an individual test caseShouldAssertion cmdlet for validating expected outcomesKey Pester 5.x Changes:Use BeforeAll for dot-sourcing scripts (not at the file level outside blocks)Discovery and Run phases are separate—code at the top level runs during discoveryCode MUST use Should -Be, Should -BeExactly, Should -BeNullOrEmpty, etc. (not legacy Assert-* patterns)Test File Dot-Sourcing PatternPester test files that dot-source scripts under test in BeforeAll MUST use the Split-Path + Join-Path two-step pattern. This pattern resolves the parent directory of the test file's directory and then builds the path to the source file:PowerShellBeforeAll {
    $strSrcPath = Join-Path -Path (Split-Path -Path $PSScriptRoot -Parent) -ChildPath 'src'
    . (Join-Path -Path $strSrcPath -ChildPath 'FunctionName.ps1')
}
Why this pattern is required:Multi-segment Join-Path forms such as Join-Path $PSScriptRoot '..' 'src' 'FunctionName.ps1' rely on the -AdditionalChildPath parameter, which was introduced in PowerShell 6.0 and is not available in Windows PowerShell 5.1. Test files MUST NOT use this form.For consistency and canonical style in test files, $PSScriptRoot-anchored .. path forms such as $PSScriptRoot/../src/... or Join-Path -Path $PSScriptRoot -ChildPath '../src/...' MUST NOT be used; use the explicit parent-resolution pattern instead.Test Structure: Arrange-Act-AssertTests SHOULD follow the Arrange-Act-Assert (AAA) pattern for clarity and maintainability:Arrange: Set up test data, preconditions, and inputsAct: Execute the function or script under testAssert: Verify the output matches expectationsEach It block SHOULD test one specific behavior. Use comments to delineate the AAA sections for readability.Example:PowerShellIt "Returns success code 0 when given valid input" {
    # Arrange
    $refResult = $null
    $strInput = "valid-input"

    # Act
    $intReturnCode = Get-ProcessedData -ReferenceToResult ([ref]$refResult) -InputString $strInput

    # Assert
    $intReturnCode | Should -Be 0
}
Defensive Assertions Before Iteration and IndexingWhen a test iterates or indexes into a collection returned by the function or script under test, the test MUST include defensive pre-assertions so that an empty or $null result produces a clear, immediate Pester failure instead of silently passing or generating a confusing runtime error.Pre-iteration non-emptiness. Tests that iterate a collection with foreach ($x in $collection) { ... } MUST assert $collection | Should -Not -BeNullOrEmpty before the foreach. A foreach over $null or an empty collection executes zero iterations, causing all inner assertions to be silently skipped.Pre-index count assertion. Tests that access specific indices of a returned collection (e.g., $arrResult[0]) MUST assert $arrResult.Count | Should -Be <N> before any indexed access when the exact count is part of the contract being tested. If exact count is not part of the contract, the test MUST assert a minimum-count condition that covers the highest index accessed—for example, Should -BeGreaterThan <highest-index-accessed> (since collections are zero-based, $arr.Count | Should -BeGreaterThan 2 guarantees that $arr[0], $arr[1], and $arr[2] are safe to access).Pre-index non-empty on nested properties. When a test indexes into a property of a returned element (e.g., $arrResult[0].Principals[0]), the test MUST also assert $arrResult[0].Principals | Should -Not -BeNullOrEmpty before the inner index.Ordering. For a test that accesses $arr[i].Prop[j], assertions SHOULD follow this order:$arr | Should -Not -BeNullOrEmpty or $arr.Count | Should -Be <N>$arr[i].Prop | Should -Not -BeNullOrEmptyStrong-type check on $arr[i].Prop, if applicableAssertions that verify the actual behavior under testCompliant (foreach — assert non-emptiness before iterating):PowerShellIt "Each ClusterActions entry includes a Principals array" {
    # Assert
    $script:objResult.ClusterActions | Should -Not -BeNullOrEmpty
    foreach ($objCluster in $script:objResult.ClusterActions) {
        $objCluster.PSObject.Properties.Name | Should -Contain 'Principals'
        $objCluster.Principals | Should -Not -BeNullOrEmpty
        ($objCluster.Principals -is [string[]]) | Should -BeTrue
    }
}
Non-Compliant (foreach — missing non-emptiness assertion):PowerShell# Non-Compliant: foreach over $null or an empty collection can execute zero
# iterations and leave the test without any evaluated inner assertions.
It "Each ClusterActions entry includes a Principals array" {
    # Assert
    foreach ($objCluster in $script:objResult.ClusterActions) {
        $objCluster.PSObject.Properties.Name | Should -Contain 'Principals'
    }
}
Compliant (indexed access — count and nested non-emptiness before indexing):PowerShell# Assert
$arrResult.Count | Should -Be 1
$arrResult[0].Principals | Should -Not -BeNullOrEmpty
$arrResult[0].Principals.Count | Should -Be 2
$arrResult[0].Principals[0] | Should -Be 'userA'
$arrResult[0].Principals[1] | Should -Be 'userB'
Non-Compliant (indexed access — no count assertion before [0]):PowerShell# Non-Compliant: no count assertion before [0].
# Assert
$arrResult[0].Principals.Count | Should -Be 1
$arrResult[0].Principals[0] | Should -Be 'userA'
Asserting Successful Execution With Should -Not -ThrowWhen a Pester test's purpose is to assert that a call succeeds — that is, completes without throwing — the test MUST wrap the invocation in a script block and assert it with Should -Not -Throw. Such tests MUST NOT use try { ... } catch { $e = $_ } followed only by negated assertions against exception text (for example, Should -Not -Match) as the mechanism for proving success. Negated assertions on exception text silently pass when an unrelated exception is thrown whose message does not happen to match the negated pattern, producing a green result for fundamentally broken code.Tests whose purpose is to assert a specific expected failure MAY inspect exception details, but follow-up assertions on the captured exception MUST fail when the expected exception is absent or different — for example, Should -Throw -ExpectedMessage '<pattern>', or Should -Throw -PassThru (which returns the thrown ErrorRecord) or an explicit try { ... } catch { $e = $_ } to capture the exception, followed by assertions such as Should -Match or Should -Be against the captured object. A presence guard that fails when no exception was captured — specifically $e | Should -Not -BeNullOrEmpty immediately after a try/catch capture — IS permitted (and SHOULD be used before dereferencing $e.Exception) because it fails when $e is $null, which is the "expected exception absent" case. Should -Throw without -PassThru does not implicitly expose the thrown exception; a capture mechanism is required before any follow-up assertion. Negated assertions against exception text (for example, $e.Exception.Message | Should -Not -Match '<pattern>') MUST NOT be used as the sole mechanism for validating either success or expected failure, because any exception whose message does not match the negated pattern — including an unrelated exception — will silently satisfy the assertion.Compliant (success assertion — Should -Not -Throw fails on any exception):PowerShellIt "Completes without throwing for valid input" {
    # Arrange
    $strInput = 'valid-data'

    # Act / Assert
    { Convert-StringToObject -StringToConvert $strInput } | Should -Not -Throw
}
Non-Compliant (success assertion — try/catch plus negated message assertion can pass on an unrelated failure):PowerShell# Non-Compliant: if the function throws for an unrelated reason whose message
# does not contain 'invalid', the negated -Not -Match assertion still passes
# and the test reports success even though the call failed.
It "Completes without throwing for valid input" {
    # Arrange
    $strInput = 'valid-data'
    $e = $null

    # Act
    try {
        Convert-StringToObject -StringToConvert $strInput
    } catch {
        $e = $_
    }

    # Assert
    $e.Exception.Message | Should -Not -Match 'invalid'
}
Compliant (expected-failure assertion — capture with -PassThru and assert positively):PowerShellIt "Throws a specific error for invalid input" {
    # Arrange
    $strInput = 'bad-data'

    # Act
    $errorRecord = { Convert-StringToObject -StringToConvert $strInput } |
        Should -Throw -PassThru

    # Assert
    $errorRecord.Exception.Message | Should -Match 'invalid'
}
Compliant (expected-failure assertion — capture with try/catch and assert positively):PowerShellIt "Throws a specific error for invalid input" {
    # Arrange
    $strInput = 'bad-data'
    $e = $null

    # Act
    try {
        Convert-StringToObject -StringToConvert $strInput
    } catch {
        $e = $_
    }

    # Assert — positive assertion fails when $e is $null (no exception thrown)
    $e | Should -Not -BeNullOrEmpty
    $e.Exception.Message | Should -Match 'invalid'
}
Testing Return Code ConventionsFor functions and scripts that use explicit integer status codes, tests MUST verify the return code conventions documented in Return Semantics: Explicit Status Codes.Note for functions and scripts that return objects: If a function or script returns [pscustomobject] or other structured data instead of integer status codes, this section does not apply. For such cases, output contract verification — including edge cases such as $null returns — SHOULD be covered by Pester tests in accordance with Testing with Pester, where applicable.Functions Returning Integer Status CodesFor functions that return integer status codes (0 = success, 1-5 = partial success, -1 = failure), tests MUST cover:Return CodeTest Requirement0At least one test verifying success case1-5At least one test for partial success cases (if applicable to the function)-1At least one test verifying failure caseAdditionally, if the function uses [ref] parameters for output:Tests MUST verify the reference parameter is populated correctly on successTests MUST verify the reference parameter state on failure (typically $null or unchanged)Example for Integer Status Code Function:PowerShellDescribe "Convert-StringToObject" {
    BeforeAll {
        $strSrcPath = Join-Path -Path (Split-Path -Path $PSScriptRoot -Parent) -ChildPath 'src'
        . (Join-Path -Path $strSrcPath -ChildPath 'Convert-StringToObject.ps1')
    }

    Context "When given valid input" {
        It "Returns 0 for success" {
            # Arrange
            $refResult = $null
            $strInput = "valid-data"

            # Act
            $intReturnCode = Convert-StringToObject -ReferenceToResult ([ref]$refResult) -StringToConvert $strInput

            # Assert
            $intReturnCode | Should -Be 0
        }

        It "Populates the reference parameter with the converted object" {
            # Arrange
            $refResult = $null
            $strInput = "valid-data"

            # Act
            [void](Convert-StringToObject -ReferenceToResult ([ref]$refResult) -StringToConvert $strInput)

            # Assert
            $refResult | Should -Not -BeNullOrEmpty
        }
    }

    Context "When given invalid input" {
        It "Returns -1 for failure" {
            # Arrange
            $refResult = $null
            $strInput = ""

            # Act
            $intReturnCode = Convert-StringToObject -ReferenceToResult ([ref]$refResult) -StringToConvert $strInput

            # Assert
            $intReturnCode | Should -Be -1
        }
    }
}
Test-* Functions Returning BooleanFor Test-* functions that return Boolean values (as documented in the exception for Test-* functions), tests MUST verify:A case that returns $trueA case that returns $falseExample for Boolean Test Function:PowerShellDescribe "Test-PathExists" {
    BeforeAll {
        $strSrcPath = Join-Path -Path (Split-Path -Path $PSScriptRoot -Parent) -ChildPath 'src'
        . (Join-Path -Path $strSrcPath -ChildPath 'Test-PathExists.ps1')
    }

    Context "When the path exists" {
        It "Returns true" {
            # Arrange
            $strPath = $env:TEMP  # Known to exist

            # Act
            $boolResult = Test-PathExists -Path $strPath

            # Assert
            $boolResult | Should -BeTrue
        }
    }

    Context "When the path does not exist" {
        It "Returns false" {
            # Arrange
            $strPath = "C:\NonExistent\Path\That\Does\Not\Exist"

            # Act
            $boolResult = Test-PathExists -Path $strPath

            # Assert
            $boolResult | Should -BeFalse
        }
    }
}
Testing Property Names on PSCustomObjectWhen testing that a [pscustomobject] contains the expected property names, assertions MUST use an order-insensitive comparison. Although PSObject.Properties.Name preserves declaration order in practice for objects created via the [pscustomobject] type accelerator with a hashtable literal, this ordering is not a documented guarantee. Tests SHOULD NOT rely on property ordering because:Future refactors might change the property declaration order.Objects constructed via Add-Member or other mechanisms may not preserve insertion order.Order-insensitive tests are more resilient and communicate intent more clearly.Per-property containment (preferred when property count is small):PowerShell$objResult.PSObject.Properties.Name | Should -Contain 'Key'
$objResult.PSObject.Properties.Name | Should -Contain 'Type'
$objResult.PSObject.Properties.Name | Should -HaveCount 2
Sorted array comparison (acceptable alternative — the expected array must be in sorted order to match the Sort-Object output):PowerShell($objResult.PSObject.Properties.Name | Sort-Object) |
    Should -Be @('Key', 'Type')
Non-Compliant (order-sensitive — fragile):PowerShell# Non-Compliant
$objResult.PSObject.Properties.Name | Should -Be @('Key', 'Type')
Testing Strongly-Typed Array PropertiesWhen asserting that a property on a returned object is a non-empty, strongly-typed array, tests MUST follow these rules:Non-emptiness first. Tests MUST use Should -Not -BeNullOrEmpty before any .Count-based assertion. This produces a clear failure message when the property is $null or empty, rather than a confusing "expected greater than 0" when the property is $null.Strongly-typed assertion. When production code explicitly casts an output property to a strongly-typed array (e.g., [string[]]), tests MUST assert that exact array type using the -is operator wrapped in Should -BeTrue:PowerShell($obj.Prop -is [string[]]) | Should -BeTrue
Tests MUST NOT use a disjunction that also permits [object[]], because that masks regressions when the intended production cast is accidentally removed.Avoid Should -BeOfType [string[]] for array types. Tests SHOULD NOT use $x | Should -BeOfType [string[]] to assert array type, because the pipeline unrolls the array before Pester evaluates the type. Prefer the -is [string[]] pattern.Ordering. When combined with a property-name check, the recommended assertion order SHOULD be: property name first, then non-empty assertion, then strongly-typed assertion.Compliant (preferred pattern):PowerShell$script:objResult.ClusterActions | Should -Not -BeNullOrEmpty
foreach ($objCluster in $script:objResult.ClusterActions) {
    $objCluster.PSObject.Properties.Name | Should -Contain 'Principals'
    $objCluster.Principals | Should -Not -BeNullOrEmpty
    ($objCluster.Principals -is [string[]]) | Should -BeTrue
}
Non-Compliant (too permissive):PowerShell# Non-Compliant: [object[]] disjunction masks regressions in the
# production strongly-typed cast.
(($objCluster.Principals -is [string[]]) -or ($objCluster.Principals -is [object[]])) |
    Should -BeTrue

# Non-Compliant: .Count on a potentially-null value is asserted before
# proving the property is non-empty.
$objCluster.Principals.Count | Should -BeGreaterThan 0
Non-Compliant (pipeline unrolling):PowerShell# Non-Compliant: the array is unrolled before Pester evaluates the type assertion.
$objCluster.Principals | Should -BeOfType [string[]]
Mocking External DependenciesUse Pester's Mock command to isolate the function under test from external dependencies:PowerShellContext "When external service is unavailable" {
    BeforeAll {
        Mock Get-ExternalData { throw "Connection failed" }
    }

    It "Returns failure code -1 and does not throw" {
        # Arrange
        $refResult = $null

        # Act
        $intReturnCode = Process-ExternalData -ReferenceToResult ([ref]$refResult)

        # Assert
        $intReturnCode | Should -Be -1
    }
}
Mocking Guidelines:Mock cmdlets and external commands that introduce dependencies (network, file system, cloud services)Mock at the narrowest scope possible (prefer Context-level mocks over Describe-level)Use Assert-MockCalled to verify expected interactions when appropriatePSScriptAnalyzer CI Diagnostic OutputWhen a PSScriptAnalyzer CI integration emits host-native diagnostics in addition to or instead of plain analyzer output, it MUST use the command format for the active CI host. GitHub Actions annotations MUST use GitHub Actions workflow commands such as ::warning file=...,line=...::... or ::error file=...,line=...::.... Azure Pipelines issues MUST use Azure Pipelines logging commands such as ##vso[task.logissue type=warning;sourcepath=...;linenumber=...]... or ##vso[task.logissue type=error;sourcepath=...;linenumber=...].... These command syntaxes MUST NOT be interchanged.When a command string includes dynamic values such as file paths, line numbers, rule names, messages, or titles, those values MUST be formatted, escaped, or encoded according to the active host's command syntax before they are written to the log. File paths SHOULD be emitted in the form the active host expects so that diagnostics resolve to the correct file.Host-neutral, local, and interactive runs SHOULD use plain PSScriptAnalyzer output unless the active CI host is explicitly known. If host detection is ambiguous, missing, or contradictory, the integration MUST use plain PSScriptAnalyzer output and MUST NOT emit host-native diagnostic commands.Running Pester TestsFor local developer runs, use the documented project test root directly:PowerShellInvoke-Pester -Path tests/ -Output Detailed
CI workflow runs often need a PowerShell run: step that performs both test discovery and Pester execution. In those steps, CI Pester discovery (Get-ChildItem ... -Filter '*.Tests.ps1' -Recurse) and execution (the Pester configuration Run.Path) MUST be scoped to the project-owned tests/ tree or to the project's documented test root. They MUST NOT scan from the repository root, because root-level scanning can sweep up unrelated tests, including starter, sample, template, vendored, or dependency *.Tests.ps1 files, and produce a misleading green test signal.The Pester configuration Run.Path value and the discovery step's path MUST be derived from a single source of truth, such as a workflow-level env: value like PESTER_TEST_ROOT, so the discovery scope and execution scope cannot drift apart.The discovery step SHOULD guard against a missing test root using Test-Path -LiteralPath ... -PathType Container so projects that have not yet created or have intentionally removed the tests/ directory still see a clean "no test files" skip rather than a workflow error. Using -PathType Container keeps the skip scoped to "the test root is a missing directory"; a bare Test-Path would also succeed when the path resolves to a file (for example a mis-set PESTER_TEST_ROOT), masking a real misconfiguration as a clean skip. Get-ChildItem ... -ErrorAction SilentlyContinue MAY be used as an alternative, but it is NOT equivalent: SilentlyContinue also suppresses non-existence-related errors such as permission or IO failures, which can mask genuine CI problems as a clean skip. A Test-Path guard followed by Get-ChildItem without -ErrorAction SilentlyContinue is preferred.Compliant (single env-var-driven test root for discovery and execution):YAML- name: Run Pester tests
  shell: pwsh
  env:
    PESTER_TEST_ROOT: tests
  run: |
    $strPesterTestRoot = Join-Path -Path $env:GITHUB_WORKSPACE -ChildPath $env:PESTER_TEST_ROOT
    $arrPesterTestFiles = @()

    if (Test-Path -LiteralPath $strPesterTestRoot -PathType Container) {
        $arrPesterTestFiles = @(
            Get-ChildItem -LiteralPath $strPesterTestRoot -Filter '*.Tests.ps1' -Recurse -File
        )
    }

    if ($arrPesterTestFiles.Count -eq 0) {
        Write-Output ("No Pester test files found under '{0}'." -f $strPesterTestRoot)
        exit 0
    }

    $objPesterConfiguration = New-PesterConfiguration
    $objPesterConfiguration.Run.Path = $strPesterTestRoot
    $objPesterConfiguration.Output.Verbosity = 'Detailed'
    Invoke-Pester -Configuration $objPesterConfiguration
Non-compliant (repository-root discovery and execution):YAML- name: Run Pester tests
  shell: pwsh
  run: |
    $arrPesterTestFiles = @(
        Get-ChildItem -Path . -Filter '*.Tests.ps1' -Recurse -File
    )

    if ($arrPesterTestFiles.Count -eq 0) {
        Write-Output "No Pester test files found."
        exit 0
    }

    $objPesterConfiguration = New-PesterConfiguration
    $objPesterConfiguration.Run.Path = '.'
    $objPesterConfiguration.Output.Verbosity = 'Detailed'
    Invoke-Pester -Configuration $objPesterConfiguration
Performance, Security, and OtherPrefer -LiteralPath Over -Path for Concrete PathsWhen a cmdlet supports both -Path and -LiteralPath, and the code is operating on a single concrete path value—not an intentionally wildcarded pattern—-LiteralPath SHOULD be used instead of -Path. This especially applies when the path is derived from variables, Join-Path, or string construction, because -Path interprets wildcard characters ([, ], *, ?) and can silently match the wrong files or match nothing at all.For destructive operations—Remove-Item, Move-Item—-LiteralPath MUST be used when the path value comes from a variable or expression. Wildcard interpretation of a variable-derived path in a destructive cmdlet can silently delete or move unintended files.Reserve -Path for cases where wildcard expansion is explicitly intended.Exception — New-Item: New-Item does not have a -LiteralPath parameter (across Windows PowerShell 5.1 and PowerShell 7.x). Use New-Item -Path for item creation. Because -Path still interprets wildcard characters, code SHOULD validate or reject untrusted input containing [, ], *, or ? as literal characters, or use a .NET file API (e.g., [System.IO.File]::Create()) when literal path semantics are required.Directory creation: When creating a directory from a variable-derived path that may contain wildcard characters ([, ], *, or ?), code SHOULD prefer [System.IO.Directory]::CreateDirectory() over New-Item -Path ... -ItemType Directory. The path MUST first be resolved to an absolute filesystem path per Resolving Paths for .NET Static Methods.Compliant (wildcard-safe directory creation):PowerShell$strOutputPath = $ExecutionContext.SessionState.Path.GetUnresolvedProviderPathFromPSPath($OutputPath)
if (-not (Test-Path -LiteralPath $strOutputPath)) {
    [void]([System.IO.Directory]::CreateDirectory($strOutputPath))
}
Common cmdlets where this rule applies: Copy-Item, Get-ChildItem, Get-Content, Get-Item, Move-Item, Remove-Item, Set-Content, Test-Path.Compliant:PowerShellTest-Path -LiteralPath $strFilePath
Get-Content -LiteralPath $strConfigFile -ErrorAction Stop
Remove-Item -LiteralPath $strTempFile -Force
Non-compliant (variable-derived path with -Path):PowerShell# Risk: $strFilePath may contain [] or wildcard characters
Test-Path -Path $strFilePath
Get-Content -Path $strConfigFile -ErrorAction Stop
Remove-Item -Path $strTempFile -Force   # Dangerous: destructive + wildcard
Acceptable (intentional wildcard):PowerShell# Intentional wildcard — -Path is correct here:
Get-ChildItem -Path 'C:\Logs\*.log'
Remove-Item -Path 'C:\Temp\*.tmp' -Force
