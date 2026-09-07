<!-- Context: Part 1 of 3 for LLM ingestion - PowerShell Writing Style Guide -->
<!-- markdownlint-disable MD013 -->

# PowerShell Writing Style

**Version:** 2.23.20260726.0

## Metadata

- **Status:** Active
- **Owner:** Repository Maintainers
- **Last Updated:** 2026-07-26
- **Scope:** PowerShell coding standards for all `.ps1` files in this repository — style, formatting, naming, error handling, documentation, and compatibility patterns for both legacy (v1.0) and modern (v2.0+) codebases.

## Applicability and Portability

- This guide is self-contained and intended for standalone use or vendoring into another repository.
- Apply each requirement according to its scope tag and any explicit conditions.
- Requirements tied to an optional toolchain, file type, or repository feature apply when the adopting project uses or intentionally adopts that surface.
- Additional repository-wide instructions in the adopting repository continue to apply; this guide creates no exception to them.
- Resolve actual conflicts through the adopting repository's documented precedence rules.

## Keywords

Per [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119): **MUST** / **SHALL** / **REQUIRED** = absolute requirement; **MUST NOT** / **SHALL NOT** = absolute prohibition; **SHOULD** / **RECOMMENDED** = strong recommendation (deviations require justification); **SHOULD NOT** / **NOT RECOMMENDED** = strong discouragement; **MAY** / **OPTIONAL** = truly optional.

<!-- rationale-anchor: keywords-extended-explanation -->

## Quick Reference Checklist

Scope tags: **[All]** = all PowerShell versions, **[Modern]** = PowerShell v2.0+ (requires features not available in v1.0), **[v1.0]** = backward compatible with Windows PowerShell v1.0. Each item links to its detailed section.

### Code Layout and Formatting (Quick Reference)

