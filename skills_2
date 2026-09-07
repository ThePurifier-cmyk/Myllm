***

### Part 2 (Lines 281 to 560)

```markdown
<!-- Context: Part 2 of 3 for LLM ingestion - PowerShell Writing Style Guide -->
<!-- markdownlint-disable MD013 -->

# PowerShell Writing Style (Part 2)

### Script and Function Naming: Approved Verbs

Functions **MUST** use approved PowerShell verbs. Run `Get-Verb` for the complete list. If a verb (like `Review` or `Check`) is not approved, choose the closest alternative (e.g., `Get-` or `Test-`). For the full reference, see [Microsoft's Approved Verbs](https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7.5).

> **Note:** The term *verb* in PowerShell describes any word implying an action, even if it isn't a standard English verb (e.g., `New`).

**Reserved verbs** (do not use): `ForEach` (`foreach`), `Ping` (`pi`), `Sort` (`sr`), `Tee` (`te`), `Where` (`wh`).

#### Similar Verbs for Different Actions

The following similar verbs represent different actions.

##### `New` vs. `Add`

Use the `New` verb to create a new resource. Use the `Add` to add something to an existing container or resource. For example, `Add-Content` adds output to an existing file.

##### `New` vs. `Set`

Use the `New` verb to create a new resource. Use the `Set` verb to modify an existing resource, optionally creating it if it doesn't exist, such as the `Set-Variable` cmdlet.

##### `Find` vs. `Search`

Use the `Find` verb to look for an object. Use the `Search` verb to create a reference to a resource in a container.

##### `Get` vs. `Read`

Use the `Get` verb to obtain information about a resource (such as a file) or to obtain an object with which you can access the resource in future. Use the `Read` verb to open a resource and extract information contained within.

##### `Invoke` vs. `Start`

Use the `Invoke` verb to perform synchronous operations, such as running a command and waiting for it to end. Use the `Start` verb to begin asynchronous operations, such as starting an autonomous process.

##### `Ping` vs. `Test`

Use the `Test` verb.

#### Common Verbs

| Verb (alias) | Synonyms to avoid |
| --- | --- |
| `Add` (`a`) | Append, Attach, Concatenate, Insert |
| `Clear` (`cl`) | Flush, Erase, Release, Unmark, Unset, Nullify |
| `Close` (`cs`) | |
| `Copy` (`cp`) | Duplicate, Clone, Replicate, Sync |
| `Enter` (`et`) | Push, Into |
| `Exit` (`ex`) | Pop, Out |
| `Find` (`fd`) | Search |
| `Format` (`f`) | |
| `Get` (`g`) | Read, Open, Cat, Type, Dir, Obtain, Dump, Acquire, Examine, Find, Search |
| `Hide` (`h`) | Block |
| `Join` (`j`) | Combine, Unite, Connect, Associate |
| `Lock` (`lk`) | Restrict, Secure |
| `Move` (`m`) | Transfer, Name, Migrate |
| `New` (`n`) | Create, Generate, Build, Make, Allocate |
| `Open` (`op`) | |
| `Optimize` (`om`) | |
| `Pop` (`pop`) | |
| `Push` (`pu`) | |
| `Redo` (`re`) | |
| `Remove` (`r`) | Clear, Cut, Dispose, Discard, Erase |
| `Rename` (`rn`) | Change |
| `Reset` (`rs`) | |
| `Resize` (`rz`) | |
| `Search` (`sr`) | Find, Locate |
| `Select` (`sc`) | Find, Locate |
| `Set` (`s`) | Write, Reset, Assign, Configure, Update |
| `Show` (`sh`) | Display, Produce |
| `Skip` (`sk`) | Bypass, Jump |
| `Split` (`sl`) | Separate |
| `Step` (`st`) | |
| `Switch` (`sw`) | |
| `Undo` (`un`) | |
| `Unlock` (`uk`) | Release, Unrestrict, Unsecure |
| `Watch` (`wc`) | |

#### Communications Verbs

| Verb (alias) | Synonyms to avoid |
| --- | --- |
| `Connect` (`cc`) | Join, Telnet, Login |
| `Disconnect` (`dc`) | Break, Logoff |
| `Read` (`rd`) | Acquire, Prompt, Get |
| `Receive` (`rc`) | Read, Accept, Peek |
| `Send` (`sd`) | Put, Broadcast, Mail, Fax |
| `Write` (`wr`) | Put, Print |

#### Data Verbs

| Verb (alias) | Synonyms to avoid |
| --- | --- |
| `Backup` (`ba`) | Save, Burn, Replicate, Sync |
| `Checkpoint` (`ch`) | Diff |
| `Compare` (`cr`) | Diff |
| `Compress` (`cm`) | Compact |
| `Convert` (`cv`) | Change, Resize, Resample |
| `ConvertFrom` (`cf`) | Export, Output, Out |
| `ConvertTo` (`ct`) | Import, Input, In |
| `Dismount` (`dm`) | Unmount, Unlink |
| `Edit` (`ed`) | Change, Update, Modify |
| `Expand` (`en`) | Explode, Uncompress |
| `Export` (`ep`) | Extract, Backup |
| `Group` (`gp`) | |
| `Import` (`ip`) | BulkLoad, Load |
| `Initialize` (`in`) | Erase, Init, Renew, Rebuild, Reinitialize, Setup |
| `Limit` (`l`) | Quota |
| `Merge` (`mg`) | Combine, Join |
| `Mount` (`mt`) | Connect |
| `Out` (`o`) | |
| `Publish` (`pb`) | Deploy, Release, Install |
| `Restore` (`rr`) | Repair, Return, Undo, Fix |
| `Save` (`sv`) | |
| `Sync` (`sy`) | Replicate, Coerce, Match |
| `Unpublish` (`ub`) | Uninstall, Revert, Hide |
| `Update` (`ud`) | Refresh, Renew, Recalculate, Re-index |

#### Diagnostic Verbs

| Verb (alias) | Synonyms to avoid |
| --- | --- |
| `Debug` (`db`) | Diagnose |
| `Measure` (`ms`) | Calculate, Determine, Analyze |
| `Ping` (`pi`) — *deprecated; use `Test`* | |
| `Repair` (`rp`) | Fix, Restore |
| `Resolve` (`rv`) | Expand, Determine |
| `Test` (`t`) | Diagnose, Analyze, Salvage, Verify |
| `Trace` (`tr`) | Track, Follow, Inspect, Dig |

#### Lifecycle Verbs

| Verb (alias) | Synonyms to avoid |
| --- | --- |
| `Approve` (`ap`) | |
| `Assert` (`as`) | Certify |
| `Build` (`bd`) — *PS 6+* | |
| `Complete` (`cp`) | |
| `Confirm` (`cn`) | Acknowledge, Agree, Certify, Validate, Verify |
| `Deny` (`dn`) | Block, Object, Refuse, Reject |
| `Deploy` (`dp`) — *PS 6+* | |
| `Disable` (`d`) | Halt, Hide |
| `Enable` (`e`) | Start, Begin |
| `Install` (`is`) | Setup |
| `Invoke` (`i`) | Run, Start |
| `Register` (`rg`) | |
| `Request` (`rq`) | |
| `Restart` (`rt`) | Recycle |
| `Resume` (`ru`) | |
| `Start` (`sa`) | Launch, Initiate, Boot |
| `Stop` (`sp`) | End, Kill, Terminate, Cancel |
| `Submit` (`sb`) | Post |
| `Suspend` (`ss`) | Pause |
| `Uninstall` (`us`) | |
| `Unregister` (`ur`) | Remove |
| `Wait` (`w`) | Sleep, Pause |

#### Security Verbs

| Verb (alias) | Synonyms to avoid |
| --- | --- |
| `Block` (`bl`) | Prevent, Limit, Deny |
| `Grant` (`gr`) | Allow, Enable |
| `Protect` (`pt`) | Encrypt, Safeguard, Seal |
| `Revoke` (`rk`) | Remove, Disable |
| `Unblock` (`ul`) | Clear, Allow |
| `Unprotect` (`up`) | Decrypt, Unseal |

#### Other Verbs

| Verb (alias) | Synonyms to avoid |
| --- | --- |
| `Use` (`u`) | |

### Script and Function Naming: Nouns

**Noun Singularity:** The noun **MUST** be singular, even if the function returns multiple objects. This is a core PowerShell convention (e.g., `Get-Process`, `Get-ChildItem`) and corresponds to the **PSScriptAnalyzer `PSUseSingularNouns`** rule. The noun describes the *type* of object the function works with, not the *quantity* of its output.

- **Correct:** `Get-Process` (returns *many* process objects)
- **Incorrect:** `Get-Processes`
- **Correct:** `Expand-TrustPrincipal` (operates on *one* principal node, even if it results in many values)
- **Incorrect:** `Expand-TrustPrincipals`

### Module Naming: Noun-Based Containers

**Modules are treated as .NET Namespaces or Class Libraries (Containers), not Actions.** Therefore, Module names **MUST** be **PascalCase Nouns** or **Noun Phrases**.

- **Correct:** `ObjectFlattener`, `NetworkManager`, `DataParser`
- **Incorrect:** `FlattenObject`, `ManageNetwork`, `ParseData`

Module names **MUST NOT** be compromised for the sake of keyword searching.

**[Modern]** In module-based code, the **Module Manifest (`.psd1`)** handles discoverability. The `Tags` key in the manifest **MUST** be populated aggressively with relevant keywords (including verbs) to ensure the module is found during searches, while keeping the architectural name pure.

### Do Not Use Aliases

Aliases (e.g., `gci`, `gps`) or abbreviated forms **MUST NOT** appear in the code. Even common operations **MUST** use full command names.

Furthermore, **Modules MUST NOT export "Compatibility Aliases"** solely to bridge a gap between a module name and a command name (e.g., do **not** export `Flatten-Object` when the correct command is `ConvertTo-FlatObject`).

**Exceptions:**

Aliases **MAY** only be exported in a Module Manifest if they provide genuine short-hand convenience for *interactive* users (e.g., `cfo` for `ConvertTo-FlatObject`) and are strictly documented as optional. They **MUST NOT** be used to mask non-approved verbs.

### Parameter Naming

**Parameter names** **MUST** use PascalCase and be highly descriptive (e.g., `$ReferenceToResultObject`, `$StringToProcess`, `$PSVersion`). The `ReferenceTo` prefix for `[ref]` parameters signals **pass-by-reference** semantics. [ref] **MUST** be used only when data needs to be written back to the caller’s scope; for passing complex objects that do not need modification, pass by value.

### Local Variable Naming: Type-Prefixed camelCase

Local variables follow a **Hungarian-style notation** combining a **type-hinting prefix** with **descriptive `camelCase`**. **The descriptive portion of each name—everything after the type prefix—MUST be fully spelled out; abbreviations and shorthand are not permitted.**

- **Prefixes:** `$str` (string), `$int` (integer), `$dbl` (double), `$bool` (boolean), `$arr` (array), `$obj` (object/default), `$hashtable` (hashtable), `$list` (generic list), etc.
- **Default prefix — `obj`:** Use `$obj` for any .NET type that does not have a dedicated approved prefix above. This includes enum values (e.g., `$objActionPreference`), complex .NET reference types (e.g., `$objMemoryStream`), and `[pscustomobject]` instances (e.g., `$objResult`).
- **Open-ended list:** The "etc." above means additional descriptive prefixes such as `$ref` and `$version` are permitted when they provide immediate type clarity (e.g., `$refLastKnownError`, `$versionPowerShell`). However, authors **SHOULD NOT** invent ad hoc abbreviated type-name prefixes when a canonical documented prefix already exists. Specifically:
  - Do **not** use `$enumActionPreference`; use `$objActionPreference` instead (enum values fall under the default `$obj` prefix).
  - Do **not** use `$hashSeen`, `$hashResult`, etc.; use `$hashtableSeen`, `$hashtableResult`, etc. instead (the canonical prefix for hashtables is `$hashtable`, not the abbreviated `$hash`).
- **Descriptive Name:** The name **MUST** be **fully spelled out**.

**Examples:**

- `$strPolicyString` (not `$strS` or `$strPolicy`)
- `$objMemoryStream` (not `$objMs` or `$stream`)
- `$arrStatements` (not `$arrStmt` or `$stmts`)
- `$strMessage`
- `$intReturnValue`
- `$boolResult`
- `$arrElements`
- `$hashtableSettings`
- `$objActionPreference`
- `$objResult`
- `$refLastKnownError`
- `$versionPowerShell`

<!-- rationale-anchor: local-variable-naming-defensive-design-philosophy -->

### Path and Scope Handling

Code **SHOULD** avoid relative paths (`.`, `..`) and the **home directory shortcut `~`** entirely. This is due to:

- `~` behavior varies by provider (FileSystem vs. Registry vs. others).
- Relative paths depend on `[Environment]::CurrentDirectory`, which **MAY** diverge from `$PWD` when calling .NET methods or external tools.

Instead, **explicit scoping** **SHOULD** be used:

```powershell
$global:ErrorActionPreference