- **[All]** Code **MUST** use 4 spaces for indentation, never tabs → [Indentation Rules](#indentation-rules)
- **[All]** Opening braces **MUST** be placed on same line (OTBS) → [Brace Placement (OTBS)](#brace-placement-otbs)
- **[All]** `catch`, `finally`, `else` **MUST** be on same line as closing brace → [Exception: catch, finally, and else Keywords](#exception-catch-finally-and-else-keywords)
- **[All]** Code **MUST** use single space around operators, no extra alignment → [Operator Spacing and Alignment](#operator-spacing-and-alignment)
- **[All]** Operators **MUST NOT** be vertically aligned across multiple lines → [Operator Spacing and Alignment](#operator-spacing-and-alignment)
- **[All]** Multi-line method parameters **MUST** have extra indentation → [Multi-line Method Indentation](#multi-line-method-indentation)
- **[All]** Blank lines **SHOULD** be used sparingly: two around functions, one within → [Blank Line Usage](#blank-line-usage)
- **[All]** Blank lines **MUST NOT** contain any whitespace (spaces or tabs) → [Blank Line Usage](#blank-line-usage)
- **[All]** Lines **MUST NOT** end with trailing whitespace → [Trailing Whitespace](#trailing-whitespace)
- **[All]** Variables in strings **SHOULD** be delimited with `${}` or `-f` operator → [Variable Delimiting in Strings](#variable-delimiting-in-strings)
- **[All]** Source `.ps1` files **MUST** be UTF-8 without BOM by default; see [File Encoding](#file-encoding) for the Windows PowerShell/non-ASCII exception
- **[All]** When writing text files programmatically, encoding **MUST** be specified explicitly; prefer `.NET` for cross-version UTF-8 without BOM → [Programmatic File Writing Encoding](#programmatic-file-writing-encoding)
- **[All]** When producing byte-exact text artifacts, serializer output **MUST** be normalized to LF in memory before writing or comparing → [Line Endings for Byte-Exact Text Artifacts](#line-endings-for-byte-exact-text-artifacts)
- **[All]** Text-level file comparison **MUST** read files with `Get-Content -Raw` or `[System.IO.File]::ReadAllText()` under a fixed encoding/BOM convention; `Get-Content` without `-Raw` **MUST NOT** be used → [Line Endings for Byte-Exact Text Artifacts](#line-endings-for-byte-exact-text-artifacts)
- **[All]** True byte-for-byte comparison **MUST** read files with `[System.IO.File]::ReadAllBytes()`; this is required for hash/signature inputs and any other byte-exact identity check → [Line Endings for Byte-Exact Text Artifacts](#line-endings-for-byte-exact-text-artifacts)

### Capitalization and Naming Conventions (Quick Reference)

- **[All]** Public identifiers (functions, parameters, properties) **MUST** use PascalCase → [Capitalization and Naming Conventions](#capitalization-and-naming-conventions)
- **[All]** PowerShell keywords (function, param, if, else, return, trap) **MUST** be lowercase → [Capitalization and Naming Conventions](#capitalization-and-naming-conventions)
- **[All]** Local variables **MUST** use camelCase with type-hinting prefixes, fully descriptive (e.g., $strMessage,$intCount, no abbreviations) → [Local Variable Naming: Type-Prefixed camelCase](#local-variable-naming-type-prefixed-camelcase)
- **[All]** Functions **MUST** follow Verb-Noun pattern with approved verbs → [Script and Function Naming: Full Explicit Form](#script-and-function-naming-full-explicit-form)
- **[All]** Functions **MUST** use singular nouns in function names → [Script and Function Naming: Nouns](#script-and-function-naming-nouns)
- **[All]** Modules **MUST** use PascalCase nouns (containers, not actions) → [Module Naming: Noun-Based Containers](#module-naming-noun-based-containers)
- **[Modern]** Module manifest `Tags` key **MUST** be populated aggressively with relevant keywords for discoverability → [Module Naming: Noun-Based Containers](#module-naming-noun-based-containers)
- **[All]** Aliases **MUST NOT** be used in code → [Do Not Use Aliases](#do-not-use-aliases)
- **[Modern]** Modules **MUST NOT** export compatibility aliases (exception: genuine interactive shortcuts) → [Do Not Use Aliases](#do-not-use-aliases)
- **[All]** Parameters **MUST** use PascalCase, fully descriptive names → [Parameter Naming](#parameter-naming)
- **[v1.0]** Reference parameters **MUST** use "ReferenceTo" prefix → [Parameter Naming](#parameter-naming)
- **[All]** Code **SHOULD** avoid relative paths and tilde (~) shortcut → [Path and Scope Handling](#path-and-scope-handling)
- **[All]** Code **SHOULD** use explicit scoping ($global:,$script:) → [Path and Scope Handling](#path-and-scope-handling)
- **[All]** `-LiteralPath` **SHOULD** be used instead of `-Path` when operating on concrete (non-wildcard) paths derived from variables or `Join-Path` → [Prefer `-LiteralPath` Over `-Path` for Concrete Paths](#prefer--literalpath-over--path-for-concrete-paths)
- **[All]** For destructive cmdlets (`Remove-Item`, `Move-Item`), `-LiteralPath` **MUST** be used for variable-derived paths → [Prefer `-LiteralPath` Over `-Path` for Concrete Paths](#prefer--literalpath-over--path-for-concrete-paths)
- **[All]** `New-Item` does **not** support `-LiteralPath`; use `-Path` with `New-Item` → [Prefer `-LiteralPath` Over `-Path` for Concrete Paths](#prefer--literalpath-over--path-for-concrete-paths)
- **[All]** For directory creation from variable-derived paths that may contain wildcard characters, prefer `[System.IO.Directory]::CreateDirectory()` → [Prefer `-LiteralPath` Over `-Path` for Concrete Paths](#prefer--literalpath-over--path-for-concrete-paths)
- **[All]** Paths passed to .NET file APIs (`System.IO.*`) **MUST** be resolved to absolute via `GetUnresolvedProviderPathFromPSPath()` first; non-FileSystem provider paths **MUST NOT** be used → [Resolving Paths for .NET Static Methods](#resolving-paths-for-net-static-methods)

### Documentation and Comments (Quick Reference)

- **[All]** All functions **MUST** have full comment-based help → [Comment-Based Help: Structure and Format](#comment-based-help-structure-and-format)
- **[All]** Comment-based help **MUST** be placed inside function body, above param block → [Comment-Based Help: Structure and Format](#comment-based-help-structure-and-format)
- **[All]** Comment-based help **MUST** use single-line comments (#) with dotted keywords (.SYNOPSIS, .DESCRIPTION, etc.) → [Comment-Based Help: Structure and Format](#comment-based-help-structure-and-format)
- **[v1.0]** Block comments (`<# ... #>`) **MUST NOT** be used — they cause parser errors in PowerShell v1.0; use single-line comments (`#`) instead → [Help Format Options: Comparison](#help-format-options-comparison)
- **[All]** Comment-based help **MUST** include sections: .SYNOPSIS, .DESCRIPTION, .PARAMETER (one per parameter, if any), .EXAMPLE, .INPUTS, .OUTPUTS, .NOTES → [Comment-Based Help: Structure and Format](#comment-based-help-structure-and-format)
- **[All]** Comment-based help **MUST** use exactly one comment blank line between top-level help sections → [Comment-Based Help Spacing](#comment-based-help-spacing)
- **[All]** Explanatory or output-description lines within `.EXAMPLE` blocks **MUST** use double `#` (`# # <text>`) so that `Get-Help` renders them as valid PowerShell comments (`# <text>`) → [Inline Comments Within `.EXAMPLE` Blocks](#inline-comments-within-example-blocks)
- **[All]** Functions **SHOULD** provide multiple examples with input, output, and explanation → [Help Content Quality: High Standards](#help-content-quality-high-standards)
- **[All]** Every possible output/return value **MUST** be documented in .OUTPUTS with exact type and meaning; integer status codes **MUST** include full code-to-meaning mapping; output examples **MUST** be placed in .EXAMPLE blocks → [Help Content Quality: High Standards](#help-content-quality-high-standards)
- **[All]** Positional parameter support **MUST** be documented in .NOTES → [Help Content Quality: High Standards](#help-content-quality-high-standards)
- **[All]** Script/module/tool-specific private/internal helper functions' `.NOTES` **MUST** begin with a private-helper banner; distributable/vendored helpers with a per-function license region and clear cross-project reuse intent are exempt → [Private/Internal Helper Function Documentation](#privateinternal-helper-function-documentation)
- **[Modern]** Functions omitted from module manifest `FunctionsToExport` are treated as private/internal helpers unless the distributable/vendored-helper exemption applies → [Private/Internal Helper Function Documentation](#privateinternal-helper-function-documentation)
- **[All]** Positional parameter documentation for script/module/tool-specific private/internal helpers **SHOULD** state it is an internal-caller contract only; distributable/vendored helpers document a stable distributable contract → [Positional Parameter Support](#positional-parameter-support)
- **[All]** Version number **MUST** be included in .NOTES (format: Major.Minor.YYYYMMDD.Revision) → [Function and Script Versioning](#function-and-script-versioning)
- **[All]** Version build component **MUST** be current date in YYYYMMDD format → [Function and Script Versioning](#function-and-script-versioning)
- **[All]** `.NOTES` `Revision` **MUST** reset to `0` when `Major`, `Minor`, or `Build` changes; otherwise increment (`N + 1`) for same-day updates → [Function and Script Versioning](#function-and-script-versioning)
- **[All]** Inline comments **SHOULD** focus on "why" not "what" → [Inline Comments: Purpose and Placement](#inline-comments-purpose-and-placement)
- **[All]** Code **SHOULD** use #region / #endregion for logical code folding → [Structural Documentation: Regions and Licensing](#structural-documentation-regions-and-licensing)
- **[All]** The param() block **MUST** be placed before license region (if applicable) → [Structural Documentation: Regions and Licensing](#structural-documentation-regions-and-licensing)
- **[All]** Distributable helpers **SHOULD** use per-function licensing (#region License after param block) → [Structural Documentation: Regions and Licensing](#structural-documentation-regions-and-licensing)
- **[All]** Parameter documentation **SHOULD** be centralized in help block, not above individual parameters → [Parameter Documentation Placement: Strategic Choice](#parameter-documentation-placement-strategic-choice)

### Functions and Parameter Blocks (Quick Reference)

- **[v1.0]** v1.0-targeted functions **MUST NOT** use [CmdletBinding()] attribute → [Function Declaration and Structure](#function-declaration-and-structure)
- **[v1.0]** v1.0-targeted functions **MUST NOT** use [OutputType()] attribute → [Function Declaration and Structure](#function-declaration-and-structure)
- **[v1.0]** v1.0-targeted functions **MUST NOT** use begin/process/end blocks → [Function Declaration and Structure](#function-declaration-and-structure)
- **[v1.0]** v1.0-targeted functions **MUST NOT** support pipeline input → [Pipeline Behavior: Deliberately Disabled](#pipeline-behavior-deliberately-disabled)
- **[v1.0]** v1.0-targeted functions **MUST** use simple function keyword with param() block → [Function Declaration and Structure](#function-declaration-and-structure)
- **[v1.0]** Parameters **MUST** use strong typing → [Parameter Block Design: Detailed Analysis](#parameter-block-design-detailed-analysis)
- **[v1.0]** v1.0-targeted functions **MUST** use explicit return statements → [Return Semantics: Explicit Status Codes](#return-semantics-explicit-status-codes)
- **[v1.0]** Reference parameters ([ref]) **MUST** be used for outputs requiring caller modification → [Input/Output Contract: Reference Parameters](#inputoutput-contract-reference-parameters)
- **[v1.0]** Functions **MUST** return single integer status code (0=success, 1-5=partial, -1=failure) → [Return Semantics: Explicit Status Codes](#return-semantics-explicit-status-codes)
- **[v1.0]** Exception: Test-* functions **MAY** return Boolean when no practical error handling needed → [Return Semantics: Explicit Status Codes](#return-semantics-explicit-status-codes)
- **[v1.0]** Positional parameters **SHOULD** be supported for v1.0 usability → [Positional Parameter Support](#positional-parameter-support)
- **[All]** One positional message/payload argument to covered `Write-*` cmdlets is an allowed syntax exception; additional options **SHOULD** be named → [Positional Parameter Support](#positional-parameter-support)
- **[v1.0]** v1.0-targeted functions **MUST** use trap-based error handling (not try/catch) → [Core Error Suppression Mechanism](#core-error-suppression-mechanism)
- **[Modern]** Modern functions and scripts **MUST** use [CmdletBinding()] attribute → [Rule: "Modern Advanced" Function/Script Requirements (v2.0+)](#rule-modern-advanced-functionscript-requirements-v20)
- **[Modern]** Modern functions and scripts **MUST** use [OutputType()] declaring singular primary type → [Rule: "Modern Advanced" Function/Script Requirements (v2.0+)](#rule-modern-advanced-functionscript-requirements-v20)
- **[Modern]** Modern functions and scripts **MUST** use streaming output (write objects directly to pipeline in loop) → [Rule: "Modern Advanced" Function/Script Requirements (v2.0+)](#rule-modern-advanced-functionscript-requirements-v20)
- **[Modern]** Modern functions and scripts **MUST** use try/catch for error handling → [Rule: "Modern Advanced" Function/Script Requirements (v2.0+)](#rule-modern-advanced-functionscript-requirements-v20)
- **[Modern]** Modern functions and scripts **MUST** use Write-Verbose and Write-Debug (not manual preference toggling) → [Rule: "Modern Advanced" Function/Script Requirements (v2.0+)](#rule-modern-advanced-functionscript-requirements-v20)
- **[Modern]** Exception: Modern functions and scripts **MAY** temporarily suppress $VerbosePreference for noisy nested commands using try/finally → ["Modern Advanced" Functions/Scripts: Exception for Suppressing Nested Verbose Streams](#modern-advanced-functionsscripts-exception-for-suppressing-nested-verbose-streams)
- **[Modern]** [Parameter(Mandatory=$true)] **SHOULD** be used only when function cannot work without value → ["Modern Advanced" Functions/Scripts: Parameter Validation and Attributes (`[Parameter()]`)](#modern-advanced-functionsscripts-parameter-validation-and-attributes-parameter)
- **[Modern]** [ValidateNotNullOrEmpty()] **SHOULD** be used for optional-but-not-empty parameters and for mandatory [string] parameters whose logic depends on a non-empty value → ["Modern Advanced" Functions/Scripts: Parameter Validation and Attributes (`[Parameter()]`)](#modern-advanced-functionsscripts-parameter-validation-and-attributes-parameter)
- **[Modern]** [ValidateRange(min, max)] **SHOULD** be used on numeric parameters with a constrained valid domain (counts, delays/timeouts, thresholds, percentages) so invalid input fails at parameter binding rather than producing a confusing downstream error → ["Modern Advanced" Functions/Scripts: Parameter Validation and Attributes (`[Parameter()]`)](#modern-advanced-functionsscripts-parameter-validation-and-attributes-parameter)
- **[Modern]** Multiple [OutputType()] **SHOULD** only be used for intentionally polymorphic returns → ["Modern Advanced" Functions/Scripts: Handling Multiple or Dynamic Output Types](#modern-advanced-functionsscripts-handling-multiple-or-dynamic-output-types)
- **[Modern]** Subset-only positional contracts **MUST** use `PositionalBinding = $false` with explicit `[Parameter(Position = N)]` → [Positional Parameter Support](#positional-parameter-support)
- **[All]** Functions **MUST** be atomic, reusable tools with single purpose → [Function Declaration and Structure](#function-declaration-and-structure)
- **[All]** Polymorphic parameters (multiple incompatible types) **SHOULD** be left un-typed or [object] → [Parameter Block Design: Detailed Analysis](#parameter-block-design-detailed-analysis)
- **[All]** [ref] **MUST** be used exclusively for output requiring write-back to caller scope → [Input/Output Contract: Reference Parameters](#inputoutput-contract-reference-parameters)
- **[All]** [ref] **MUST NOT** be used for complex objects that don't need modification → [Input/Output Contract: Reference Parameters](#inputoutput-contract-reference-parameters)

### Error Handling (Quick Reference)

- **[v1.0]** v1.0-targeted functions **MUST** use trap {} for error suppression → [Core Error Suppression Mechanism](#core-error-suppression-mechanism)
- **[Modern]** catch blocks **MUST NOT** be empty; default pattern is `Write-Debug` + `throw` → [Modern catch Block Requirements](#modern-catch-block-requirements)
- **[Modern]** Non-throwing catch (no `throw`) **MUST** have a documented non-throwing contract → [Modern catch Block Requirements](#modern-catch-block-requirements)
- **[Modern]** `throw "message"` and `throw ("fmt" -f $args)` **MUST NOT** be used in catch blocks intended to rethrow → [Rethrow Anti-Pattern](#rethrow-anti-pattern)
- **[Modern]** Exception wrapping **SHOULD** use `$PSCmdlet.ThrowTerminatingError()` with the original as `InnerException` → [Wrapping Exceptions with `$PSCmdlet.ThrowTerminatingError()`](#wrapping-exceptions-with-pscmdletthrowterminatingerror)
- **[Modern]** Variables referenced in `finally` that are assigned in `try` **MUST** be initialized before the `try` block → [Set-StrictMode Considerations for finally Blocks](#set-strictmode-considerations-for-finally-blocks)
- **[Modern]** In files bundled into a module or other aggregate script artifact, `Set-StrictMode -Version Latest` **MUST** be placed at script scope as the first executable statement in the file, after any `#requires` comments, `using` statements, and any script-level `[CmdletBinding()]`/`param` block → [Set-StrictMode Placement for Dot-Sourced Files](#set-strictmode-placement-for-dot-sourced-files)
- **[Modern]** In files intended to be dot-sourced directly into the caller's scope (test fixtures, ad-hoc scripts, build tooling), `Set-StrictMode -Version Latest` **MUST NOT** be placed at script scope; it **MUST** be placed inside the function body (as the first statement in `begin {}` when using a `begin/process/end` layout, or otherwise as the first statement in the function body) → [Set-StrictMode Placement for Dot-Sourced Files](#set-strictmode-placement-for-dot-sourced-files)

### File Writeability Testing (Quick Reference)

- **[All]** Scripts **MUST** verify file writeability before significant processing when writing output to files → [File Writeability Testing](#file-writeability-testing)
- **[v1.0]** v1.0-targeted scripts **MUST** use `.NET` approach (`Test-FileWriteability` function) → [Approaches](#approaches)
- **[Modern]** Scripts **MAY** use `.NET` or `try/catch` approach based on requirements → [Approaches](#approaches)

### Operating System Compatibility Checks (Quick Reference)

- **[All]** Scripts/functions supporting only specific operating systems **MUST** include OS compatibility checks → [Operating System Compatibility Checks](#operating-system-compatibility-checks)
- **[Modern]** PowerShell Core 6.0+ only scripts **SHOULD** use built-in `$IsWindows`, `$IsMacOS`, `$IsLinux` variables → [PowerShell Core 6.0+ OS Detection](#powershell-core-60-os-detection)
- **[v1.0]** Scripts supporting older versions **MUST** use `Test-Windows`, `Test-macOS`, `Test-Linux` functions from PowerShell_Resources → [Cross-Version OS Detection](#cross-version-os-detection)
- **[All]** Wrong OS errors **MUST** be reported consistently with existing error handling patterns → [Error Handling for Wrong OS](#error-handling-for-wrong-os)

### Output Formatting and Streams (Quick Reference)

- **[Modern]** Modern functions **MUST NOT** collect results in `List<T>` and return; **MUST** stream objects to pipeline → [Processing Collections in Modern Functions (Streaming Output)](#processing-collections-in-modern-functions-streaming-output)
- **[Modern]** Streaming function calls **SHOULD** be wrapped in @(...) to handle 0-1-Many problem → [Consuming Streaming Functions (The `0-1-Many` Problem)](#consuming-streaming-functions-the-0-1-many-problem)
- **[All]** Code **MUST** use Write-Warning for user-facing anomalies; Write-Debug for internal details → [Choosing Between Warning and Debug Streams](#choosing-between-warning-and-debug-streams)
- **[All]** .NET method output **MUST** be suppressed with [void](...), not | Out-Null → [Suppression of Method Output](#suppression-of-method-output)
- **[All]** `Write-Verbose` / `Write-Debug` **MUST NOT** emit raw PII, credentials, tokens, or other sensitive identifiers → [Sensitive Data in Verbose and Debug Streams](#sensitive-data-in-verbose-and-debug-streams)
- **[Modern]** Hot-path `Write-Verbose` / `Write-Debug` with string formatting **SHOULD** be guarded behind a preference check → [Performance-Sensitive `Write-Verbose` / `Write-Debug` in Hot Paths](#performance-sensitive-write-verbose--write-debug-in-hot-paths)
- **[All]** `-f` format operator **MUST** be applied inside the argument-expression parentheses of cmdlet calls → [String Formatting in Cmdlet Arguments (`-f` Scoping)](#string-formatting-in-cmdlet-arguments--f-scoping)

### Language Interop and .NET (Quick Reference)

- **[All]** `System.Collections.ArrayList` is deprecated and **MUST NOT** be used in new code; use `System.Collections.Generic.List[T]` instead → [.NET Interop Patterns: Safe and Documented](#net-interop-patterns-safe-and-documented)
- **[All]** Generic collections **MUST** provide specific type T (List[PSCustomObject], not List[object]) → [.NET Interop Patterns: Safe and Documented](#net-interop-patterns-safe-and-documented)
- **[All]** Code **MUST NOT** grow PowerShell arrays with `+=` inside accumulation loops; use `System.Collections.Generic.List[T]` when an in-memory collection is required → [.NET Interop Patterns: Safe and Documented](#net-interop-patterns-safe-and-documented)

### Testing (Quick Reference)

- **[All]** New functions **SHOULD** have corresponding Pester tests when testability is a project requirement → [Testing with Pester](#testing-with-pester)
- **[All]** Test files **MUST** use `*.Tests.ps1` naming convention → [Test File Naming and Location](#test-file-naming-and-location)
- **[All]** Tests **MUST** use Pester 5.x syntax (BeforeAll, Describe, Context, It) → [Pester 5.x Syntax Requirements](#pester-5x-syntax-requirements)
- **[All]** Tests **SHOULD** use Arrange-Act-Assert pattern in test cases → [Test Structure: Arrange-Act-Assert](#test-structure-arrange-act-assert)
- **[All]** Tests **MUST** verify all documented return codes for functions → [Testing Return Code Conventions](#testing-return-code-conventions)
- **[All]** Test-* functions **MUST** have tests for both `$true` and `$false` cases → [Testing Return Code Conventions](#testing-return-code-conventions)
- **[All]** Tests asserting property names on `[pscustomobject]` **MUST** use order-insensitive comparisons → [Testing Property Names on PSCustomObject](#testing-property-names-on-pscustomobject)
- **[All]** Tests asserting strongly-typed array properties **MUST** check non-emptiness first, then assert the exact array type with `-is`; **MUST NOT** permit `[object[]]` fallback → [Testing Strongly-Typed Array Properties](#testing-strongly-typed-array-properties)
- **[All]** Test `BeforeAll` dot-sourcing **MUST** use the `Split-Path` + `Join-Path` two-step pattern; multi-segment `Join-Path` forms **MUST NOT** be used → [Test File Dot-Sourcing Pattern](#test-file-dot-sourcing-pattern)
- **[All]** Tests iterating a returned collection with `foreach` **MUST** assert non-emptiness before the loop → [Defensive Assertions Before Iteration and Indexing](#defensive-assertions-before-iteration-and-indexing)
- **[All]** Tests accessing specific indices of a returned collection **MUST** assert count before any indexed access → [Defensive Assertions Before Iteration and Indexing](#defensive-assertions-before-iteration-and-indexing)
- **[All]** Tests asserting that a call does not throw **MUST** use `{ ... } | Should -Not -Throw` and **MUST NOT** rely on `try/catch` plus negated assertions on exception text → [Asserting Successful Execution With Should -Not -Throw](#asserting-successful-execution-with-should--not--throw)
- **[All]** PSScriptAnalyzer CI integrations that emit host-native diagnostics **MUST** use the active CI host's command format → [PSScriptAnalyzer CI Diagnostic Output](#psscriptanalyzer-ci-diagnostic-output)
- **[All]** Host-neutral, local, and interactive PSScriptAnalyzer runs **SHOULD** use plain output; ambiguous, missing, or contradictory host detection **MUST** fall back to plain output → [PSScriptAnalyzer CI Diagnostic Output](#psscriptanalyzer-ci-diagnostic-output)
- **[All]** CI Pester discovery and execution **MUST** be scoped to the project-owned `tests/` tree or documented test root, not the repository root → [Running Pester Tests](#running-pester-tests)
- **[All]** CI Pester discovery and the Pester configuration `Run.Path` **MUST** share one test-root source of truth and **SHOULD** guard missing test roots cleanly → [Running Pester Tests](#running-pester-tests)

<!-- rationale-anchor: executive-summary-author-profile -->

## Code Layout and Formatting

### Indentation Rules

Indentation **MUST** use four spaces for all logical blocks, including param declarations, conditional statements (if/else), loops, and function bodies—tabs **MUST NOT** be used.

### Brace Placement (OTBS)

Bracing **MUST** strictly adhere to the "One True Brace Style" (OTBS): opening braces **MUST** be placed at the end of the statement line, and closing braces **MUST** start on a new line, aligned with the opening statement. This applies universally to functions, conditionals, and most script blocks.

### Exception: catch, finally, and else Keywords

> **Exception for `catch`, `finally`, and `else`:** These keywords are the major exception to this rule. To be syntactically valid, the `catch`, `finally`, and `else` (or `elseif`) keywords **MUST** follow the closing brace (`}`) of the preceding block on the **same line**.
>
> **Compliant `if/else`:**
>
> ```powershell
> if ($condition) {
>     # ...
> } else {
>     # ...
> }
> ```
>
> **Compliant `try/catch`:**
>
> ```powershell
> try {
>     # ...
> } catch {
>     # ...
> } finally {
>     # ...
> }
> ```

### Operator Spacing and Alignment

Whitespace **MUST** be used precisely to enhance clarity: a single space **MUST** surround operators (e.g., -gt, =, -and, -eq) and **MUST** follow commas in parameter lists or arrays, with no unnecessary spaces inside parentheses, brackets, or subexpressions. Line terminators **SHOULD** avoid semicolons entirely, as they are unnecessary and can complicate edits. Line continuation **SHOULD** eschew backticks, preferring natural breaks at operators, pipes, or commas where possible—though in v1.0-focused code, long lines (e.g., in comments or regex patterns) **MAY** be tolerated for completeness. Line lengths **SHOULD** aim for under 115 characters where practical, but verbose comments **MAY** exceed this; this is acceptable per flexible guidelines, as it prioritizes detailed explanations without sacrificing core code readability.

Code **MUST** use **exactly one space** on either side of an operator (e.g., `=`, `-eq`). Code **MUST NOT** add extra whitespace to vertically align operators across multiple lines. This ensures compliance with standard PSScriptAnalyzer rules.

### Multi-line Method Indentation

When a method call (like `.Add()`) is wrapped (e.g., in a `[void]` cast) and its parameter is a multi-line script block (like a hashtable or `[pscustomobject]`), an **additional** level of indentation **MUST** be used for the contents of that script block.

```powershell
[void]($list.Add(
        [pscustomobject]@{
            # This line is indented three times:
            # 1. For the opening parenthesis
            # 2. For the .Add() method
            # 3. For the [pscustomobject]@{...} block
            Key = $Value
        }
    ))
